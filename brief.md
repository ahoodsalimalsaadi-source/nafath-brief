Version: NAFATH-V4
Track: Software

## Overview
Securing a national service provider's supply chain requires defending interconnected layers against sophisticated intrusions. Software foundations must maintain isolation across operational environments to prevent credential leakage. AI pipelines demand resilience against data poisoning and evasion attacks that manipulate models. Mobile endpoints rely on rigorous verification standards to safeguard client-side integrity. At the infrastructure level, BGP route hijacking threatens data transit, mitigated partially by RPKI cryptographic validation. Meanwhile, pervasive libraries like Log4j introduce severe systemic risks through arbitrary code execution, requiring precise patching. Finally, comprehensive Software Bills of Materials ensure complete software transparency across every component. Protecting this ecosystem ultimately depends on robust configuration and secret management.

## Software
According to the Twelve-Factor App methodology, configuration—including database credentials, API keys, and external service endpoints—should be stored strictly in environment variables rather than hardcoded in the codebase. Environment variables can be easily changed between deploys without altering application code. Keeping secrets out of source control prevents accidental exposure in public or compromised repositories, ensuring strong separation between code and configuration across staging and production environments.

Resource: The Twelve-Factor App - Config - https://12factor.net/config

## AI
Adversarial machine learning attacks primarily include poisoning, evasion, privacy, and abuse attacks. Data poisoning targets the training phase by injecting malicious data to corrupt the model's learned parameters or behavior. In contrast, evasion attacks occur during inference, where perturbed inputs are crafted to deceive a fully trained model into misclassification. While poisoning undermines model integrity at its root, evasion exploits decision boundaries of deployed models without altering training weights.

Resource: NIST AI 100-1: Artificial Intelligence Risk Management Framework - https://www.nist.gov/itl/ai-risk-management-framework

## Mobile
The OWASP Mobile Application Security Verification Standard (MASVS) is a comprehensive security standard for mobile app architecture, design, and development. It defines baseline security requirements across categories such as storage, cryptography, authentication, and network communication. Developers and security auditors use MASVS alongside the testing guide (MASTG) to verify that mobile applications resist reverse engineering, protect sensitive data, and securely interact with backend services.

Resource: OWASP MASVS - https://masvs.owasp.org/

## Networking
BGP route hijacking occurs when an autonomous system falsely announces ownership of IP address prefixes it does not control, redirecting or intercepting internet traffic. Resource Public Key Infrastructure (RPKI) prevents this by using cryptographic Route Origin Authorizations (ROAs) to cryptographically verify which AS is authorized to originate specific prefixes. However, RPKI does not protect against path spoofing or AS-path alteration beyond the origin AS.

Resource: RFC 6480 - An Infrastructure to Support Secure Internet Routing - https://www.rfc-editor.org/rfc/rfc6480

## Cybersecurity
The Log4Shell vulnerability (CVE-2021-44228) was a critical remote code execution flaw in Apache Log4j 2 caused by improper handling of Java Naming and Directory Interface (JNDI) lookup features in log messages. It was rated severe (CVSS 10.0) because Log4j is ubiquitous in enterprise Java software, and attackers could trigger exploits simply by logging unvalidated user-supplied strings, allowing unauthenticated remote code execution. It was fixed by disabling JNDI lookups by default.

Resource: Apache Log4j Security Vulnerabilities - https://logging.apache.org/log4j/2.x/security.html

## Data
A Software Bill of Materials (SBOM) is a formal, structured inventory of software components and dependencies, detailing supply chain relationships of open source and proprietary code. To provide adequate transparency, minimum data fields should include supplier name, component name, version string, dependency relationship, unique identifiers, and the timestamp of the SBOM generation. These fields enable organizations to quickly identify and remediate vulnerable components across their operational environment.

Resource: CISA Software Bill of Materials - https://www.cisa.gov/sbom

## Misconception in My Track
A common misconception in software configuration management is that storing secrets in encrypted configuration files within the source code repository provides adequate security. While encryption protects data at rest against casual inspection, decryption keys often end up managed improperly or committed alongside ciphertext. The Twelve-Factor App methodology explicitly refutes this, stating that configuration should be stored in environment variables, which are completely decoupled from code storage. The Config section notes that apps sometimes store config as constants in code, violating the core tenet that code should not vary across deploys.


## Open Question
How can organizations effectively automate SBOM generation and vulnerability ingestion across heterogeneous CI/CD pipelines without introducing severe build bottlenecks?
