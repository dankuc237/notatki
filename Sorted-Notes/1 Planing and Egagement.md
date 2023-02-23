TABLE OF CONTENT
<!-- TOC -->

- [Recipe](#recipe)
- [Planning and Scoping the Pentest](#planning-and-scoping-the-pentest)
- [Types of penetration testing](#types-of-penetration-testing)
- [Basic Agreement Concepts](#basic-agreement-concepts)
- [Most Common Compliance Standards - normy bezpieczeństwa](#most-common-compliance-standards---normy-bezpieczeństwa)
- [Main Pentest Methodologies and Frameworks - The overall pentest process](#main-pentest-methodologies-and-frameworks---the-overall-pentest-process)

<!-- /TOC -->
---
Regulatory and compliance considerations for penetration tests
Legal concepts including limitations on testing, contracts, and documentation
Penetration testing types, scoping, and testing requirements
Professionalism, integrity, the ethical hacking mindset, and risks and responsibilities for penetration testers

# Recipe
1. Initial information gathering
Understand the magnitude of the pentest
	- How many IPs will be tested?
	- How many assets?
	- How many URLs? How many pages per URL?
Understand the detection capabilities
	- Are there any WAF or next gen firewall?
3. Create, review and sign agreements
4. Refine assets in scope
5. Define attacks and methodologies
6. Define rules of engagement

# Planning and Scoping the Pentest
How to define assets/attacks in scope, out of scope: Types of assets and types of attacks
Considerations when pentesting a cloud or third party environment: Prefer single IPs instead of IP ranges and review pentest policy for provider
Main methodologies and frameworks: OWASP Top 10, Mitre ATT&CK, NIST and PTES
Assessing pentest impact: Heavy scans, password brute forcing, exploits, denial of service attacks
Rules of Engagement (ROE): Assets/attacks in scope, pentest schedule, testing times, network limitations, data integrity and communications.

# Types of penetration testing
Internal, external, web application, IoT, mobile, etc.
Black-box vs. grey-box vs white-box

# Basic Agreement Concepts
**Non-Disclosure Agreements (NDAs)**: Ensure that the information discussed during the pentest will not be released to anyone outside of the project, hefty fines for breaking confidentiality rules
Also known as: Confidentiality Agreement (CA), Confidential Disclosure Agreement (CDA), Proprietary Information Agreement (PIA)
**Master Service Agreements (MSA)** Includes terms such as: how invoices will be sent, how payments will be made, ownership of intellectual properties, etc.
**Statement of Work (SOW)** Documents the details of a specific project, one SOW per pentest engagement, define things such as: assets in scope, project deliverables, price for the services, etc. You can have multiple SOWs for a client while having just one MSA
**Permission to Attack** Also known as “Get-Out-of-Jail-Free” cards, a document authorizing you to perform the attacks, Describe the attacks and dates of the tests, signed by a high-level executive in the client, includes their contact information, it is what differentiates you from a criminal.
**Rules of Engagement** The rules of engagement (RoE) document puts into writing the guidelines and constraints regarding the execution of a pentest—most importantly, what is and is not authorized for testing; for example, whether or not brute force is an allowed tactic, whether bruteforce counts are limited by password lockout policies, automated fuzzing versus manual exploitation, etc.

# Most Common Compliance Standards - normy bezpieczeństwa
- PCI-DSS
- GDPR
- HIPAA
- SOX
- NERC-CIP
- ISO27001

# Main Pentest Methodologies and Frameworks - The overall pentest process
- [PTES](http://www.pentest-standard.org/index.php/PTES_Technical_Guidelines)
- [OWASP](https://owasp.org/), mainly focused on Web Applications,
- MITRE ATT&CK, framework for adversary emulation
- NIST, non-regulatory agency of the US
- OSSTMM, in-depth description of each step of a penetration testing
- ISSAF, covers some of the most common attacks and tools. With a lot of practical examples