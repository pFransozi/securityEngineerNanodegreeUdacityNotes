# Security Engineer

## Mandatory Access Control

It is **a security implementation** where the **OS (and not the user) controls the access** to data objects by subjects. Each **subject and object have a set of security attributes** that are validated (through policy rules) by the operating system before granting permission to perform the action. The validation or policy rules are centrally controlled by the operating system and cannot be modified by the ordinary user.

**In a Linux MAC-based process** the flow would look like: an administrator defines the validation policies and assigns security attributes, confidentiality levels, and clearances for accessing different projects and types of resources. Each subject (user or resource that accesses data) and object (files, databases, ports, etc.) is then assigned a set of attributes.

When a system call is made by a subject to access an object, the operating system examines the subject’s security attributes against the validation policies to either allow or deny the action.

### How Mandatory Access Control Improves Security

One of the biggest concerns with the Linux OS **is the danger presented by the root account**. As the SU-account, it has the power to control all files and processes. If the **root account, or a process that runs with its privileges, is compromised**, an attacker can take control of the system and its data. It is often the root user account that gets compromised and exposes everything to the attacker.

**A more secure approach would be to limit or eliminate the need for a root account, and shift the power from the user accounts to the owner of the system. This is the approach that MAC adopts.** Implementing **a strong MAC policy will prevent an attacker or system exploit from gaining complete access over the system**.

Unlike in DAC, if a process with a certain privilege level is compromised, everything accessible to that user is now exposed to the attacker. The rule management in MAC happens through the kernel which eliminates the need for a root or super-user account.

In DAC, the resource owner can decide who else can access the resource. The root user is a super-user and can make any changes to the system.

### AppArmor is a MAC (Mandatory Access Control) system


It is a kernel enhancement to confine programs to a limited set of resources. **AppArmor provides the ability to bind access control attributes to programs rather than to users**. AppArmor **restrictions are defined by creating profiles which are loaded into the Linux kernel during the system boot**.

The profiles can have two modes:
    * enforcement: Profiles loaded in enforcement mode will be strictly applied on the target's requests by taking the respective action (for example, denying the request). A policy violation will also be reported to logging and monitoring tool like syslog or audited.
    * complain: profiles loaded in complain mode will not enforce the policy but instead report policy violation attempts for monitoring and alerting purposes.

Lab: 

All AppArmor profiles are located in /etc/apparmor.d. To begin creating an AppArmor profile for Nginx, use the aa-autodep command of apparmor-utils.

aa-autodep nginx

This will create a new file called usr.sbin.nginx. Launch the file and view its content:

# Last Modified: Mon Jul 27 07:22:49 2020
#include <tunables/global>

/usr/sbin/nginx flags=(complain) {
  #include <abstractions/base>

  /usr/sbin/nginx mr,

}

This tells us that the profile is currently set in complain mode. In order to allow Nginx to only access the /data/www/public folder and deny access to /data/www/private folder, simply add the two lines to the profile:

/data/www/public/* r,
deny /data/www/private/* r

This tells AppArmor to only allow the public* directory to be readable for the Nginx process and deny access to the private directory. Restarting the Nginx and AppArmor process will allow the new changes to take effect.

The new usr.sbin.nginx profile will look like:

# Last Modified: Mon Jul 27 07:22:49 2020
#include <tunables/global>

/usr/sbin/nginx flags=(complain) {
  #include <abstractions/base>

  /usr/sbin/nginx mr,
  /data/www/public/* r,
 deny /data/www/private/* r

}

### Advance Protections: Memory Overflow Attack & Defense

One increasingly used technique is memory corruption, and the most common example of memory-based attacks is a Buffer Overflow Attack. To better understand buffer overflow attacks, we need to have an understanding of how memory management works in operating systems. 

Address Space Layout Randomization (ASLR) is a memory-protection process for operating systems that guards against buffer overflow attacks. It involves randomly positioning the base address of an executable as well as the position of libraries, heap, and stack, in a process's address space. With ASLR, the entry point of a process is randomized each time it is executed. It is never in a fixed location. This is why it is called Address Space Layout Randomization. With this randomness, exploiting a buffer overflow becomes difficult as it's not easy to guess the location of the return address and overwrite it with the address of shell-code.

Usually, ASLR is now enabled by default. You can check it by using the two commands below:

cat /proc/sys/kernel/randomize_va_space
> 2
sysctl -a --pattern randomize
kernel.randomize_va_space = 2

The value (2) above indicates that ASLR is working in full randomization mode. The possible output values can be:

0 = Disabled
1 = Conservative Randomization
2 = Full Randomization

* ASLR doesn't mitigate exploits. It only makes it harder for attackers to execute it. It is still the responsibility of the code owners or software developers to mitigate the bugs in their codes which can potentially lead to a buffer overflow.
* Older versions of operating systems do not have in-built support for ASLR leaving those systems vulnerable to buffer overflow attacks.
* Modern exploits can even bypass ASLR by using advance exploiting techniques. Hence, an in-depth defensive security approach should be practiced.