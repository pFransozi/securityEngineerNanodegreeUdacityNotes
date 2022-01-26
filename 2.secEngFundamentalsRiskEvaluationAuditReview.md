# Security Engineering Fundamentals

## Risk Evaluation

**The ability to evaluate risks** is a critical responsibility for a security engineer.

**Big picture to developing your intuition about risk evaluation**

Most organizations’ information technology operations are incidental and performed in order to support the products or services they are offering. **As security engineers, our ultimate goal is to reduce the risk of those operations**. We (security engineer) **need to help business leaders understand the risk, their impact, and how to remediate them**. **Security help the operation of IT and IT help the operation of the business**.

Risk formula is: THREAT x VULNERABILITY x IMPACT;
AND: THREAT x VULNERABILITY = LIKELIHOOD;
SO: RISK = LIKELIHOOD x IMPACT

How to prioritize the risk?
**The key is evaluating risk to prioritizing work.** But for that, it need understand my company in order to appropriately asses risk.

Let's take a closer look at the concepts.

1. **vulnerability**: a vulnerability **is a weakness in a system or software that can be exploited** to make a system behave in an unintended way. A un-patched system is an example of vulnerability.
1. **threat**: **a threat is a hypothetical event wherein an attacker could use (or exploit) a vulnerability**.

## Asset Valuation

In the context of information security, an asset is anything of value to a business that is related to information system.

**To think about**: Why is it important to understand the value of an asset for the purposes of information security? **Without understanding the value it is difficult to recommend a good remediation plan**. **It is important to understand the value of the asset you're trying to protect**. **This helps the business make an informed decision on whether or not we should deploy recommended mitigation strategies**.

Say you have an asset that you've valued at $1 million, for instance. This asset is an outdated server and in order to properly protect it, we must spend $5 million. In this case it may be better to just decommission the asset and buy/build something new. You wouldn't spend $5 million to protect $1 million.

**To think about**: While it might not seem important to someone who isn't a security professional, it's important to be able to use **the right terminology to describe events**. Describe the difference between a threat and a vulnerability. **A threat is** a hypothetical event wherein an attacker could use (or exploit) a vulnerability. **It is a potential threat**. **A vulnerability is something concrete because it is a weakness in a system or software that can be exploited any time to make a system behave in an untended way**. A threat is exploited by a vulnerability.

**To think about**: Injection has been part of the OWASP Top 10 since its inception. What is an injection vulnerability and why is it so dangerous? Injection flaws occur when **an attacker can send hostile data to an interpreter**. It is dangerous because injection can result in data loss, corruption, or disclosure to unauthorized parties, loss of accountability, or denial of access.

## Mitigation and prioritizing risk

**Mitigation is an action taken to reduce the risk of a given threat.**

**Remember**: Risk = Threat x Vulnerability x Impact (asset valuation)
And: (Threat = Potential Event) x (Vulnerability = Weakness) = Likelihood
**Impact = asset valuation X business impact X reputation damage**. Remember, these aren't exact values. This is a formula that can be used to estimate risk for your organization.
Or: Impact: measures the consequences of a successful attack.

There is no neutral measure of threat, vulnerability and impact.

## CVSS

Common vulnerability scoring system (CVSS) provides a way to capture the principal characteristics of a vulnerability and produce a numerical score reflecting its severity.

## Threat models

Threat Modeling is the process for identifying potential security threats and vulnerabilities, evaluating the risk, determining mitigation for such threats, and prioritizing any mitigation or fixes to the system.

**Threat Model Frameworks: STRIDE, DREAD, PASTA, VAST, NIST.**

Let's take a closer look at STRIDE
1. **spoofing**: it occurs when someone masquerades as a person or system they are not.  (Correct! Since the token never expires, and the application doesn't check for concurrent logins, it is very possible for someone to login as someone else. By using that token to authenticate, I am now authenticated as the user who owns that token. )
1. **tampering**: Someone alters data (Correct! If users have unrestricted access to the logs, they can edit or delete the logs. This is tampering. Tampering is often used in conjunction with other issues. For example, someone may alter or delete logs to cover their tracks when performing a spoofing attack.)
1. **repudiation**: the ability to deny something (if you can’t be certain that all actions were done by the user, it opens the door for any user to refute an action)
1. **information disclosure** - Threat of leaking privileged or sensitive information (Correct! Decrypted backups are effectively stored in plaintext. Storing them on a server with public read access means anyone who can access that server can view those backups. )
1. **denial of service**: it aims to render a service or system unusable (Correct! Lack of rate limiting can result in Denial of Service. By not controlling the amount of requests, someone can easily overwhelm the system (on purpose or accidentally)
1. **elevation of privilege**: A user performs actions not intended for their level of permissions

## Security review and audit

Big picture to developing your intuition about security review and audit.

**Audit plays an important role in overall security strategy**. 3rd parties such as clients and regulators have a vested interest in your security. **Auditors will assert that you are doing the things you say you are doing**. **When designing security solutions it is important to always consider how this can be audited**. Audit serves to prove that you do what you claim when it comes to security operations. Auditors will assert that you are doing the the things you say you are doing. **The best method to prove is documentation**. For instance, What is the purpose of access control?, What about Exceptions?, Documentation to the rescue!

**From a compliance and audit perspective**, a security program that **can't be audited is effectively non-existent**. Auditors, clients, and other parties will not just take you at your word, **you must be able to prove that you do what you claim**. If you have a robust change management program, but you lack in documentation (policy) or cannot provide evidence through a tracking system, auditors cannot attest that you have good change management. This type of opinion is very negative for an organization. Although auditors don't necessarily have a say in what we do in terms of security, they do hold us to our word. That is, auditors can act as a forcing function to make sure we have good practices. Without robust process and tracking, the likelihood of making mistakes is a process is much higher.

Some points about control audits:

1. **controls**: the measures an organization takes to reduce risk (Policies, procedures, systems).
1. **preventive**: security measures to stop an event from occurring. They can be: Physical (Lock on the door), Technical (firewall, antivirus), Procedural (security awareness policies)
1. **detective**: security measures to detect or alert on an event or incident (**surveillance, SIEMs**)
1. **corrective**: security measures are taken to repair damage. Ex. Patching a system, quarantining a breached system.
1. **control frameworks**: define security practices, provide structure; frameworks provide a structure that can be used to manage security controls.
1. **audit**: An official examination or review by 3rd party. 
1. **control audit**: the more robust your process and systems are, the easier it is provide this evidence.
1. **information system security audit**: systematic assessment of an organization's security operations
1. **infrastructure audits**: Performed internally to assess our information systems infrastructure; less formal, performed internally; helps improve I.S. infrastructure.

## design, architecture, and code review

**A security review is a process for identifying risks in a given scenario. Identify the risks.**

1. **design**: assess a proposed design and highlight areas to consider when building out the system. Identify goal and risks in the design. Encryption requirements, logging and monitoring and data access requirements. High level risks to consider.
1. **architecture**: Assess a proposed (or in some cases already built) architecture. Encrypted data storage for credit cart, but method of encryption is satisfactory?
1. **code**: Aims to identify security issues in the source code. Review the code to ensure that engineers didn’t include any vulnerability. Secure code and identify issues, OWASP 10. Proactive strategy, before the system goes to production.

**To think about**: What are the goals and risks associated with this system or feature? What are the requirements? Are there any high level risks to consider? Are there any sensitive data?

**To think about**: Is the architecture ensure CIA principles? if there any any sensitive data, it is encrypted? Is the method of encryption satisfactory? If there are high level risks, is the architecture ensure the information security? Is the a way to ensure that any new vulnerability was included in the architecture?

**To think about**: Was the code reviewed to ensure that any new vulnerability was included? Does the code use the best practices to ensure a safe code, such as OWASP 10? Do the team code and security have a proactive strategy?

Some questions about design:
* What type of data we will be processing and storing?
    * Is it new?
    * Is it a protected type?
* Where will the system be hosted? On-premise or public cloud?
* Any new risky processes or features?
    * New encryption or authorization? 
    * New user functionality? 

Some questions about architecture:
* Tell me about how you’re encrypting __.
    * Which algorithm?
* How is data stored?
    * How is it encrypted?
    * How is it accessed?
* Dig into APIs?

Some questions about code:
* How are you sanitizing output and verifying input? 
* What third-party libraries are you using? 
* Are there any hard-coded secrets?

## Industry standards and best practices

* Independent Parties
    * CIS Critical Security Controls are a set of 20 controls designed to address the threat of common cyber attacks.
    * ISO 27001 
    * PCI DSS Payment card industry data security standard (any organization that accepts, stores, transmits, or processes credit card)
* Government Organizations
    * NIST Cybersecurity Framework assist organizations in managing and mitigating risk based on standards, guidelines and best practices.
    * Healthcare Insurance Portability and Accountability Act (HIPAA)

## Writing Reports and Recommendations

* Methodology: why your assessment and conclusions are reasonable and appropriate?
* type of assessment: audit, penetration test, security review?
* describe any tools that you used in your test
* describe how you determined the severity of the risks you identified
* mention if you used any framework
* Threat Likelihood
    * High: A threat actor is highly likely to create an event 
    * Moderate: A threat actor is likely to create an event 
    * Low: A threat actor is unlikely to create an event 
* Threat Impact
    * Critical: The event would have a catastrophically negative impact on the organization. 
    * High: The event would have a severe negative impact on the organization. 
    * Moderate: The event would have a negative impact on the organization. 
    * Low: The event would have a limited negative impact on the organization. 
    * Informational: The event would have a negligible impact on the organization. 
* Level of Risk: Likelihood x Impact
    * Critical: The event would have multiple severe or catastrophic negative effects on the organization. 
    * High: The event would have a catastrophic negative effect on the organization. 
    * Moderate: The event would have a negative effect on the organization. 
    * Low: The event would have a limited negative impact on the organization 
    * Informational: The event would have a negligible impact on the organization. 
* scope: be specific about what systems or application you included in your assessment; be clear what is included and what is excluded; explicitly state what systems, IP addresses, applications, code repos; note primary goals of the assessment (Were you attempting to find vulnerabilities? Or Was this an in-depth assessment of a new potential security investment?)
* executive summary: it should outline the key points you want to highlight; non-technical
* Synopsis: The assessment team discovered several vulnerabilities including cross-site scripting, SQL injection, and denial of service.
* Finding and Recommendations: identified threats, remediation recommendations, be detailed)