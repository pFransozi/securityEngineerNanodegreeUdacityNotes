# Security Engineering Fundamentals

## Security Principles

There are four principles:

* CIA Triad
* Authentication, Authorization, Non-Repudiation
* Principles of secure design
* Security strategies

A security mindset: how can I break this system?

As a professional, you will evaluate risk based on the potential impact they may have on one of these three principles. That evaluation will drive your strategy for designing, and implementing a remediation plan.

### CIA Triad

* **confidentiality**: it is **keeping data secret or private**, in theory. In practice, it is **controlling access to prevent unauthorized disclosure**. Employee data, for instance, needs to be kept private and it should only be accessible by certain members of HR. Therefore, any access outside constitutes a breach of confidentiality.

* **integrity**: it is **ensuring the legitimacy of data so it can be trusted**, in theory. In practice, it means **no unauthorized modification or deletion**. Information must remain integral, without unauthorized modifications.

* **availability**: ensuring networks, systems, and applications are up and running. Denial of service (DoS) is a common vulnerability that affects availability of a service. Even though availability seems less obvious than confidentiality and integrity, it is equal important. Consider the healthcare industry or airline systems, for instance.

**To think**: not to fall in the trap assuming breaches to these principles **only occur by a malicious third party**. **A breach can occur by a malicious third party or by mistake of an authorized party**. 

**To think**: although each of the TRIAD is important for information security, **depending on the company the priority may vary**, and for that the impact also may vary. 

**To think**: **confidentiality**: keeping data secret or private; **integrity**: ensuring the data can be trusted; **availability**: ensuring networks, systems, and applications are up and running.

**To think**: bad performance does or does not violate availability principle? If the system is up and running, but unusable is it still considered available? What is our threshold for unusable? Is it some percentage of loss of expected performance? **It is important to consider what constitutes a security issue**. **Perhaps degrade in performance can be indicative of an attack, or perhaps it's merely a system issue**.

**To think**: working for a large eCommerce site, it happened an error that marked down the newly released video game system by 50%. Instead of $60, the game is selling for $30! As a result, the number of visits to your website increased substantially, and this caused an outage. Which security principles would this violate? **Integrity and Availability**.

### Authentication and Authorization

