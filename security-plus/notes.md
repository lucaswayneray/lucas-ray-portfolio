# CompTIA Security+ Study Notes

## Domain 1: Threats, Attacks, and Vulnerabilities

### 1.1 Types of Threat Actors

* **Script Kiddies**: Unskilled individuals using tools made by others.
* **Hacktivists**: Politically or socially motivated attackers.
* **Organized Crime**: Sophisticated, financially motivated attackers.
* **Nation-State/APT**: Highly skilled government-sponsored groups.
* **Insiders**: Threats originating within the organization.

### 1.2 Types of Attacks

* **Phishing**: Deceptive emails to trick users into giving up information.
* **Spear Phishing**: Targeted phishing aimed at specific individuals.
* **Whaling**: Phishing targeting high-profile individuals.
* **Vishing**: Phishing via voice call.
* **Smishing**: Phishing via SMS.
* **Credential Harvesting**: Collecting usernames/passwords.
* **Watering Hole**: Compromising a site commonly visited by targets.

### 1.3 Threat Vectors

* **Email attachments, websites, social engineering, USB devices**

## Domain 2: Architecture and Design

### 2.1 Secure Network Design

* **DMZ**: Public-facing services isolated from internal network.
* **Segmentation**: Dividing the network to limit attack spread.
* **Zero Trust**: Never trust, always verify—access is continuously validated.

### 2.2 Security Concepts

* **Least Privilege**: Users get only the access they need.
* **Defense in Depth**: Layered security controls.
* **Vendor Diversity**: Avoiding reliance on a single vendor for all solutions.

## Domain 3: Implementation

### 3.1 Secure Protocols

* **HTTPS**: Encrypted web traffic.
* **SSH**: Secure remote access.
* **SFTP**: Secure file transfer.
* **TLS/SSL**: Secure communication.
* **IPSec**: Secures IP traffic using authentication/encryption.

### 3.2 Endpoint Security

* **Antivirus, EDR, Application Whitelisting**

## Domain 4: Operations and Incident Response

### 4.1 Incident Response Process

* **Preparation**
* **Identification**
* **Containment**
* **Eradication**
* **Recovery**
* **Lessons Learned**

### 4.2 Tools

* **SIEM**: Collects and analyzes logs for threats.
* **SOAR**: Automates incident response workflows.
* **Syslog**: Standard logging format.

## Domain 5: Governance, Risk, and Compliance

### 5.1 Frameworks and Guidelines

* **NIST, ISO, COBIT, GDPR, HIPAA**

### 5.2 Risk Management

* **Risk Assessment**: Identifying and evaluating risks.
* **Risk Mitigation**: Reducing impact or likelihood of risks.

---

## Security Controls Overview

### Categories of Security Controls

**Technical Controls**: Implemented by technology (e.g., firewalls, antivirus, software policies).

**Managerial Controls**: Policies and procedures defined by management to guide secure system use (e.g., onboarding policies, compliance standards).

**Operational Controls**: Processes and activities carried out by people (e.g., guards, training, awareness posters).

**Physical Controls**: Devices or measures that prevent physical access (e.g., locks, fences, badge readers).

### Types of Control Functions

**Preventive Controls**: Stop incidents before they happen.

* *Examples:* Firewall rules (Technical), onboarding policy (Managerial), guard shack (Operational), door lock (Physical)

**Deterrent Controls**: Discourage potential attackers.

* *Examples:* Splash screen with security notice (Technical), threat of demotion (Managerial), reception desk (Operational), warning signs (Physical)

**Detective Controls**: Identify and log incidents.

* *Examples:* System logs (Technical), log reviews (Managerial), patrols (Operational), motion detectors (Physical)

**Corrective Controls**: Respond to and fix issues after detection.

* *Examples:* Backup restoration (Technical), incident reporting policies (Managerial), calling authorities (Operational), fire extinguisher (Physical)

**Compensating Controls**: Temporary solutions when primary controls can't be used.

* *Examples:* Firewall rule to mitigate unpatched vulnerability (Technical), separation of duties (Managerial), multiple guards (Operational), generator (Physical)

**Directive Controls**: Direct user actions through rules or training.

* *Examples:* Encrypted folder policies (Technical), compliance policies (Managerial), security training (Operational), "Authorized Personnel Only" signs (Physical)

---

*Add notes as you progress through your Security+ study. Use subheadings, lists, and examples to make the material easier to review.*

CIA triad-fundmentls of scrty- combo of princples
Sometimes called AIC triad
Confidentiality- Integrity- Availability

Confidentiality- Prvnt disclsure of info to unauthrzed indivduals or systms

Integrity- Messges can't be modified w/out detection- make sure what is received is what was really sent

Availability- Systems up and running at all times even if implmntng some type of IT secrty

Confidentiality- certain info should only be known to certain people- prvnt unauth'd info disclosure- One way to prvide confidentiality is through encryption

Encryption- encode messges so only certain people can read it.- one person encrypts data, send it, then the recipient can decrypt to be able to see orig plaintext- anyone in the middle would not be able to read any of the data contained while encrypted

Access Controls- set limits on access- slctvly restrct access to a resrce or info. Ex: may allow marketing to look at all marketing materials, but restrict from seeing accounting material.

Two Factor Authentction- Additional confrmtion before info is disclosed- another type of confidntiality

When recvng data from third party, would like to be able to see that data being rcved is what is expected- Data is stored and trnsfrred as intnded- Any mod to data would be id'd- able to do that use methods of Integrity

Integrity-
Hashing- person sending the data will create a hash of the data and send the data and the hash at the same time- when you recv the data you will prfrim the hashng function and if your hash matches sender's hash then you know the data sent is what is also recved.

Can enhance this scrty by sending a Digital Signature, which is a mathmtical scheme to verfy the integrty of data. Takes a hash and encrpts it w/ an asymmetric encrption algorithm

Means you can check to make sure that none of the data has changed. And can confirm the person who sent the data.

Also common to include certificates to id dvcs or people and prvde addtnl factrs of integrty esp when trnsfrring data from one dvc to another- combines w/ digtal signture to verify an individual

Non-repudiation- proof of integrity and can confirm that the info rcved really came from origin. Provides proof of integrty can be asserted to be genuine. 

Availability- ensures that people have access to the data they need- 

Have systems that are designed to be always up and running- might combine this with fault tolerance- where you have multiple components, so if one fails the other component can pick up and continue to operate normally

Redundancy- build srvcs that will always be availble

Patching- stability- close secrity holes- 