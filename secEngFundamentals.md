# Security Engineering Fundamentals

## Introduction

### Outline main aspects

1. Security engineering is about reducing risk business operations by building security systems and processes
1. CIA triad: confidentiality - integrity - availability, which are the foundation for our information security understanding
1. Encryption and Hashing
1. Risk = Threat x Vulnerability x Impact
1. Cybersecurity aims building systems to protect against cyber attacks

**Big picture**

1. What is security engineering?
1. Why is it important? What are some common strategies?
1. What are the foundational security principles? Through them is it possible to build expertise?
1. What are the best encryptions to use? What are the best practices about them?
1. How to evaluate and prioritize risk?
1. Why is it important audit and what is its role?

## What is security engineering?

Understand functions and techniques employed by security engineer:

1. Offense vs. Defense
1. Roles and specializations
1. Big security issues
1. Other fields

**What is the difference between a security analyst and a security engineer?**

Even though the roles are similar, they are not the same.
1. Analyst:
    * responsible for utilizing tools, processes, and systems to protect an organization from threats
    * he will utilize the SIEM and action on the alerts in an effort to protect the organization from attacks. He will provide input on requirements and will help define requirements from a SIEM user perspective. He will utilize SIEM to analyze alerts and logs. Security Analysts are typically tasked with ensuring the security of an organization by utilizing security tools and processes. 
1. Engineer
    * help builds systems, processes and tools
    * SIEM is developed and deployed by engineer based on his understand of the environment to get requirements for the SIEM following requirements to select a tool. After that SIEM will be installed and deployed. And yet he will ensure data sources will be logged in the SIEM.

**What is the main difference between them?**

**While analyst utilizes the security tools and systems, engineers are tasked with building and deploying security tools and systems.**

## Why security engineering?

I consider security engineering to be essential to an organization because even more the organization because even more the organizations have a lot of sensible information that criminals want. **An organization's information is like commodity and security engineering helps to protect it from leaks**. From this point of view, security engineering is essential as much as organization's sensible information. We, security engineering, need to protect against risks that we know and risks we’ve never seen.

**Information Security give support to IT operations, that, in your turn, it gives support to business operation.**

## Offensive and Defensive engineering

1. Defensive security team: they protect the company by strengthening its defenses; they establish **security measures**, taking an inside out view of the organization. This team is as also known **as the blue team**, and they are characterize as: **perform vulnerability scans, analyze logs, deploy security tools (SIEMS, endpoint protection, etc), establish security processes**; patching an unpatched system, scanning for vulnerabilities, deploying least privilege throughout an organization.
1. Offensive security team: they approach the situation **from the perspective of an attacker with permission**. **Permission is the key difference between offensive and external hacker**. This team is as also know the **red team**, and they are characterize as: **penetration testing, social engineering, phishing**; exploiting a vulnerability to determine likelihood or impact, intercepting communications to map out a network.

**A holistic strategy of building a strong defense and testing with offensive tactics is extremely important.**

1. **From the defense perspective, we can**: Scan the network to identify vulnerable systems; Patch the affected systems; The best remediation effort is to patch the affected systems when the vendor releases the patch; Create a mitigation plan in the interim: What additional steps can be taken to prevent/limit the exposure? In some cases, a vulnerability may be reported and a patch is not yet available; In many cases, patching takes time (testing, change management process, etc). There will be a period of time that the systems are vulnerable before you can patch. Add new signatures to monitoring solutions (SIEM, HIDS, NIDS, etc); Check logs and monitoring systems for any indicators of attack/compromise.
1. **From the offensive perspective, we can**: Create POC of a successful exploit; this will help understand and illustrate the impact of the vulnerability. Can answer questions such as: What is the difficulty of the exploit? Can it be done by a malicious user with little to no access/knowledge of the infrastructure? If the vulnerability is successfully exploited, what damage can be caused? (data leak, root access, etc). Once patching has been complete: Confirm that the systems are no longer vulnerable by performing remediation testing. Identify IOC/IOA and give information to the defensive team for monitoring. Test defenses by simulating attack/compromise.

## Roles and specialization

There are three level of roles in information security and both share the same ultimate goal, which is reduce risk.

1. Strategy: CISO, chief information security officer, and directors.
1. Execution: security engineers (Application security focuses on securing software and the process to develop software, Network/systems security focused on securing IT systems and networks, incident response: how to quickly respond and react to security incidents or breaches, forensics: understand the root cause for security incidents by performing forensic analysis)), security analyst, security archtects.
1. Compliance: compliance analyst depends on the industry you're in as well as the type of data you store or process. For instance, healthcare (HIPPAA), process credit card (PCI-DSS)

Another summary about roles in information security
* Security engineer builds security solutions
* Security analyst utilizes security systems
* Forensics performs analysis to collect evidence of a breach
* Incident response is responsible for the detection and eradication of cyber attack events
* Penetration tester performs attacks against a system in order to discover weaknesses

**Think** What is unique about security engineering and why is it important, considering the cost of improper security?

The role of an security professional is to protect the organization from potential risks. The difference is how they go about it. Some role are more focused on the figuring out what a malicious actor may do, while others are focused on protecting against those actions. Each role **is an important piece of the overall security posture**.


**Big Security Issue**

**It is important to understand what can impact your organization**. It helps to break up some functions of security and solve the issues that pertain to your organization. Some examples of big security issues that have impacted the world:

1. Heartbleed: it is a vulnerability in a popular open source library OpenSSL. This vulnerability allowed an attacker to circumvent the encryption provided by this library. The result is an attacker could view encrypted data in transit.
1. Ransomware: it is an attacker renders your data unusable by encrypting it and demands a ransom to get a key to decrypt your data.

**Think** What the organization needs to be prepared to defend? Build software? Need data protection? 

1. user security: you need to be aware of attacks that target users attacks such **as phishing**, which is an attempt to circumvent security measures through digital communication such as email and, most commonly, an attacker is trying to get a user to click on a malicious link by crafting a fake email; **as ransomware**, which is an attacker renders your data unusable by encrypting it and demands a ransom to get a key to decrypt your data. Phishing is a common vector for this type of attack; as **social engineering**, which is A malicious party will get a user to grant them access that they shouldn't have by masquerading as a legitimate party.
1. application security: deals with the security of custom-built applications. Also known as product security.
1. network/infrastructure security: network and internal infrastructure.
