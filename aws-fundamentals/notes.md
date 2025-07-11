# AWS Fundamentals – Study Notes

Welcome to my AWS Fundamentals note tracker. These notes cover key services, use cases, commands, and diagrams encountered during the course.

---

##  Core Services & Concepts

### EC2 (Elastic Compute Cloud)
- Virtual server instances
- Key terms: AMI, instance type, EBS volume, key pair, security group
- Common use: hosting web apps, custom environments

### S3 (Simple Storage Service)
- Object storage for files, images, backups
- Key terms: bucket, object, versioning, lifecycle policies
- Common use: website hosting, data lake storage, backups

### IAM (Identity and Access Management)
- Manages users, groups, roles, and permissions
- Policies written in JSON
- Follows least privilege principle

---

##  Infrastructure Tools

### VPC (Virtual Private Cloud)
- Customizable network environment
- Key parts: subnets, route tables, internet gateways, NAT gateways

### CloudWatch
- Monitoring service for AWS resources
- Logs, metrics, alarms

### CloudFormation
- Infrastructure as Code (IaC)
- Automate resource deployment using templates (YAML/JSON)

---

##  AWS CLI (Command Line Interface)
- `aws configure`
- `aws s3 ls`
- `aws ec2 describe-instances`
- Unified tool to manage AWS services across platforms
- Automates interactions using command-line scripts
- Useful for scaling, reporting, and recurring tasks

Example:
```bash
aws ec2 describe-instances
```

---

##  AWS SDK (Software Development Kits)
- SDKs allow developers to interact with AWS services using programming languages
- Supported languages: Python, JavaScript, Java, C++, Go, PHP, .NET, Ruby
- Example: Uploading a file to S3 using Python’s `boto3` SDK

Example:
```python
import boto3

ec2 = boto3.client('ec2')
response = ec2.describe_instances()
print(response)
```

---

##  AWS Management Console
- Web-based GUI for interacting with AWS services
- Services categorized by function (e.g., Compute, Storage, Security)
- Region selector in the top right determines where your resources are deployed
- Changing regions redirects requests to different subdomains based on location

---

##  Notes by Module

### Module 1: Introduction to Cloud & AWS
- Benefits of cloud: elasticity, cost efficiency, scalability
- AWS global infrastructure: regions, availability zones, edge locations
- Traditionally, companies managed their own compute, storage, and networking hardware in physical data centers.
- Dedicated IT departments were required to support and maintain these systems, resulting in high operational costs and limited flexibility.
- As internet usage grew, the demand for scalable infrastructure exceeded what many could maintain economically.
- Cloud computing emerged as a solution: the on-demand delivery of IT resources over the internet with pay-as-you-go pricing.
- It eliminates the need to own and manage physical infrastructure, lowering barriers to scale and innovation.
- AWS owns and maintains data centers and provides virtualized infrastructure and services over the internet.
- Example: In an on-premises setup, replicating a QA environment involves purchasing and installing hardware, cabling, powering systems, and configuring operating systems—often taking days.
- In the cloud, the same environment can be replicated in minutes or seconds using logical provisioning.
- Cloud computing saves time, removes undifferentiated heavy lifting, and lets businesses focus on what's strategically unique (like their application code), while AWS manages infrastructure like VMs and backup storage.
- AWS provides cloud computing services that help architect scalable, highly available, and cost-effective infrastructures.

### Six Benefits of Cloud Computing
1. **Pay-as-you-go**: Only pay when using resources, and only for what you use.
2. **Massive economies of scale**: Aggregated usage enables AWS to offer lower pricing.
3. **Stop guessing capacity**: Scale infrastructure up or down as needed without overprovisioning.
4. **Increase speed and agility**: Reduce setup time from weeks to minutes, enabling faster innovation.
5. **Stop spending on running data centers**: Focus on differentiation, not infrastructure management.
6. **Go global in minutes**: Deploy applications to multiple regions easily to serve global users with low latency.

### Module 2: Compute and Storage
- EC2 basics and pricing models
- S3 storage classes (Standard, Infrequent Access, Glacier)

### Module 3: Networking and Monitoring
- Intro to VPC setup
- Using CloudWatch to track metrics

### Module 4: AWS Global Infrastructure
- AWS infrastructure consists of **Regions** and **Availability Zones (AZs)**.
- **Regions** are geographic locations around the world where AWS hosts data centers (e.g., `us-east-1` = Northern Virginia, `ap-northeast-1` = Tokyo).
- Each Region is isolated, meaning data is not replicated across Regions without explicit authorization.
- Four main factors for choosing a Region:
  1. **Latency** – Choose a Region close to your user base to minimize response times.
  2. **Price** – Costs vary based on geography, local economies, internet connectivity, and operational factors.
  3. **Service Availability** – Not all services are available in all Regions; check AWS documentation.
  4. **Data Compliance** – Some businesses must store data in specific geographies to meet legal/regulatory requirements.

#### Availability Zones (AZs)
- Inside every Region are multiple AZs.
- Each AZ consists of one or more data centers with redundant power, networking, and connectivity.
- AZs are isolated but connected via low-latency, high-throughput links.
- Example: `us-east-1a` is an AZ in the Northern Virginia Region (`us-east-1`).

#### Scope of AWS Services
- Services may operate at the AZ, Region, or Global level.
- Region-scoped services only require you to select a Region; AWS handles redundancy within it.
- AZ-scoped services may require manual configuration for high availability and durability.

#### Resiliency Best Practices
- Use managed, Region-scoped services when possible—they have built-in availability and failover.
- If using AZ-scoped services, deploy across **at least two AZs** to ensure failover capability in case one AZ goes down.

### Module 5: Security and the Shared Responsibility Model
- Security and compliance in AWS is a shared responsibility between AWS and the customer.
- **AWS is responsible for security _of_ the cloud** (infrastructure, data center hardware, host OS, virtualization, network stack).
- **Customers are responsible for security _in_ the cloud** (configuring services, managing applications, encrypting data, access control).

#### AWS Responsibility by Service Category
| Category                | Examples                           | AWS Responsibility                                                                 |
|-------------------------|------------------------------------|-------------------------------------------------------------------------------------|
| Infrastructure Services | Amazon EC2                         | AWS manages infrastructure and foundation services                                 |
| Container Services      | Amazon RDS                         | AWS manages infra, OS, and application platform                                    |
| Abstracted Services     | Amazon S3                          | AWS manages infra, OS, platform, and server-side encryption and data protection    |

Note: "Container Services" here refer to abstracted app environments like RDS, not Docker/Kubernetes-style containers.

#### Customer Responsibility
- Customers must configure each service properly and secure their data.
- Responsibilities vary depending on how abstracted the service is.

| Category                | Customer Responsibility                                                                      |
|-------------------------|---------------------------------------------------------------------------------------------|
| Infrastructure Services | Configure OS and app platform, manage encryption and access control                         |
| Container Services      | Encrypt and protect customer data, configure firewalls and backups                          |
| Abstracted Services     | Manage customer data, implement client-side encryption, control access                      |

#### Best Practices
- Choose regions in compliance with data sovereignty laws
- Implement encryption and backup solutions
- Use IAM policies and roles to control access to data and services
- Regularly review shared responsibility model as it applies to each AWS service

---

##  Key Terms to Remember
- **Elasticity**: Automatically adjusts capacity
- **High availability**: System remains accessible under failure
- **Scalability**: Handles increasing demand
- **Serverless**: Code execution without managing infrastructure (e.g., Lambda)
- **Undifferentiated heavy lifting**: Tasks like racking, stacking, powering servers—not unique to the business but necessary
- **Availability Zone (AZ)**: One or more discrete data centers in a Region
- **Region**: A physical location with a cluster of AZs
- **Management Console**: Web UI for managing AWS
- **CLI**: Command line interface for programmatic access
- **SDK**: Developer libraries to interact with AWS in various languages
- **Shared Responsibility Model**: AWS secures the infrastructure; customers secure their use of services

---

### Module 6: Identity & Access Management – Root User and MFA

#### 6.1 Authentication vs. Authorization
- **Authentication** verifies *who* you are (e.g., username and password, token, or biometric data).
- **Authorization** determines *what* you can do once authenticated (e.g., read, edit, delete, or create AWS resources).

#### 6.2 AWS Root User
- When you create an AWS account you start with one sign‑in identity with full access: the **root user**.
- Root credentials include:
  - **Email & password** – used for AWS Management Console sign‑in.
  - **Access key ID & secret access key** – enables programmatic access via AWS CLI or SDKs.
- Because the root user has unlimited power (including billing), follow strict best practices:
  1. **Create a strong password** and never share it.
  2. **Delete or disable root access keys** unless absolutely needed.
  3. **Use the root user only for a short list of account‑level tasks**: [AWS tasks that require root credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds.html#aws_tasks-that-require-root)

#### 6.3 Multi‑Factor Authentication (MFA)
- **Single‑factor auth** relies on just one factor (e.g., password) and is vulnerable to guessing or brute‑force attacks.
- **Multi‑factor auth (MFA)** requires at least two of:
  1. **Something you know** – password or PIN
  2. **Something you have** – one‑time code from a hardware token or mobile app
  3. **Something you are** – biometric, such as fingerprint or facial scan
- Enabling MFA on the root user dramatically reduces risk even if the password is compromised.

#### 6.4 Supported MFA Device Types
| Device Type | Description | Examples |
|-------------|-------------|----------|
| Virtual MFA | A software app that provides a one-time passcode. May be less secure than hardware. | Authy, Duo Mobile, LastPass Authenticator, Google Authenticator |
| Hardware    | Physical key fob or display card that generates numeric codes | Key fob, display card |
| U2F Device  | USB hardware security key | YubiKey |

#### 6.5 Enabling MFA
- [Enable Virtual MFA](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html)
- [Enable Hardware MFA](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_physical.html)
- [Enable U2F Security Key](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_fido.html)
- [AWS MFA Device Table](https://aws.amazon.com/iam/features/mfa/)

### Module 7: Introduction to AWS Identity and Access Management (IAM)

#### 7.1 What is IAM?
IAM is a global web service that lets you **manage who (users, groups, roles) and what (applications, services)** can access your AWS account and resources.
- **Authentication** – verifies identity.
- **Authorization** – defines the allowed actions on specific resources.

... (existing content remains unchanged here) ...

#### 7.5 Summary
- Use **least privilege**: grant only the permissions required.
- Prefer **groups** over individual user policies.
- Protect the **root user** with strong credentials and **MFA**.
- Favor roles and temporary credentials over long‑term access keys.

---

#### 7.6 Granular Policy Example – Self‑Manage Credentials
The following JSON policy allows an IAM user to **change their own password** and **view their own user details**, but nothing else. Resource access is limited using the variable substitution `${aws:username}` so each user touches only their own identity.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iam:ChangePassword",
        "iam:GetUser"
      ],
      "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
    }
  ]
}
```

> **Key Point:** By scoping the `Resource` to `user/${aws:username}`, you avoid creating separate policies for every individual.

---

#### 7.7 IAM Policy Statement Elements
| Element  | Description                                                             | Required | Example                                |
|----------|-------------------------------------------------------------------------|----------|----------------------------------------|
| Effect   | Determines whether the statement results in an **Allow** or explicit **Deny** | Yes      | `"Effect": "Deny"`                   |
| Action   | Lists the specific API actions that are allowed or denied               | Yes      | `"Action": "iam:CreateUser"`          |
| Resource | Specifies the ARN(s) the statement applies to                           | Yes      | `"Resource": "arn:aws:iam::111122223333:user/Bob"` |

All three elements are mandatory in every IAM policy statement. (Conditions are optional but common.)

---

#### 7.8 Further Reading
- [AWS IAM Access Management Guide](https://docs.amazonaws.cn/en_us/IAM/latest/UserGuide/access.html)
- [AWS IAM Identities (Users, Groups, Roles)](https://docs.amazonaws.cn/en_us/IAM/latest/UserGuide/id.html)
- [IAM Introduction](https://docs.amazonaws.cn/en_us/IAM/latest/UserGuide/introduction.html)

### Module 8: Role‑Based Access in AWS

#### 8.1 Summary of IAM Best Practices
1. **Protect the Root User**  
   - Do **not** share root credentials.  
   - Delete or deactivate root access keys.  
   - Enable Multi‑Factor Authentication (MFA) on the root account.
2. **Principle of Least Privilege**  
   - Grant only the permissions required to complete a task.  
   - Start with minimal policies and add permissions incrementally.
3. **Use IAM Appropriately**  
   - IAM secures access *within* AWS accounts; it is **not** designed to provide sign‑up/sign‑in for your public applications or to replace OS and network security controls.
4. **Prefer IAM Roles over Long‑Term Users**  
   - Roles supply **temporary credentials** (15 min – 36 hr) that auto‑expire.  
   - Users rely on long‑term passwords or access keys that require manual rotation.
5. **Consider an Identity Provider (IdP)**  
   - Centralize workforce identities with AWS IAM Identity Center or a third‑party IdP.  
   - Federated users assume roles in AWS instead of having separate IAM users in every account.

#### 8.2 IAM Roles
- Roles are **identities with no permanent credentials**.  
- When assumed, AWS issues temporary security credentials for a defined session.  
- Ideal for:
  - **Cross‑account access**  
  - **AWS service‑to‑service access**  
  - **Federated workforce or applications**

Credential Lifetime Comparison
| Identity Type | Credential Type | Typical Lifetime |
|---------------|-----------------|------------------|
| IAM User      | Password / Access Keys | Until rotated / password‑policy expiry |
| IAM Role      | Temporary Credentials  | 15 minutes – 36 hours (defined at role assumption) |

#### 8.3 Identity Federation & AWS IAM Identity Center
- **Identity Provider (IdP)** – your single source of truth for workforce accounts.  
- AWS IAM Identity Center (successor to AWS SSO) lets employees sign in **once** and access all assigned AWS accounts & apps via a user portal.
- Advantages over standalone IAM:
  1. Sync existing users/groups from an external IdP (Azure AD, Okta, etc.).
  2. Centralized user and permission management separate from cloud resources.
  3. Avoids duplicating user objects in every AWS account.

Example Workflow
1. Employee *Martha* exists in the corporate IdP.  
2. Martha is mapped to groups in IAM Identity Center (e.g., *Developers*, *Admins*).  
3. Martha signs in once and selects the AWS account/role she needs.  
4. If Martha changes jobs or leaves, update or disable her account **once** in the IdP.

---

#### 8.4 Further Reading
- [AWS IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)  
- [Managing Users with AWS IAM Identity Center](https://aws.amazon.com/blogs/security/how-to-create-and-manage-users-within-aws-sso/)

Reading 1:8- Role based access in AWS

Lock Down the AWS Root User- all powrful and all-knwing ID w/in your AWS accnt. If malicious user gains ctrl of root-user creds, they'd be able to accss evry resrce w/in your accnt, inclding prsnal and bllng info
To lock down root user: 
1) Don't share the creds asscted w/ root user
2)Consider deleting the root user accss keys
3) Enable MFA on root accnt.

FOLLOW PRINCIPLE OF LEAST PRIVILEGE

Least Privilege is a stndrd scrty princple that advses you to grant only the necessary permissions
to do a particular job and nothing more. To implement least privilege for access ctrl, start w/ minmum set of prmissions in IAM policy and then grant addtional permssions as necessry for user, group, or role


USE IAM APPRPRTLY

IAM is used to secre access to your AWS accnt and rsrcs- simply prvdes a way to create and mnge, users, groups and roles to access, rsrcs w/in a single AWS accnt, IAM is NOT used for website authntction and authrztion, such as prvding users of a wbsite
w/ sign in and sign up fnctnlty. IAM also does NOT supprt scrty ctrls for prtcting OSs and netwrks. 

USE IAM ROLES WHEN POSSIBLE

Maintaining roles is easier than maintaining users. When you asume a role, IAM dynmcllty prvdes temprary creds that expire after a defned period of time, bt 15 minutes and 36 hours.
Users, however, have long-term creds in form of user name and password combos or a set of access keys. User access keys only expire when you or the admin of your accnt rottes these keys. User login creds expire if you have applied a pword policy to your accnt that forces users to rotate passwords.

CONSIDER USING AN ID PROVIDER

If you decide to make your cat photo app into a busness and begin to have more than a handful of people working on it, consider managing emplyee ID info through and ID provider (IdP). 
Using an IdP, AWS, IAM ID center, or third-party ID prvider, prvdes you a single src of truth for all IDs in your org. No longer have to create separate IAM users in AWS.
Can instead use IAM roles to prvide permissions to IDs that are fedrated from your IdP. For ex: you have an emplyee, Martha, that has access to multple AWS accnts. Instead of creating and managing multple IAM users named Martha in each AWS accnt, can manage Martha in your company's IdP. If Martha moves w/in the compny or leaves the compny, Martha can be updated in the IdP, rather than in every AWS accnt you have. 

CONSIDER AWS IAM ID CENTER

If you have an org that spans many emplyees and multple AWS accnt, you may want your emplyees to sign in w/ a single credntial. AWS IAM ID Center is an IdP that lets your users sign into a user portal w/ single set of creds. Then prvdes them access to all their assgned accnts and apps in one centrl location. AWS IAM ID Center is simlar to IAM in that it offers a drctry where you can create users, orgnize them in groups and set permssions across those groups, and grant access to AWS resrces.
But AWS IAM ID Center has some advntges over IAM. For ex:, if using a third-party IdP you can sync your users and groups to AWS IAM ID Center.This removes the burden of having to re-create users that already exist elsewhree, and enables you to manage thos users from your IdP.
More imprtntly, AWS IAM ID Center separtes the duties bt your IdP and AWS, ensring that your cloud access mgmt is not inside or depndent on your IdP.


Links:
https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html

