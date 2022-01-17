# Security Engineer

## Isolation

Restrict jail is a operation with chroot that changes the apparent root directory for a running process and its children. It allows us to change the root directory **to anything other than /.**
This increases the protection of the system as a process and does not let the user access other critical resources of the system. It locks down the process and the logged-in user sees only the directory that the process is running in. The newly created artificial root directory becomes the chroot jail. Chroot allows an administrator to control access to a service or filesystem while controlling exposure to the underlying server environment. **for a chroot process to successfully start, the chroot directory must be populated with all required program files, configuration files, device nodes, and shared libraries at their expected locations.**

https://www.redhat.com/sysadmin/set-linux-chroot-jails

Steps for Creating a Jailed Environment:

* **step 1**: it must be defined **the requirements and build the initial base for creating the jailed environment**. This would involve **creating the restricted user and group accounts, defining the directories and permissions, installing the required services (like ssh, apache, nginx), etc.**

* **step 2**: now it will have **to set up the service we want to get jailed**. This can either involve **creating a copy of the service with required dependencies or making configuration changes in the service to restrict accessing locations protected through chroot**.

* **step 3**: Once we have **defined the environment and prepared the service**, we now need to **initialize and test out our new service to ensure that the jailed restrictions are properly in place**.

* **step 4**: Test Your Restrictions: This is an essential step to ensure that your jailed setup satisfies the security restrictions that you want to impose.

1. / Linux root
    * usr
        * src
        * bin
        * local
    * bin
    * home
        * erange
        * / jailed root
            * upload
            * download


Lab: implementing a restricted bash shell: We want to build a bash environment with chroot jail restriction. This bash program will run in the modified environment and will not be able to access the files outside of the designated directory tree. As an example, we will restrict the shell to only allow the ls command.

* **step 1**:
    * to create a directory we want to create our restricted shell service.
    * to create the sub-directories to store the binaries and packages which are required by the bash terminal to execute along with the commands that we want to permit inside this shell.

    mkdir /home/jailrestricted
    cd /home/jailrestricted

    mkdir -p bin lib64/x86_64-linux-gnu lib/x86_64-linux-gnu

* **step 2**: 
    * since we want to run the bash and **ls command binaries**, we will have to copy the binaries and their required packages to this new location.
    * We can use the **which command** to find the location of ls and bash command binaries in the system.
    * We can then copy them over to the bin directory of our /home/jailrestricted/ directory. 

    cp $(which ls) ./bin/
    cp $(which bash) ./bin/

    ldd $(which bash)

    cp /lib/x86_64-linux-gnu/libtinfo.so.5 lib/x86_64-linux-gnu/
    cp /lib/x86_64-linux-gnu/libdl.so.2 lib/x86_64-linux-gnu/
    cp /lib/x86_64-linux-gnu/libc.so.6 lib/x86_64-linux-gnu/
    cp /lib64/ld-linux-x86-64.so.2 lib64/

    ldd $(which ls)
    cp /lib/x86_64-linux-gnu/libselinux.so.1 lib/x86_64-linux-gnu/
    cp /lib/x86_64-linux-gnu/libc.so.6 lib/x86_64-linux-gnu/
    cp /lib/x86_64-linux-gnu/libpcre.so.3 lib/x86_64-linux-gnu/
    cp /lib/x86_64-linux-gnu/libdl.so.2 lib/x86_64-linux-gnu/
    cp /lib64/ld-linux-x86-64.so.2  lib64/
    cp /lib/x86_64-linux-gnu/libpthread.so.0 lib/x86_64-linux-gnu/
    cd ..

    * We can use the **tree command** to look at the directory structure of the jailrestricted directory. 

* **step3**:
    * our initial configuration and setup is ready, we only need to change the root to the jailrestricted directory, along with the path to the shell. 
    
    sudo chroot jailrestricted/ bin/bash

Lab: SFTP Chroot Jail to Allow or Deny Access to Directories

* **step1**: 

    groupadd remoteusergroup
    usermod -g remoteusergroup -s /bin/false remoteuser 
    useradd -s /bin/false -m -d /home/remoteuser remoteuser
    passwd remoteuser

    The -s /bin/false option sets the user’s login shell. By setting the login shell to /bin/false, this user would not be able to login to the server via SSH. The -m -d /home/remoteuser option creates the home directory for the user. 

    sudo chown root: /home/remoteuser
    sudo chmod 755 /home/remoteuser

    sudo mkdir /home/remoteuser/{uploads, downloads}
    sudo chmod 755 /home/remoteuser/{uploads, downloads}
    sudo chown remoteuser /home/remoteuser/{uploads, downloads}

* **step2**: SFTP is a subsystem of SSH and supports all SSH authentication mechanisms.
    * One last change will be to update the sshd_config file to consume this group as the chroot restricted group instead of just the remoteuser. Match User remoteuser with Match Group remoteusergroup. Now restart the ssh service. 