# Security Engineer

## Introduction to systems security

**No system is completely secure.** A system is said to be secure if its resources are used and accessed only by approved users, processes and services. **With constant changes to system services and processes**, security of those services needs to be constantly updated to ensure that the required best practices are in place.

Security roles are essentially three:
1. Provide a secure environment
1. Enable safe operations (it enables safe operation of applications and services implemented on the organization's IT systems)
1. Protect data

**IT security control must be proportional to the complexity of IT environment based on those three roles**.

**Security is everyone’s job**! **Humans are often the weakest links in any technological process**. It takes years and teams of security engineers to implement strong and effective security controls, **but it takes just one careless employee to accidentally infect the whole network**.

**Security should be a priority discussion at all levels in an organization**. This means from the C-level executives to Engineers and IT personnel in the company.

Let's look closer at five key:
1. 3rd party vulnerabilities
1. authentication
1. authorization
1. isolation
1. auditing

## 3rd party vulnerabilities

### Big picture and intuition

* Understanding the OS's security model as it forms **the first layer of defense in a system**. If you lose the OS, probably your APP is lost as well.
* How to interpreting CVE advisories and their significance in measuring the impact of security vulnerabilities?
* How to identify vulnerabilities **through automated scanning tools** to quantify and prioritize system vulnerabilities?
* How to build a vulnerability management plan and define **security baseline configurations** and requirements in an enterprise environment?
* How to design an initial setup for building a secure baseline? This would **ensure** that **every existing or new system being added in the larger network would have a fixed set of updates and patches**. This can greatly **reduce the overhead of system patching and will add consistency in building up systems across a larger network consisting of thousands of machines**. If the overhead is reduced, the network overload is reduced as well. And it is reduced the probability of DoS.
* How to identify and patch security vulnerabilities in an automated manner? This helps improve the speed of responding to a security exposure caused by an insecure or unpatched system in the network.

Why we are learning these topics?

* To prevent initial compromise on a system and then to the larger network the compromised system is a part of.
* To look at security incidents as an enterprise wide issue rather than a single system issue.
* To understand how software and system vulnerabilities are patched and secured. To patch and mitigate them across the network to ensure that there are no holes for the attackers to gain a foothold of the network.
* **To understanding zero days** and **other critical vulnerabilities** and defining a mitigation plan.
* To identify the gaps and quickly mitigating them across the network can contain the risk and improve system security.
* **Vulnerabilities exist in the operating system or other third party software and libraries installed on the system**. A point to note here is that **a fully patched system can also be prone to a credential compromise or malware attack**. Hence, vulnerability cannot be introduced through either of those two ways. It can only be introduced through third party software and operating systems installed on the system.

### OS protection principles

**The basis of OS protection is separation of its components into an inner layer, middle layer, and outer layer**. This ensures that there are proper protection mechanisms in place to **guarantee that different levels can be protected from one another**. Operating systems perform the task of orchestrating the flow of information between the three separated components.

* First level: User programs and applications
* Second level: Process, Memory, Filesystem, I/O interface management, protections of resources and networking
* Third level: hardware and BIOS & firmware.

#### Layered Architecture of an Operating system 

**Events inside an OS are managed through a set of processes**. **A process is** an instance of a program that has a specific purpose. **A software can** invoke multiple processes based on the instructions received from the end user. **The OS executes** those processes and provides the result to the software or application. **Due to the separation model of OS**, **processes are executed in layered rings**. **Each ring has its own level of permissions and privileges**. **The central ring has the highest privileges while the outermost ring has the least amount of privilege**.

There are two major advantages that the OS achieves by using this layered approach towards process execution: 
    1. **Stability**: A process failure in outer rings can be easily recovered without a system crash as only the innermost ring has access to the CPU and memory. 
    1. **Defense in Depth**: These rings act as layers of defense that the attacker must compromise to gain full access to the system

1. **Ring 0 (central ring)**: it is the **innermost ring and has the highest access privilege**, which means that **it has access to the OS's kernel**. Processes running in kernel mode **can affect the entire system**. Processes running at this level will have direct access to the CPU and the system memory. 
1. **ring 1**: it is responsible for **controlling and managing interaction with the hardware devices connected to the OS**.
1. **ring 2**: it **handles the storage-related operations like managing data retrieval from the filesystem, accessing database services**.
1. **ring 3**: it is the **least privileged ring** which directly interacts with the end-user, and this is also known as the user mode. Software and applications run in this region and receive actions from the end user.

#### User mode & kernel mode

**User mode denotes lesser privileged access**, whereas kernel mode is everything else. **A process in user mode does not have direct access to hardware, CPU, or memory**. User mode does this by creating system calls to the kernel mode, which has complete access to the hardware, CPU & memory.

### Introduction to CVE

CVE is acronym for common vulnerabilities and exposures, which means a dictionary that provides, in a standardized way, definitions for publicly disclosed cybersecurity vulnerabilities and exposures. This helps to quickly and accurately identify a vulnerability, its severity, and the overall impact on the system where it exists.

**There are quite a few well known CVE advisory databases that can be used to track reported vulnerabilities in software and libraries**. These databases provide nearly similar information with slightly different formats. The most common are:

https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2019-0708
https://cve.mitre.org/cve/
https://www.cvedetails.com/cve-details.php?t=1&cve_id=CVE-2019-0708
https://www.exploit-db.com/
https://nvd.nist.gov/

### CVSS

The Common Vulnerability Scoring System, or CVSS, provides a severity score in the range of 1 to 10. 1 is the lowest and least severe score with 10 being the highest severity. CVSS score's severity is dependent on how easy it is to execute the exploit, does it lead to remote code execution, and if it leads to a complete system takeover and information disclosure. As a security engineer, you receive a bug report about your company's video chat product and you have to decide the severity score. Which of these indicators will you look for to mark the bug as a severe security vulnerability?

### OpenVAS Scanning

The OpenVAS tool is part of the commercial vulnerability management product family "Greenbone Security Manager" (GSM).

Links: https://www.openvas.org/
https://hub.docker.com/r/atomicorp/openvas

### Planning and management

Vulnerability planning and management must be done in four essential steps:

1. identify (with tools)
2. prioritize vulnerabilities
3. remediate
4. verify (with tools to scanner)

Some of the advantages of such a program include: Identification of known security exposures in your network before attackers find and exploit them. It also allows us to quickly identify any new vulnerability and patch it. Such processes help create an inventory of all the devices on the network, including purpose and system information. This helps in increasing the visibility of the network and also improves upgrade management programs.

### Boot loader secure

We can secure the BIOS and the boot loader by password protecting them. This would ensure that the BIOS and the boot loader can be protected from unauthorized users who have physical access to systems. With password protecting the boot loader, we can:
    * Prevent an attacker from booting into single user mode and becoming the root user of the system
    * Prevent an attacker from accessing the GRUB console and using the command's interface to change its configuration
    * Prevent booting of non-secure Operating Systems by enabling dual boot system 

**An unsecured Boot loader can allow the attacker to change the default boot device to a removable media like USB and launch a secondary OS through it**. The attacker can also boot into the current operating system in single user mode and become the system root.

### Security baseline

A Security Baseline **defines a set of basic or mandatory security objectives which must be uniformly met by all the systems in a large enterprise network**: the **minimum set of security requirements that should be present**. This would **ensure that a uniform level of security practices and measures have been followed across all the digital assets within an enterprise**. Security baseline is defined by segregating various system access methods into individual groups: Access Control, Network Access, Physical security, and Software & Applications.

Some of the examples of a security baseline would include: 
* **Installing only applications that are professionally needed and removing all others**. 
* **Restricting access to privileged accounts** (e.g. root, sudo, admin) **to a small, controlled group of users**. 
* **Restricting access to shared folders**.
* **Protecting access to the BIOS by a non-default password**. 
* **Ensuring that the only versions which are officially supported by the corresponding operating system or software vendor are installed**. 

Defining a security baseline for your organization is important because:
* It simplifies the process of implementing security controls uniformly across all endpoints. 
* It streamlines the process of implementing security best practices at all levels. 
* It reduces the maintenance overhead and the attack surface. 

### Principle of least privilege (PoLP)

PoLP is the idea of ensuring that **any user, process, or program should only have the bare minimum privileges necessary to perform their daily functions**. It requires a deeper understanding of the system requirements and access levels inside the organization at various levels. The principle of least privilege can also be referred to as the principle of minimal privilege (PoMP) or the principle of least authority (PoLA). 

**No softwares other than the necessary ones should be installed**. This decreases the attack surface. The IT team can be asked to uninstall the software from all the systems and from the baseline image that they are using.