# RISK Glossary

### Due Diligence
Due diligence is establishing a plan, policy, and process to protect the interests of an organization.
### Due Care
Due care is the continued application of the security structure onto the organization.

### CIA Triad
* **Confidentiality**
    * Sensitivity: quality of information (harm if disclosedThe primary goals and objectives of a security infrastructure is the CIA Triad.)
    * Discretion: act of decision where operator influences or controls disclosure to minimize damage
    * Criticality: level to which information is mission critical
    * Concealment: act of hiding (security through obscurity)
    * Secrecy: act of keeping something secret (preventing disclosure)
    * Privacy: keeping information confidential
    * Seclusion: storing something in an out-of-the-way location
    * Isolation: act of keeping something separated
* **Integrity**
    * Accuracy: being correct and precise
    * Truthfulness: reflection of reality
    * Validity: factually or logically sound
    * Accountability: responsible from actions and results
    * Completeness: having all necessary components or parts
    * Comprehensiveness: complete in scope  
* **Availability**
    * Usability: state of being easy to use
    * Accessibility: assurance that subjects can interact with resources regardless of capabilities or limitations
    * Timeliness: reasonable time frame (low latency)

### DAD Triad
The DAD Triad represent the failures of security protections from the CIA
* **Disclosure** sensitive information accessed by unauthorized entities
* **Alteration** data is maliciously or accidentally changed
* **Destruction** resource is damage or inaccessible to authorized entities

### AAA Services: Authentication Authorization Accounting
There are five elements in within the AAA services
* **Identification**: claiming to be an identity
* **Authentication**: proving that you are that claimed identity
* **Authorization**: defining the permissions
* **Auditing**: recording a log of events and activities related to the system and subjects
* **Accounting**: reviewing the logs to hold subjects accountable for their actions

### Biometry
* FRR -> False Rejection Rate -> Type 1 (System does not authenticate valid user)
* FAR -> False Acceptance Rate -> Type 2 (Authenticate someone incorrectly) 
* CER -> Cross Error Rate -> identifies the accuracy of a biometric method

### Access control
**NOTE** Following ISC risk/rule/task access control are lowercase
* Privilege creep is the tendency for users to accrue privileges over time
* **DAC** Discretionary Access Control (owner can grant or deny access to any other subject i.e NFFS)
* **NDAC** Nondiscretionary Access Control
    * **RBAC** Role-Based Access Control
    * rule-Based Access Control
    * risk-Based Access Control
    * task-based Access Control
    * **ABA** Attribute Based Access Control (SDN/SD-WAN) 
    * **MAC** Mandatory Access Controls
* **AAA Protocols** Authentication Authorization Accounting


### Testing
* SOC 1 -> accuracy of financial reporting
* SOC 2 -> confidentiality, integrity and availability (NDA)
* SOC 3 -> confidentiality, integrity and availability (Public)
* Type 1 Reports -> opinion on the description provided by management and suitability of the design
* Type 2 Reports -> opinion on the effectiveness of the controls (confirms controls are functioning properly)