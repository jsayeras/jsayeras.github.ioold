
# Security 101
The primary goals and objectives of a security infrastructure is the CIA Triad.

### CIA Triad: Confidentiality Integrity Availability
* Confidentiality
    * Sensitivity: quality of information (harm if disclosedThe primary goals and objectives of a security infrastructure is the CIA Triad.)
    * Discretion: act of decision where operator influences or controls disclosure to minimize damage
    * Criticality: level to which information is mission critical
    * Concealment: act of hiding (security through obscurity)
    * Secrecy: act of keeping something secret (preventing disclosure)
    * Privacy: keeping information confidential
    * Seclusion: storing something in an out-of-the-way location
    * Isolation: act of keeping something separated
* Integrity
    * Accuracy: being correct and precise
    * Truthfulness: reflection of reality
    * Validity: factually or logically sound
    * Accountability: responsible from actions and results
    * Completeness: having all necessary components or parts
    * Comprehensiveness: complete in scope  
* Availability
    * Usability: state of being easy to use
    * Accessibility: assurance that subjects can interact with resources regardless of capabilities or limitations
    * Timeliness: reasonable time frame (low latency)

### DAD Triad: Disclosure Alteration Destruction
The DAD Triad represent the failures of security protections from the CIA
* Disclosure: sensitive information accessed by unauthorized entities
* Alteration:  data is maliciously or accidentally changed
* Destruction: resource is damage or inaccessible to authorized entities

### AAA Services: Authentication Authorization Accounting
There are five elements in within the AAA services
* Identification: claiming to be an identity
* Authentication: proving that you are that claimed identity
* Authorization: defining the permissions
* Auditing: recording a log of events and activities related to the system and subjects
* Accounting: reviewing the logs to hold subjects accountable for their actions

### Threat modeling
Thread modeling could be focused on assets, attackers or software. Threat modeling  is the process where threats are identified, categorized and analyzed. The CISSP book covers the following techniques

#### STRIDE - Microsoft
* Spoofing: attack with the goal of gaining access through the use of a falsified identity
* Tampering: unauthorized changes or manipulation of data
* Repudiation: ability of a user to deny having performed an action
* Information disclosure: revelation or distribution of private or confidential data
* Denial of service: prevent use of a resource
* Elevation of privilege: limited user gets greater privileges

#### PASTA - Risk-centric
Process for Attack Simulation and Threat Analysis is a seven-stage methodology
* DO: Definition of Objectives 
* DTS: Definition of Technical Scope
* ADA: Application Decomposition and Analysis
* TA: Threat Analysis
* WVA: Weakness and Vulnerability Analysis
* AMS: Attack Modeling & Simulation
* RAM: Risk Analysis & Management

#### VAST - Agile
Visual, Agile, and Simple Threat it is based on a comercial tool ThreatModeler