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

https://aws.amazon.com/blogs/security/how-to-create-and-manage-users-within-aws-sso/
Hosting Applications & Compute Fundamentals

The first building block you need to host an application is a server. Servers typically handle HTTP requests and send responses to clients, following the client-server model.

Client: Person or computer sending a request

Server: Computer or group of computers processing requests and serving content

Common HTTP server software:

Windows: Internet Information Services (IIS)

Linux: Apache HTTP Server, Nginx, Apache Tomcat

To run an HTTP server on AWS:

Use AWS compute services via the AWS Management Console

AWS Compute Options:

Virtual Machines (e.g., Amazon EC2)

Container Services (e.g., ECS, EKS)

Serverless (e.g., AWS Lambda)

Virtual Machines (EC2) are often the easiest entry point for those with traditional infrastructure knowledge.

A hypervisor runs on a host machine to manage virtual machines

In AWS, these VMs are called Amazon EC2 instances

AWS manages the hypervisor, host machine, and guest operating system

Amazon EC2 and AMIs

Amazon EC2 is a web service that provides secure, resizable compute capacity in the cloud. You can provision virtual servers (EC2 instances) for any kind of workload—not just web servers.

EC2 Instance Creation Options:

AWS Management Console

AWS CLI

AWS SDKs

Automation/Orchestration tools (e.g., CloudFormation, Terraform)

To launch an EC2 instance, configure:

Hardware specs (CPU, memory, networking, storage)

Logical settings (network location, firewalls, OS, authentication)

The first setting during launch is selecting an Amazon Machine Image (AMI).

What is an AMI?

An Amazon Machine Image (AMI) defines the OS and software configuration for your EC2 instance.

In traditional IT, you'd manually install an OS—AMIs eliminate this step

AMIs include OS, architecture (32/64-bit, ARM), storage mappings, and software

AMI vs EC2 Instance:

AMI = recipe (like a class definition in code)

EC2 = actual running server (like an object created from a class)

How EC2 uses AMIs:

AWS allocates a VM using the hypervisor

The selected AMI is copied to the root volume

The system boots, and you're ready to install packages or serve content

Reusability and Custom AMIs

You can create your own AMI from a configured EC2 instance

This enables easy replication of that instance without repeating configuration steps

AMI Categories:

QuickStart AMIs – pre-made by AWS

AWS Marketplace AMIs – third-party options

MyAMIs – custom AMIs you’ve created

Community AMIs – from the AWS user community

EC2 Image Builder – for automated custom image creation

Each AMI has a unique AMI ID that is region-specific.

Stop vs Stop-Hibernate

When you stop your instance:

It enters the stopping → stopped state.

Billing stops for usage and data transfer (but EBS storage charges remain).

Data in RAM is lost.

You can change some instance attributes like instance type.

When you stop-hibernate:

AWS saves the contents of RAM to your EBS root volume.

Instance resumes from where it left off.

Ideal for use cases that rely heavily on RAM caching, such as custom backend cache layers.

EC2 Pricing Breakdown
Instance Pricing ≠ Total Pricing

EC2 pricing is based on:

Compute (instance type and specs)

Storage (EBS volumes)

Networking (data transfer)

Instances are billed per second, but pricing is shown per hour for clarity.

E.g., 5m 38s = 338 seconds of billing

Marketplace AMIs may require a 1-hour minimum

EC2 Pricing Options
1. On-Demand Instances (Pay-As-You-Go)

No long-term commitment

Billed while running

Fixed price per second

Good for unpredictable workloads or short-term testing

Drawback: For always-on workloads (e.g., web servers), On-Demand is more expensive than Reserved.

2. Reserved Instances (RIs)

1-year or 3-year commitment

Discounted hourly rate

Optional capacity reservation

Payment options: All Upfront > Partial Upfront > No Upfront (descending discounts)

Even if stopped, RIs still incur charges because of the reserved capacity.

3. Spot Instances

Take advantage of unused capacity

Up to 90% discount vs On-Demand

Set max price you're willing to pay

AWS may interrupt instance (with 2-minute warning)

Best for:

Fault-tolerant, interruptible workloads

Examples: CI/CD, big data, HPC, rendering, dev/test

Resources:

https://aws.amazon.com/ec2/

https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html

https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html

https://aws.amazon.com/ec2/pricing/

https://aws.amazon.com/ec2/pricing/on-demand/

https://aws.amazon.com/ec2/spot/pricing/

https://aws.amazon.com/ec2/pricing/reserved-instances/pricing/

REMOVE THE UNDIFFERENTIATED HEAVY LIFTING

If you run your code on Amazon EC2, AWS is responsible for the physical hardware and you are responsible for the logical controls, such as guest operating system, security and patching, networking, security, and scaling.

If you run your code in containers on Amazon ECS and Amazon EKS, AWS is responsible for more of the container management, such as deploying containers across EC2 instances and managing the container cluster. However, when running ECS and EKS on EC2, you are still responsible for maintaining the underlying EC2 instances.

If you want to deploy your workloads and applications without having to manage any EC2 instances, you can do that on AWS with serverless compute.

GO SERVERLESS

Every definition of serverless mentions four aspects.

No servers to provision or manage.

Scales with usage.

You never pay for idle resources.

Availability and fault tolerance are built-in.

With serverless, spend time on the things that differentiate your application, rather than spending time on ensuring availability, scaling, and managing servers.AWS has several serverless compute options, including AWS Fargate and AWS Lambda.

EXPLORE SERVERLESS CONTAINERS WITH AWS FARGATE

Amazon ECS and Amazon EKS enable you to run your containers in two modes.

Amazon EC2 mode

AWS Fargate mode



AWS Fargate is a purpose-built serverless compute engine for containers. Fargate scales and manages the infrastructure, allowing developers to work on what they do best: application development.

It achieves this by allocating the right amount of compute, eliminating the need to choose and handle EC2 Instances and cluster capacity and scaling. Fargate supports both Amazon ECS and Amazon EKS architecture and provides workload isolation and improved security by design.

AWS Fargate abstracts the EC2 instance so you’re not required to manage it. However, with AWS Fargate, you can use all the same ECS primitives, APIs, and AWS integrations. It natively integrates with AWS Identity and Access Management (IAM) and Amazon Virtual Private Cloud (VPC). Having native integration with Amazon VPC allows you to launch Fargate containers inside your network and control connectivity to your applications.

RUN YOUR CODE ON AWS LAMBDA

If you want to deploy your workloads and applications without having to manage any EC2 instances or containers, you can use AWS Lambda.AWS Lambda lets you run code without provisioning or managing servers or containers. You can run code for virtually any type of application or backend service, including data processing, real-time stream processing, machine learning, WebSockets, IoT backends, mobile backends, and web apps, like your corporate directory app!

AWS Lambda requires zero administration from the user. You upload your source code and Lambda takes care of everything required to run and scale your code with high availability. There are no servers to manage, bringing you continuous scaling with subsecond metering and consistent performance.

HOW LAMBDA WORKS

There are three primary components of a Lambda function: the trigger, code, and configuration.The code is source code, that describes what the Lambda function should run. This code can be authored in three ways.


You create the code from scratch.

You use a blueprint that AWS provides.

You use same code from the AWS Serverless Application Repository, a resource that contains sample applications, such as “hello world” code, Amazon Alexa Skill sample code, image resizing code, video encoding, and more.

When you create your Lambda function, you specify the runtime you want your code to run in. There are built-in runtimes such as Python, Node.js, Ruby, Go, Java, .NET Core, or you can implement your Lambda functions to run on a custom runtime.The configuration of a Lambda function consists of information that describes how the function should run. In the configuration, you specify network placement, environment variables, memory, invocation type, permission sets, and other configurations. To dive deeper into these configurations, check out the resources section of this unit.Triggers describe when the Lambda function should run. 

A trigger integrates your Lambda function with other AWS services, enabling you to run your Lambda function in response to certain API calls that occur in your AWS account. This makes you quicker to respond to events in your console without having to perform manual actions.All you need is the what, how, and when of a Lambda function to have functional compute capacity that runs only when you need it to.Amazon’s CTO, Werner Vogels, says, “No server is easier to manage than no server.” This quote summarizes the convenience you can have when running serverless solutions, like AWS Fargate and AWS Lambda. 

In the next unit, you apply all the information you’ve learned about Amazon EC2, Amazon ECS and Amazon EKS, and AWS Fargate and learn the use cases for each service.

AWS Lambda function handler

The AWS Lambda function handler is the method in your function code that processes events. When your function is invoked, Lambda runs the handler method. When the handler exits or returns a response, it becomes available to handle another event.You can use the following general syntax when creating a function handler in Python:

def handler_name(event, context):  ... return some_value

NAMING

The Lambda function handler name specified at the time you create a Lambda function is derived from the following:the name of the file in which the Lambda handler function is located the name of the Python handler functionA function handler can be any name; however, the default on the Lambda console is lambda_function.lambda_handler. This name reflects the function name as lambda_handler, and the file where the handler code is stored in lambda_function.py. If you choose a different name for your function handler on the Lambda console, you must update the name on the Runtime settings pane.

BILLING GRANULARITY

AWS Lambda lets you run code without provisioning or managing servers, and you pay only for what you use. You are charged for the number of times your code is triggered (requests) and for the time your code executes, rounded up to the nearest 1ms (duration). AWS rounds up duration to the nearest millisecond with no minimum execution time. With this pricing, it can be very cost effective to run functions whose execution time is very low, such as functions with durations under 100ms or low latency APIs. For more information, see 
AWS News Blog
. 

SOURCE CODE

This video used a small amount of sample code illustrating a pattern for lazily generating assets using AWS Lambda and Amazon S3. If you’re looking to deploy a service to resize images to production, consider using the new release  
 Serverless Image Handler 
which is a robust solution to handle image manipulation and can be deployed via an AWS CloudFormation template.

You can find a tutorial on creating the AWS Lambda function as well as the code used in the AWS Lambda demo here: see 
AWS News Blog
. 

Resources:

External Site:
 AWS: Serverless

Coursera Course:
 Building Modern Python Applications on AWS

External Site:
 AWS: AWS Serverless resources

External Site:
 AWS: Building Applications with Serverless Architectures

External Site:
 AWS: Best practices for organizing larger serverless applications

External Site:
 AWS: Managing AWS Lambda functions

External Site:
 AWS: 10 Things Serverless Architects Should Know

External Site:
 AWS: AWS Alien Attack! A Serverless Adventure

 What is Networking?- It's how you connect computers around the world and allow them to communicate w/ one another. AWS global infrstrctre
 AWS has created a network of rsrcs using data cntrs, Avaliability Zones, and Regions

 Know the ntwrkng basics- Sending a letter- Three pieces of info you need. 
       *Payload or letter inside the envelpe
       *The address of sender in the From section
       *The address of recipient in the To section

Each address must contain info such as:
       * Name of sender and recipnt
       * Street
       * City
       * State or provice
       * Zip, area, or postal code
       * Country

Need all parts of an addrss to ensre that your letter gets to destntion. W/out the crrct addrss, postl wrkrs are not able to properly deliver the message. In the digital world, computers handle the delivery of messages in simlr way. Called routing. 

What are IP Addresses?- To properly route messges to location, need an adress, each comp has IP addrss. IP uses 0's and 1's

IPV4 Notation- usually IP addrss is convrted into decimal format and noted as an IPV4 address. Grouped into 8 bits (octets). converted into decml format seprted by a period (192.168.1.30)

Good for commncting w/ one comp, but we are using a network- use CIDR notation

192.168.1.30 is a single IP addrss- if want to express IP addrsses bt the range of 192.168.1.0 and 192.168.1.255, one way is to use CIDR (Classless Inter-Domain Routing) notation. CIDR is comprssed way of spcfying range of IP addresses. Spcfying a range detrmnes how many IP addrsses are availble to you. Looks like- 192.168.1.0/24

Begins w/ strting IP addrss and is seprted by forwrd slsh (the "/" charctr) follwed by a numbr. The numbr at end spcfs how many of the bits of the IP addrss are fixed. In above ex the first 24 bits are fixed, rest are flexible.

32 total bits subtrctd by 24 fixed bits leaves 8 flexble bits- Each of these flxble bits can be either 1 or 0 bc theyre binary. Means you have two choices for each of 8 bits, prvdng 256 IP addrsses in that IP range. 

The higher the number after the /, the smaller the num of IP addrsses in your network. For ex: range of 192.168.1.0/24 is smaller thatn 192.168.1.0/16

When netwrkng in AWS cloud choose ntwrk size by using CIDR notation. In AWS smalles ranget is /28- gives you 16 IP addrsses. Largest IP range can have is /16, prvides you w/ 65,536 IP addrsses.

Resources:

External Site:
 Stanford: Introduction to Computer Networking

External Site:
 Ionos: CIDR: What is classless inter-domain routing?

 Intro to Amazon VPC- VPC is an islted ntwrk you create in the AWS cloud, simlar to trdtional ntwrk in data center. When you create a VPC need 3 main things: 1. Name of you VPC
         2. Region for your VPC to live in. Each VPC spans multple Availability Zones w/ in the region you choose.
         3.An IP range for your VPC in CIDR notation. Detrmnes the size of your ntwrk. Each VPC can have up to four /16 IP ranges

AWS will provision a network and IP addresses for that network. 

Create a subnet- After you create your VPC you need to create subnets inside of this network. Subnets are smaller netwrks inside your base ntwrk- or virtual area ntwrks (VLANs) in a trad, on-prem netwrk. In an on-prem netwrk, the typical use case for subnets is to isolate or optmize ntwrk trffic. In AWS, subnets are used for high availblty and prvding diff cnnctvty options for your rsrcs. When you create a subnet need to choose 3 settings:

1. VPC you want your subnet to live in, in this case (10.0.0.0/16)
2. The availability zone you want your subnet to live in, in this case AZ1
3. A CIDR block for your subnet, which must be a subset of the VPC CIDR block in this case. 10.0.0.0/24

When you launch an EC2 instnce, you launch it inside a subnet, which will be located inside the Availability Zone you choose.

High Availability w/ a VPC- When you create your subnets, keep high availability in mind. In order to maintain redndcy and fault tolernce, create at least two subnets config'd in two dif Availability Zones.

As you learned earlier in trail important to consider that "everything fails all the time"- If one of these AZs fail you still have rsrcs in another AZ avail as backup. 

Reserved IPs for AWS to config your VPC apprprtly, AWS resrves five IP addrsses in each subnet. These IP addresses are used for routing. Domain Name System (DNS) and ntwrk mgmt.

For ex: consider a VPC w/ the IP range 10.0.0.0/22. The VPC includes 1024 total IP addresses. THis is divided into 4 equal sized subnets, each w/ a /24 IP range w/ 256 IP addrsses. Out of each of those IP ranges, there are only 251 IP addresses that can be used bc AWS reserves 5.

Since AWS reserves these 5 IP addrsses, it can impact how you design your ntwrk. A common starting point is a range of /16 and subnets w/ a IP range of /24. Prvides a large amount of IP addrsses to work w/ at bothe the VPC and subnet level.

Gateways- To enable intrnt connctvty for your VPC, need to create an internet gatesway- Similar to a modem. Internet gateway cnncts your VPC to the intrnt- unlike a modem at home, gateway is highly availble and scalble- after you create a gateway need to attach it to your VPC

Virtual Private Gateway- allws you to cnnct your AWS VPC to anther private ntwrk. Once you create and attach a VGW to a VPC, gateway acts as anchor on AWS side of the cnnction- On the other side of the cnnctn, need to cnnct a custmer gteway to other prvate ntwrk. a custmr gteway dvc is a physcal dvc or sftwre app on your side of the cnnction. Once you have both gateways, can estblsh an encrpted VPN cnnction bt the two sides. 

Resources: 

External Site:
 AWS: VPC with public and private subnets (NAT)

External Site:
 AWS: custom route tables

External Site: Customer Gateway 

External Site:
 AWS: What Is Amazon VPC? 

External Site:
 AWS: VPCs and subnets

nbound rules

The Main Route Table- when you create a VPC, AWS cretes a route table called the main route table. A route table contains a set of rules, called routes, that are used to determne where netwrk trffic is drcted. AWS assumes that when you create a new VPC w/ subnets, you want traffic to flow bt them. Therefore, the dflt configrtion of the main route table is to allow trffic bt all subnets in local network. 

Destination      Target         Status     Propagated
10.2.0.0/16      local          active     No

Two main parts to this route table-
1. the destnation which is a range of IP addresses where you want your traffic to go. In ex of sending a letter, need a destntion to route the letter to the apprprate place. Same is true for routing trffic. In this case, the destnation is the IP range of our VPC network

2. The target which is the cnnction through which to send the trffic. In this case, the trffic is routed through the local VPC network

Custom Route Tables- While main route table ctrsl the routing for your VPC, may want to be more granular about how you route your trffic for spcfic subnets. For ex: your app may consist of a frontend and a database. You can create seprte subnets for these rsrcs and prvde diff routes for each of them.

If you associate a custom route table w/ a subnet, the subnet will use it instead of the main route table. By default each custom route table you create will have the local route already inside of it, allwng communcation to flow bt all rsrcs and subnets inside the VPC. 

Secure your subnets w/ network ACLs- think of as a firewall  at the subnet level. A network ACL enables you to ctrl what kind of trffic is allwed to enter or leave your subnet. Can configure this by setting up rules that define what you want to filter

INBOUND
Rule#   Type  Protocol  PortRange  Source  Allow/Deny
100    All    All       All        0.0.0.0/0  ALLOW
       IPv4
       Traffic

*      All    All       All        0.0.0.0/0   DENY
       IPv4
       Traffic

OUTBOUND
RULE#   Type   Protocol PortRange  Source  Allow/Deny
100     All     All      All      0.0.0.0/0 ALLOW
        IPv4
        Traffic

*       All      All      All     0.0.0.0/0  DENY
        IPv4
        Traffic

The default network ACL, shown in table above allows all trffic in and out of your subnet. To allow data to flow freely to your subnet, this is a good starting place. However, may want to restrct data a subnet level. For ex: if you have a web app, might restrct your ntwrk to allow HTTPS trfic and remote desktop protocol (RDP) trffic to your web servers

Inbound






Rule# SourceIP Protocol Port Allow/Deny Comments

100   All 
      IPv4 
        traffic   TCP     443   ALLOW   Allows inboun
                                        HTTPS traffic
                                        from anywhere

130  192.0.2.0/24 TCP    3389   ALLOW   Allows     inbound RDP traffic to the web servers from your home network’s public IP address range (over the internet gateway)

*      All 
       IPv4 
       traffic   All      All    DENY    Denies all inbound traffic not already handled by a preceding rule (not modifiable)

Outbound
Rule#  DestinationIP Protocol Port Allow/DenyComments

120    0.0.0.0/0     TCP   1025-65535 ALLOW Allows outbound responses to clients on the internet (serving people visiting the web servers in the subnet)

*      0.0.0.0/0      All     All    DENY     Denies all outbound traffic not already handled by a preceding rule (not modifiable)

In network ACL ex above, you allow inbound 443 and outbound range 1025-65535. BC HTTPuses port 443 to initiate a connction and will respnd to an ephemeral port. Netwok ACLs are considered stateless, so you need to inclde both the inbound and outbound ports used for the protcol. If you don't inclde outbound rnge your server would respnd but the trffic would never leave the subnet. Since netwrk ACLs are config'd by dflt to allw incming and outgoing trffic, don't need to change initial settngs unless need addtnl secrty layers.

Secure EC2 instnces w/ Secrty Groups- next layer of secrty is for your EC2 instnces. HEre can create a firewall called a scrty gtoup. Deflt configrtion of a scrty group blcks all inbnd trffic and allws all outbound trffic.

"Wouldn't this block all EC2 instnces from rcvng rspnse of any custmer rquests?"- Security groups are stateful, meaning they will remember if a cnnction is originally initiated by the EC2 instnce or from the outside and temprarily allow trffic to respnd w/out having to modfy the inbound rules.

If you want EC2 instnce to accpt trffic from the intrnet need to open up inbound ports. If have a web server, many need to accpt HTTP and HTTPS rqusts to allow that type of trffic in through your secrty group. can cfreate aninbnd rule that will allow port 80 (HTTP) and port 443 (HTTPS)

Inbound rules
Type     Protocol   Port Range   Source

HTTP(80) TCP(6)      80         0.0.0.0/0

HTTP(80) TCP(6)      80          ::/0

HTTPS(443) TCP(6)    443        0.0.0.0/0

HTTPS(443) TCP(6)    443         ::/0

Subnets can be used to segrgte trffic bt comps in netwrk. Scrty groups can be used to do same thing. Common design pttrn is orgnzing your rsrcs into diff groups and creating scrty groups for each to ctrl ntwrk comm bt them.

This allows you to define three tiers and islte each tier w/ scrty group rules you define. In this case, only allow intrnet trffic to the web tier over HTTPS, Web Tier to App Tier over HTTP, and Application tier to Database tier over MySQL. Diff from trad on-prem envrnmnts, in whch you islte groups of rsrcs via VLAN configrtn- in AWS, scrty groups allow you to achve same islation w/out tying it to your ntwrk.

Resources:

External Site:
 AWS: Route tables

External Site:
 AWS: Example routing options

External Site:
 AWS: Working with routing tables

External Site:
 AWS: Network ACLs

External Site:
 AWS: Security groups for your VPC

External Site:
 AWS: I host a website on an EC2 instance. How do I allow my users to connect on HTTP (80) or HTTPS (443)?

 Common network troubleshooting steps for Amazon VPC- Will see Employee Directry App launched on Amazon EC2 instnce placed in public subnet in   Amazon VPC. Multple netwrkng configrtions that playt into whether an instnce is accssble to internet or not. 

 List of congigs you should check if you have public EC2 instnce w/ web app that is not loading as expected. 

 1. Internet gateway- ensure that Internet Gateway (IGW) is attched to your VPC. W/out internet gateway no traffic will be allowed in or out of the VPC.

 2. Route Tables- Check the route table associated w/ the subnet of your EC2 instnce. Ensure ther is a route w/ a destntion of 0.0.0.0/0 that points to the Internet Gateway. This route allows outbound trffic to the internet. 

 3. Security Groups- Review the security group settings attched to your EC2 instnce. Make sure there are inbound rules allwing HTTP (port 80) and/or HTTPS (port 443) traffic from the internet (0.0.0.0/0). Also verify that outbound rules allow traffic to leave the instance.

 4. Network Access Control Lists- Check the NACLs associated w/ your subnet. Ensure that they allow inbound and outbound traffic for HTTP and HTTPS. Unlike secrty groups, NACLs are stateless, so you must explctly allow both inbound and outbound rules.

 5. Public IP Address- Ensure your EC2 instnce has a public IP addrss assgned. You can check in the EC2 console under the instance details. If does not have a public IP, relaunch the instnce and ensure you have the configrtion for assgnning a public IP addrss set crrctly.

 HTTP vs HTTPS- Confirm that your app is acssble via the crrct prtcol. If your app is config'd for HTTPs, ensure SSL/TLS certs are crrctly instlled and config'd. Also, check if the web browser is trying to conncect via the wrong protcol (HTTP instead of HTTPS or vice versa). For this course, the app is operating via HTTP, double check that your browser is not trying to connct via HTTPs. Can do this by selcting the addrss bar in the brwser and making sure the addrss starts w/ http and not https.

 7. User data script- If your instnce uses a user data script to configre the app on launch, verify that the scrpt has run succssflly. Check the instnce logs (/var/log/cloud-init.log or /var/log/cloud-init-output.log) for any errors that may have occrred dring the excution of the user data script.

 8. Permissions- Verfy the prmssions and roles attched to your EC2 instnce. Ensre the instnce has the necssr IAM roles and polcies to access any requred AWS services, such as S3, DynamoDB, or RDS

 9. Personal network permissions- Ensre that your persnal or coprrate netwrk does not have restrctions blocking access to the public IP address of your EC2 instnce. Some ntwrks might have frewlls or prxy settngs that could block outbound trffic to certain IP ranges or ports.

 10. Application- ensure that your app code is crrctly deplyed and running. Check the application's logs to diagnose any runtime errors. Also, make sure the web server (e.g., Apache, Nginx) is installed and rnning.

Week 2 quiz Review: Which info is needed to create a virtual private cloud? (VPC)- 

The AWS Region that the VPC will reside in. When creating a VPC in AWS the only required location related input is the AWS Region. Once the VPC is created, Avlblty Zonces and Subnets are dfned w/in that VPC- But not needed at VPC creation. 
1. Choose Region
2.Can then create subnets that are mpped to spcfc Availblty Zones (AZs) in that region

Which of the follwing can a route table be attched to? AWS accounts- AZ- Subnets- Regions

Answer: Subnets

Route tables in AWS defne how ntwrk trffc is drcted. They're attched to subnets in a VPC- Each subnet in a VPC must be asscted w/ a route table. Can explctly asscate a route table w/ a subnet, or will use the main route table by default. 

It's not AWS accounts bc route tables are not attched to accnts- they are a resrce w/ in a specfic VPC in an account, but not attched to the account

It's not Availblty zone bc route tables don't apply to AZs. Instead subnets, whch exst inside a spcfc AZ are what route tables are attched to.

It's not regions like AZs, regions are too broad. A route table is a regional resource, but it is not "attached" to the region. 


A compny wnts to allw rsrcs in a public subnet to commncte w/ the intrnet. Whch of the fllwing must the company do to meet this requrment?- Create a route to a private subnet? Attach an Internet gateway to their VPC? Create a route in a route table to the internet gateway? A and B? B and C?

Answer: B and C- Attach an internet gateway to their VPC and create a route in a route table to the internet gateway. 

To allow rsrcs in a public subnet to commncte w/ the internet the company must- Attach an internet gateway to their VPC- the internet gateway (IGW) is the compnnt that allws trffic bt your VPC and the internet. AND Create a route in a route table to the internet gateway- the subnet's route table must include a route that snds all outbnd trffc (0.0.0.0/0) to the intrnet gateway. These two steps tgther make the subnet public and allow intrnet accss

It's not Create a route to a privte subnet bc it doesn't enable intrnet accss. Routing to a prvte subnet stys w/ in the VPC and doesn't cnnct to the internet.

Not A and B bc creating a route to a prvte subnet (A) is unnecessary for public internet access. 

What is compute as a service (Caas) model?- The CaaS model offers compting rsrcs (such as virtual mchines that run on srvrs in data cntrs) on demand, by using virtual servces. 

CaaS is a cloud compting model that prvdes on-dmnd accss to compting power (Virtual machines (VMs))- Containers- Auto-scaling compute resrcs- This model allws users to prvsion, scale and manage computing rsrcs dynmclly- w/out mangng the underlying physcal hardwre.

It's not "requres users to prchase VMs and manlly prvsion srvrs- closer to a tradtnl hosting model like IaaS (Infrstrctre as a Service) w/out automation- 

NOT "Large discounts, but must run on-prem"- the opposite of cloud-based and on-demand nature of CaaS

NOT "Delivers cloud-based apps to users acrss the globe"- that descrbes SaaS (Software as a Service)

The settings of a security group block all inbound trffic and allows all outbound trffic by default- In AWS a scrty group acts as a virtual frewall for your EC2 instnces to ctrl inbound and outbound trffic. 
Inbound (default)- all inbound trffic is blcked- must explctly allow inbound by adding inbound rules. 
Outbound (default) ALL outbound trffic is allwec by dfault- means instnces can iniitaie trffic to the intrnet or other rsrcs w/out any configrtion.

What does an Amazon Elastic Compute Cloud (Amazon EC2) instnce type indicate?- 
Instnce family and size- An Amazon EC2 instnce type dfnes the hardwre specfctions of the virtual srver you're launching. Spcfclly, it indctes: Instnce family- reps the catgry of the instnce based on its intnded wrkload (e.g., compute optimized, memory-optmzed, general purpose)- 
EXs: 
t3- General Purpose
c6g- Compute optmzed
r5- Memory optmzed

Instnce size- Spcfies the rsrcs (vCPU, RAM, netwrking) within that family. 
EXs:
t3.micro, t3.medium, t3.large- All sizes w/in the t3 family.

EX: t3.micro- t3= instnce family
micro = instnce size. 

NOT Instnce plcement and size- Placement is not part of the type

NOT Instnce tenancy and billing- these are seprte settngs, not inclded in the "instnce type"

NOT AMI and networking speed- the AMI is a seprte compnnt you choose; netwrkng speed ma vary by type but is not part of the naming convntion.

What is the difference bt using AWS fargate or Amazon Elastic Compute Cloud (Amazon EC2) as the compute platform for Amazon Elastic Container Service (Amazon ECS)? 

With AWS Fargate, AWS manges and prvsions the underlying infrstrctre for hostng cntners.

When using Amazon ECS (Elastic Container Service)- you can choose bt two main compute platforms. AWS Fargate and Amazon ECS on EC2.

AWS Fargate- 
Servrless compte engine for containers- 
Don't manage servrs or clsters
AWS autmtclly prvsions, scales, and manges the infrstrctre
You simply define the task defntion (CPU, memory, container image), and AWS handles the rest
You only mangage your containers- AWS manges the compute

Amazon ECS on EC2
You run ECS tasks on a cluster of EC2 instnces
Must launch, scale, patch, and manage the EC2 instnces
Gives you more control over instnce types, netwrking and cost
You are respnsble for manging the infrstrctre. 

With Amazon ECS on EC2 you manage the instnces yourself

AWS Fargate removes the need to mange cluster capcty.

ECS does not handle source code builds or full dplyment autmtion- you need to contnerize your code and mange the EC2 infrstrctre- 

With a serverless computing model- Users do not pay for idle rsrcs- (AWS Lambda, Fargate, etc.) 
Users only pay for the compute time their code actually uses, 
Do not pay when the code is idle, 
Don't have to provsion, 
Scale or manage servers, benefit from built-in avalbty and fault tolernce. 

True or false: AWS Lambda is alwys the best soltion when rnning apps on AWS- FALSE

AWS Lambda is a good fit for: 
Short lived fnctions (event-driven tasks, APIs, file prcssing)
Auto-scaling needs w/out mnging infrstrctre
Lightweight workloads w/ unprdctble or intrmttnt trffic

Lambda not ideal with:
Long-running apps (max exction time is 15 min)
Large workloads w/ high memory/CPU needs
Apps that reqre persistnt cnnctions (e.g. Websockets)
Complex depndncies or contaner based archtctres
When you need fine-grained ctrl over the runtime envrnmnt or ntwrking

AWS Lambda is great for many use cases, but not always the best. Depnds on apps archtcre, perfrmnce needs and cost constrnts. 

Which compute service does Amazon Elastic Compute Cloud (Amazon EC2) prvde?- Virtual Machines (VMs)

Amazon Elastic Compute Cloud (Amazon EC2) prvdes scalble virtual machines (VMs) in the cloud. These VMs run on physicl servrs in AWS data centers and can be config'd w/
Custom amnts of CPU, memory, storage, and netwrking. 
Various OSs (Linux, Windows, etc)
Support for manual or auto-scaling
Full adminstrtve ctrl

NOT container servces through Amazon ECS or Amazon EKS, not EC2 drctly (Although EC2 can host contners)

NOT serverless- AWS Lambda is the main servrlss compute option. EC2 requres servr prvsning and mgmt.

NOT Analytics- AWS prvdes analtics via servcs like Amazon EMR, Athena, and Redshift, not EC2.

Which stage of the instnce lifecycle is an instnce in when the account strts to accmlte charges?- When an instnce is in a running stage.

Which component of the c5.4xlarge instnce detrmnes the instnce famly and genrtion number? 
4x
Large
4xlarge
c5

Answer: c5

c5 id's the Instance family "c"= Compute optmzed
AND Generation number "5"= 5th generation

4xlarge- Instance size (CPU/RAM config)

Which container runtime can be used to host a contner on Amazon Elastic Compute Cloud (Amazon EC2) instance?
Docker
Container
Amazon Simple Storage Service (Amazon S3)
Amazon EC2

Answer: Docker- a widely used container runtime that can be installed on an Amazon EC2 instnce to host and run containers. Allows you to pckge apps and depndncies into contners. Can manlly instll Docker on EC2 or use Amazon ECS (with the EC2 launch type) which uses Docker under the hood. 

NOT Container which is a general term, not a runtime
NOT Amazon Simple Storage Service (Amazon S3)- which is an object storage, not a compute or container runtime envrnmnt
NOT Amazon EC2- which is the virtual machin (VM) itself, not the software used to run containers. 



TBC


Week 3-

Storage Types on AWS-Grouped into three diff catgries: Block Storage, File Storage, and Object Storage

File Storage: Folders and Subfolders- used to organize- 
Each file has metadata- name, size, and date created. 
File also has a path e.g. computer/Application_files/Cat_photos/cats-03.png- can use to find file in hierarchy
Ideal when you need centrlzed accss to files that need to be shared and mnged by multple host comps. Typclly mounted onto multple hosts and requres file lcking and intgrtion w/ exsting file system comm protcols. Common use cases are: 
  Large Content repositories
  Development Environments
  User Home Dirctories. 

Block Storage- file storage treats files as singlar unit, blcok storge splits files into fixed-size chunks of data called blocks that have their own addresses. Each block is addressable, blocks can be rtrved efficiently 
When data is rqusted, these addrsses are used by the strge systm to orgnze the blcks in the crrct order to form a complte file to present back to the requstor. Outside of the address, there is no addtnl metadata asscted w/ each block. So, when you want to change a charctr in a file you just change the block, or the piece of the file that contains the charcter. This ease of access is why block strge solutions are fast and use less bandwdth. 
Since blck strge is optmzed for low-latncy ops it is typcl strge choice for high-perfrmnce entrprse wrkloads, such as databases or entrprse rsrc planning (ERP) systems, that require low-latency storage

Object Storage- Objcts, much like files are also treated as a single unit of data when stored. However, unlike file strge, these objcts are stred in a flat strctre instead of a hierarchy. Each object is a file w/ a unique IDer. This IDer, along w/ any addtnal metadata, is bundled w/ the data and stored. 
With object storage, you can store almost any type of data, and there is no limit to the num of objcts stored, making it easy to scale. Object storage is genrlly useful when string large data sets, unstrctred files like media assets, and static assets, such as photos. 

Relating back to Traditional Storage Systems- If you've worked w/ storage on-prem, may alrdy be famlr w/ block, file, and objct strge. Consider the fllwing techs and how they relate to systms you may have seen before. 
  Block storage in the cloud is analogous to dirct attched storage (DAS) or a Storage Area Network (SAN)
  File storage systems are often spprted w/ a netwrk attched storage (NAS) server.
Adding more strge in a trad data center enviro is a more rigid prcess, as you need to purchse, instll, and configre these strge solutions. W/ cloud compting the prcss is more flxble. You can create, delete, and modify strge soltions all w/in a matter of minutes. 

Resources:

External Site:
 AWS: What Is Cloud Storage

External Site:
 AWS: Types of Cloud Storage

Amazon EC2 Instance Storage and Amazon Elastic Block Store-

Amazon EC2 Instance Store- prvides temprry block-level strge for your instnce. This strge is lcted on disks that are phsclly attched to the host compter- ties the lifecycle of your data to the lifecycle of your EC2 instnce. If you delete your instnce, the instnce store is deleted as well. Due to this, instnce store is considered ephemeral strge. Read more here: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html

Instnce store is ideal if you are hosting apps that replcte data to other EC2 instnces, such as Hadoop clusters. For these cluster-based wrkloads, having the speed of loclly attched volmes and the resiliency of replcted data helps you achve data distrbtion at high prfrmnce. Also idel for temp strge of info that chnges frqntly, such as buffers, caches, scrtch data, and other temp content.

Amazon Elastic Block Strge (Amazon EBS)- as the name implies, Amazon EBS is a block-levl strge dvc that you can attch to an Amazon EC2 instnce. These strge dvcs are called Amazon EBS volumes. EBS volumes are essntlly drves of a user-config'd size attched to an EC2 instnce, similr to how you might attch an extrnl drive to your laptop. 
EBS volumes act simlrly to extrnal drves in more than one way.
  *Most Amazon EBS volumes can only be cnncted w/ one comp at a time. Most EBS volumes have a one-to-one reltnship w/ EC2 instnces, so they can't be shred by or attched to multple instnces at one time. Just released a multi-attach feature, not availble for all instnce types and must be in same AZ.
  *Can detach an EBS volume from one EC2 instnce and attch it to another EC2 instnce in same AZ to accss data from it.
  *The extrnl drive is seprte from the comp. That means is an accdnt hppns and the comp goes down, you still have your data on your extrnl drive. The same is true for EBS volumes.
  *You're limited to the size of the extrnl drive since it has a fixed limit to how scalble it can be. For ex. May have a 2 TB extrnl drve and that means you can only have 2 TB of contnt on there. Relates to EBS as well since vlmes also have a max limitation of how much content you can store on the volume.

Scale Amazon EBS Volumes- Can scale Amazon EBS volumes in two ways.
  1. Increase the volume soze, as long as it doesn't increase above the max size limit. For EBS volumes, the max amnt of strge you can have is 16 TB. Means if you prvision a 5 TB EBS volume, you can choose to increase the size of your volume until you get to 16 TB.

  2. Attch multple vlmes to a single Amazon EC2 instnce. EC2 has a one-to-many reltionshp w/ EBS volumes. Can add these addtnl volmes dring or after EC2 instnce creationt o prvde more strge capcty for your hosts.

Amazon EBS Use Cases- Amazon EBS is useful when you need to rtrve data quickly and have data persist lont-term. Volumes are commonly used in the fllwing scnrios.

  *Operating Systems: Boot/root volumes to store an OS. The root dvc for an instnce launched from an Amazon Machine Image (AMI) is typclly an Amazon EBS volume. These are commnly refrred to as EBS-backed AMIs
  *Databases: a strge layer for databses running on Amazon EC2 that rely on transactional reads and wtites.
  *Enterprise applications: Amazon EBS prvdes reliable blck strge to run busness-critical apps. 
  * Throughput-intensive apps: Apps that prfrm long, continuous reads and writes

EBS Provisioned IOPS SSD-
  Description
Highest performance SSD designed for latency-sensitive transactional workloads
  Use Cases
I/O-intensive NoSQL and relational databases
  Volume Size
4 GB-16 TB
  Max IOPS/Volume 
64,000
  Max Throughput/Volume
1,000 MB/s

EBS General Purpose SSD
  Description
General Purpose SSD balnces price and prfrmnce for wide vrty of transctional wrkloads
  Use Cases
Boot volumes, low-latency interactive apps, devlpmnt, and test
  Volume Size
1 GB-16 TB
  Max IOPS/Volume
16000
  Max Throughput/Volume
250 MB/s

Throughput Optimized HDD
  Description
Low-cost HDD desgned for frqntly accssed, throughput intensive wrkloads
  Use Cases
Big data, data warehouses, log processing
  Volume Size
500 GB-16 TB
  Max IOPS/Volume
500
  Max Throughput/Volume
500 MB/s

Cold HDD
  Description
Lowest cost HDD designed for less frquntly accssed wrkloads
  Use Cases
Colder data requring fewer scans per day
  Volume Size
500 GB-16 TB
  Max IOPS/Volume
250
  Max Throughput/Volume
250 MB/s

Two main catgries of Amazon EBS volumes: solid-state drives (SSDs) and hard-disk drives (HDDs). SSDs provide strong perfrmnce for random input/output (I/O), while HDDs prvde strng perfmnce for sequntial I/O. AWS offers two types of each. Above table will help decide which is best for your workload. 

Benefits of Using Amazon EBS-
  *High avlblty: when you create an EBS volume, it is autmtclly replcted w/ in its AZ to prvnt ata loss from single points of failure
  *Data persistnce: the strge prsists even when your instnce doesn't
  *Data encryption: All EBS volumes supprt encrption
  *Flexblty: EBS volmes supprt on-the-fly chnges. Can modfy volume type, volme size, and input/output ops persecond (IOPS) capcty w/out stppng your instnce.
  *Backups: Amazon EBS prvdes you the ablty to create bckups of any EBS volume

  EBS snapshots- Errors happen. one of those errors is not backing up data, and then, inevtbly losng that data. To prvnt this, back up your data. Even in AWS. Since your EBS volmes consist of the data from your Amazon EC2 instnce, you'll want to take backups of these volmes, called snapshots
  EBS snapshts are incrmntl backups that on ly save the blocks on the volume that have changed after your most recent snapshot. For ex if you have a 10 GB of data on a volume and only 2 GB of data have been modfied since your last snapshot, only the 2 GB that have been chnged are wrtten to Amazon Simple Storage Service (Amazon S3)
When you take a snapshot of any of your EBS volumes, these backups are stred redntly in multple AZs using Amazon S3. This aspect of storing the backup in Amazon S3 will be handled by AWS, so you won't need to interact with Amazon S3 to work w/ your EBS snampshots, Simply mange them in the EBS consol (part of the EC2 console)
EBS snapshots can be used to create multple new volmes, whether they're in the same AZ or a diff one. When you creat3e a new volume from a snbapshot it's an exact copy of the orignl volume at the time the snapshot was taken.

Resources
External Site:
 AWS: Amazon Elastic Block Store (Amazon EBS) 

External Site:
 AWS: Amazon EBS FAQs 


Object Storage w/ Amazon S3: What is Amazon S3?- Standalone storge solution not tied to compte. Enables you to retrve your data from anywhere on the web. 
Amazon S3 is an object storage servce- stores data in a flat strctre, using unque IDers to look up objcts when rqsted. Object is a file combned w/ metadata and that you can store as many of these objects as you want. 

Understand Amazon S3 Concepts- in Amazon S3 you have to store your objcts in contners called buckets. Can't upload any objct, not even single photo to S# w/out creatng a bucket first. When you create a bucket you choose a minimum 2 things: bucket name and AWS Region you want the bucket to reside in. 
First- choose the Region you want the bucket to reside in. Tpclly this wll be a Region that you've used for other rsrcs, such as your compute. When you choose a Region for your bucket, all objcts you put inside that bucket are redndntly sred acrss multple dvcs, acrss multple AZx this level of redndncy is dsgned to prvede Amazon S3 custmrs w 99.999999999% durblty and 99.99% avlblty for objcts over a given year. 
Second- choose bucket name- must be unique across all AWS accnts. AWS stops you from chosing a bucket name that has already been chosen by someone else in another AWS account. Once you choose a name that name is yours and cannot be clmed by anyone else unless you delete that bucket, which then releases the name for others to use. 
AWS uses this name as part of the objct IDer. in S3 each objct is IDd using a URL which looks like:
http://doc.s3.amazonaws.com/2006-03-01/AmazonS3.html

'doc' is the bucket
2006-03-01/AmazonS3.html is the Object/key

After the http://, you see the bucket name. here the bucket name is 'doc' Then the IDer uses the servce name, s3 spcfies the srvc prvder amazonaws. After that, you have an implied folder inside the bucket called 2006-03-01 and the objct insde the folder that is named AmazonS3.html. The objct name is oftn rfrred to as the key name.

Can have fldrs insde of buckts to help ou orgnze objcts. However, remmber there's no actual file hierarchy that spprts this on the back end. It is a flat strctre where all files and flders live at the same level. Using buckets and folders implies a hierarchy, which makes it easy to undrstnd for the human eye. 

S3 Use Cases- one of the most wdely used strge srvcs, with far more use cases than could fit on one screen. The fllwng list smmrzes most common uses.

  *Backup and storage- S3 is natural place to back up files bc it is highly redndnt. as mentioned in the las unit, AWS stres your EBS snapshts in S3 to take advntge of its high avlblty. 
  *Media hosting- BC you can store unlmted objcts, and each indvdl objct can be up to 5 TBs, S3 is an ideal loction to host video, photo, or music uploads. 
  *Software delvry- You can use S3 to host your software apps that custmers can download.
  *Data lakes: S3 is an optimal foundtion for a data lake bc of its vrtlly unlmted sclblty. You can increase strge from gigabytes to petabytes of content, paying for only what you can use
  *Static websites- You can config your bucket to host a static website of HTML, CSS, and client-side scripts.
  *Static content- BC of the limitless scling, the supprt for large files, and the fact that you access any objct over the web at any time, S3 is the perfct plce to store static content.

Choose the right Connctvity Option for your Rsrces-
Evrythng in Amazon S# is private by dflt. This means that all S3 resrces, such as buckets, folders, and objcts can only be viewedby the user or AWS account that created that rsrc. Amazon S3 rsrcs are all prvte and prtcted to begin with.

If you decide you want evryone on the internet to see your photos, you can choose to make your buckets, folders,and objcts public. A public rsrc means that evryone on the intrnet can see it. Most of the time, you don't want your prmssions to be all or nthng. Typclly you want to be more grnular about the way you prvide access to your rsrcs.

To be more spcfc about who can do what w/ your S3 rsrcs, Amazon S3 prvdes two main accss mgmt featres: IAM policies and S3 bucket policies. 

Understand IAM policies- When Iam polcies are attched to IAM users, groups, and roles, the polcies define which actions they can prfrm. IAM polcies are not tied to any one AWS servce and can be used to define access to nearly any AWS action. You should use IAM polcies for prvte buckets when:
  *You have many buckets w/ diff permssion reqrmnts. Instead of defning many diffrnt S3 bucket polcies, you can use IAM polcies instead
  *You want all polcies to be in a centrlzed location. Using IAM polcies allws you to manage all policy info in one location. 

Understand S3 Bucket Policies- S3 bucket polcies are simlar to IAM polcies, in that they are both defined using the same policy lang in a JSON format. The Diff is IAM polcies are attched to users, groups, and roles, whereas S3 bucket polcies are only attched to buckets. S3 bucket polcies specfy waht actions are allwed or dnied on the bucket.
For ex: if you have a bucket called employeebucke, you can attch an S3 bucket polcy to it that allws another AWS account to put objcts in that bucket.
Or if you wanted to allow anonymous viewers to read the objcts in employeebucket, then you can apply a policy to that bucket that allows anyone to read objcts in the bucket using "Effect": Allow on the "Action["s3:GetObject"]"

Here's an ex of what that S3 bucket policy may look like.

{

    "Version":"2012-10-17",
    "Statement":[

      {

        "Sid":"PublicRead",

        "Effect":"Allow", 

        "Principal":"*",

        "Action":["s3:GetObject"],

        "Resource":["arn:aws:s3:::employeebucket/*"]

      }
    ]
}

S3 bucket policies can only be placed on buckets, and can't be used for folders or objcts. However, the policy that is placed on the bucket applies to every objct in that bucket. You should use S3 bucket polcies when:
  *You need a simple way to do cross-account access to S3, w/out using IAM roles.
  *Your IAM policies bump up against the defined size limit. S3 bucket polcies have a larger size limit

Encrypt S3- Amazon S3 reinforces encrption in trnsit (as it travels to and from Amazon S3) and at rest. To prtct data at rest, you can use:
  *Server-side encrption: this allws Amazon S3 to encrpt your objct before saving it on disks in its data centers and then decrypt it when you download the objcts
  *Client-side encrption: encrpt your data client-side and upload the encrpted data to Amazon S3. In this case, you manage the encrption prcess, the encrption keys, and all related tools.

To encrpt in transit, you can use client-side encrption or Secure Sockets Layer (SSL)

Use Versioning to Preserve Objects- As ou know Amazon S3 IDs objcts in part by using the onjct name. For ex: when you upload an emplyee photo to S3, you may name the objct employee.jpg and store it in a folder called employees. If you don't use Amazon S3 versioning, anytime you upload an objct called employee.jpg to the employees folder, it overwrites the orignal file. This can be an issue:
  *employee.jpg is a common name for an employee photo objct. You or someone else who has access to that bucket might not have intnded to overwrite it, and now that you ahve, no longer have access to the orignl file.
  *May want to preserve diff versions of employee.jpg. Without versioning, if you wantd to create a new version of employee.jpg, you would need to upload the objct and choose a diff name for it. Having several objcts all w/ slight diffs in naming variations may cause confusion and clutter in your bucket. 

  So you use S3 versioning. Versioning enables you to keep multple versions of a single objct in the same bucket. This allows you to preserve old versions of an objct w/out having to use diff naming constrcts, in case you need to recover from accdntl deletions, accdntal overwrites, or app failures. Let's see how this works:

  If you enable versioning for a bucket, Amazon S3 autmtclly genrates a unique version ID for the objct being stored. In one bucket, for ex, you can have two objcts w/ the same key, but diff version IDs, such as employeephoto.gif (version 111111) and employeephoto.gif (version 121212). Versioning-enabled buckets let you recover objcts from accdntl deletion or overwrite. 

    *Deleting an objct does not remove teh objct permnntly. Instead, Amazon S3 puts a marker on the object that shows you tried to delet it.If you want to restore the objct, you can remove this marker and it reinstates the objct. 

    *If you overwrite an objct, it reslts in a new objct version in the bucket. You still have access to ppprevious versions of the objct. 

Understand versioning States- 

  *Unversioned (the default): No new or existing objcts in the bucket have a version

  *Versioning-enabled: This enables versioning for all objcts in the bucket. 

  *Versioning-suspended: This suspends versioning for new objcts. All new objcts in the buckt will not have a version. However, all existing objcts keep their objct versions.

The versioning state applies to all of the objcts in that bucket. Keep in mind that storage costs are incurred for all objcts in your bucket and all versions of those objects. To reduce your S3 bill, you may want to delet previous version of your objcts that are no longer in use. 

What are Amazon S3 Storage Classes?

When you upload an objct to Amazon S3 and you don't specify the strage class, you're uploading it to the dflt strge class- often refrred to as stndrd strage. When you learned about Amazon S3 in previous units, you were learning about the standard storage class w/out even knowing it. S3 storage classes let ou change your storage tier as your data chrctrstcs change. For ex, if you are now accssing your old photos infrquntly, you may want to change the strge class those phots are stored in to save on costs. There are six S3 strage classes.

  1. Amazon S3 Standard: This is considered general purpose strage for cloud apps, dynamic websites, content distrbtion, mobile and gaming apps, and big data analytics

  2. Amazon S3 Intelligent-Tiering: This tier is useful if your data has unkown or changing access patterns. S3 Intelligent-tiering stores objcts in two tiers, a frequent access tier and an infrquent access tier. Amazon S3 monitors access patterns of your data, and automatically moves your data to the most cost-effective storage tier based on frequncy of access.

  3. Amazon S3 Standard-Infrequent Access (S3 Standard-IA): S3 Standard-IA is for data that is accessed less frequently, but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, adn low latency of S3 Standard, with a low per-GB storge prce and per GB retrval fee. This storge tier is ideal if you want to store long-term backups, disaster recovery files, and so on. 

  4. Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA): Unlike other S3 storage classes which store data in a minimum of three AZs, S3 One Zone-IA stores data in a single AZ and costs 20% less than S3 Standard-IA. S3 One Zone-IA is ideal for custmers who want a lower-cost option for infrqntly accssed data but do not require the availability and resilience of S3 Standard or S3 Standard-IA. A good choice for storing secondary backup copies on on-prem data or easily re-creatable data. 

  5. Amazon S3 Glacier Instant Retrieval: Amazon S3 Glacier Instant Retrieval is an archive strage class that delivers the lowest-cost strage for long-lived data that is rarely accssed and requres retrval in milliseconds.

  6. Amazon S3 Glacier Flexible Retrieval: S3 Glacier Flexible Retrieval delivers low-cost strage up to 10% lower cost (than S3 Glacier Instant Retrieval), for archive data that is accessed 1-2 times per year and is retrieved asynchronously.

  7. Amazon S3 Glacier Deep Archive: S3 Glacier Deep Archive is Amazon S3's lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed once or twice in a year. Designed for customers- particularly those in highly regulated industries, such as Financial Services, Healthcare, and Public Sectors- that retain data sets for 7 to 10 years or longer to meet regulatory compliance requrments. 

  8. Amazon S3 Outposts: Amazon S3 on Outposts delivers objct storage to your on-prem AWS Outposts environment.

Automate Tier Transitions With Object Lifecycle Management

If you keep manually changing your objcts, such as your employee photos, from storage tier to storage tier, you may want to look into autmating this prcess using a lifecycle polcy. When you define a lifecycle polcy configrtion for an objce or group of objcts, you can choose to automate two actions: transition and expiration actions. 

  *Transition actions are used to defne when you should transition your objcts to another strage class

  *Expiration actions define when objcts expire and should be permnntly deleted

For ex, you might choose to transtion objcts to S3 Standard-IA strage class 30 days after you created them, or archive objcts to the S3 Glacier Strge class one year after creating them. 

The fllwing use cases are good candidates for lifecycle mgmt. 

  *Periodic logs: If you upload periodic logs to a bucket, your app might need them for a week or a mont. After you might want to delete them.

  *Data that changes in access freqncy: some docs are frquntly accssed for a limited period of time. After that, they are infrquntly accssed. At some point, you might not need real-time access to them, but your org or regltions might requre you to archve them for a spcfic period. After that you can delete them. 

# Choose the Right Storage Service

Amazon EC2 Instance Store- Instance store is ephemeral block storage. Preconfig'd storage that exists on the same physical server that hosts the EC2 instance and cannot be detached from Amazon EC2. can think of it as a built-in drive for your EC2 instnce. Instnce store is genrlly well-suited for temp strage of info that is constntly changng, such as bufers, caches, and scratch data. Not meant for data that is persistnt or long-lasting. If you need persistent long-term block strage that can be detached from Amazon EC2 and prvide you mor mgmt scalablty, such as incrsing volume size or creating snapshots, then you should use Amazon EBS. 

Amazon EBS- meant for data that chnges frquntly and needs to persist through instnce stops, terminations, or hardware failures. Amazon EBS has two dif types of volumes: SSD-backed volumes and HDD-backed volumes. SSD-backed volumes have the following charctrstcs
  *Perfrmnce depnds on IOPS (input/output operations per second)

  *Ideal for transactional wrkloads such as databases and boot volumes.

HDD-backed volumes have the fllwing chrctrstics:

  *Prfrmnce dpnds on MB/s

  *Ideal for throughput-intensive workloads, such as big data, data warehouses, log prcessing, and sequntial data I/O

A few important features of Amazon EBS that you need to know when comparing it to other srvcs:

  *It is block strage

  *You pay for what you provision (have to provision storage in advance).

  *EBS volumes are replcated across multple srvrs in a single AZ.

  *Most EBS volumes can only be attached to a single EC2 instance at a time

  Amazon S3- If data doesn't change that often, Amazon S3 might be more cost-effctive and scalble sorage solution. S3 is ideal for storing static web content and media, backups and archiving, data for analytics, and can even be used to host entire static websites w/ custom domain names. A few imprtnt features of Amazon S3 to know about when comparing it to other services.

    *It is Object Storage

    *Pay for what you use (don't have to provision storage in advance)

    *Amazon S3 replcates your objcts acrss multple AZs in a Region. 

    *Amazon S3 is not storage attached to compute

  
Amazon Elastic File System (Amazon EFS) and Amazon FSx

S3 uses a flat namespace and isn't meant to serve as a standalone file system. 

Most EBS volumes can only be attchd to one EC2 instnce at a time. 

If you need file strage on AWS, whch srvc should you use? For file strage that can mount on to multple EC2 instnces, you can use Amazon Elstic File System (AMazon EFS) or Amazon FSx. Following table prvides more info on each srvce.

Service: Amazon Elastic File System (EFS)
Charctrstic- Fully managed NFS file system.
More info- https://aws.amazon.com/efs/faq/

Service: Amazon FSx for Windows File Srver
Charctrstic- Fully Managed file servr built on Windows Servr that spprts the SMB protocol
More info- https://aws.amazon.com/fsx/windows/faqs/?nc=sn&loc=8

Service: Amazon FSx for Lustre
Charctrstic- Fully managed Lustre File system that integrates with S3
More info- https://aws.amazon.com/fsx/lustre/faqs/?nc=sn&loc=5

A few imprtant features of Amazon EFS and FSx to know about when compring to other srvcs

  *It is file storage

  *You pay for waht you use (don't have to provision strage in advnce)

  *Amazon EFS and Amazon FSx can be mounted onto multple EC2 instnces


Resources:

External Site:
 AWS: Storage- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Storage.html

External Site:
 AWS: Cloud Storage on AWS- https://aws.amazon.com/products/storage/

External Site: 
Amazon EFS How it works
 

External Site: 
Amazon FSx for Windows File Server
 

External Site: 
Amazon FSx for Lustre


### Explore Databases on AWS

The History behind Enterprise Databases- Used to be strghtfrwrd, Only a few vendors and chose one for all apps.

Often would slct database before knowledge of use case. Since 1970's most common was relational database

What is Relational Database?- Orgnzes data into tables. Data in one table can be linked to data in other tables to create reltionships- hence, the reltnal part of the name

A table sotres data in rows and columns. A row often called a record, contains all info about a spcfic entry. Columns descrbe attrbtes of that entry. 

The tables, rows, columns, and reltionshps bt them is refrred to as logical schema. With relational databases a schema is fixed. Once the database is oprtnal, becomes diffclt to chnge the schema. This reqres most of the data modeling to be done upfront before the database is active

WHAT is a Relational Database Mgmt System? (RDBMS)- lets you create, update, and adminster a reltional database. Some ex's:
  *MySQL
  *PostgresQL
  *Oracle
  *SQL server
  *Amazon Aurora

You communcate w/ most RDBMS by using Structured Query Language (SQL) queries. Here's an ex: SELECT*FROM table_name

This query slcts all the data from a partclr table. But the real power of SQL quries is in creating more complex queris that let you pull data from severl tables to piece togther pattrns and answers to busnss prblms. For ex: querying the sales table and the book table togther to see sales in reltion to an author's books. This is made possble by a join, Which we talk about next. 

THe Benefits of Using a Relational Database-
  *Joins: can join tables, allwng to bettr undrstnd reltnshps bt your data
  *Reduced Redundncy: can store data in one table and refrnce it from other tables instead of savng the same data in diff places
  *Familiarity: Reltional datbases have been a poplr choice since 70's. Due to this poplrity, technical pros oftne have famlrity and exprience w/ this type of database
  *Accuracy: Reltnal datbases ensure that your data is persisted w/ high integrty and adheres to the ACID (atomicity, consistency, isolation, durability) principle.

USE CASES FOR RELATIONAL DATABASES-Much of the world runs on reltional databases. In fact, at the core of many mission-critical apps, some of which you may use in your day to day life. Some common use cases for relatnal databases. Apps that have a solid schema that doesn't change often, i.e.
  *Lift and shift apps that lifts an app from on-prem and shifts to the cloud w/ littl or no mods

Applications that need persistnt strage that fllws the ACID principle, such as:
  *Entrprise Rsrc Plnning (ERP) apps
  *Customer Reltionship MGMT (CRM) apps
  *Commerce and financial apps

CHOOSE BT UNMANAGED and MANAGED DATABASES-

If you want to run a reltional database on AWS, first need to slct how you want to run it: the unmanaged or managed way

Paradigm of managed versus unmanaged services is similar to the Shared Responsibility Model. The Shared Responsibility MOdel distngshes bt AWS's and the customer's scrty respnsbility over a service. Similrly, managed versus unmanaged can be understood as a trade off bt convnience and control.

ON-PREM DATABASE- Let's say uo oprte a reltnal database on-prem (in your own data center.) In this scenario, you are respnsble for all aspcts of oprtion inclding the scrty and elctrcty of the data center, the magmt of the host machine, the mgmt of the dtbase on that host, as well as optmzing quries and managing customer data. You are respnsble for absltely evrthing, which means you have ctrl over absltely evrthing.

Includes-App optmzation, scaling, high avlblty, dtbase backups, DB s/w patches, DB s/w installs, OS patches, OS instlltions, server maintnce, Rack & stack, Power, HVAC, net.

Where with AWS hosting they take care of OS instlltion, Server maintnce, Rack and stack, Power, HVAC, net

Now say you want to shift some of this to AWS by running your reltnal datbase on Amazon EC2. If you host a database on Amazon EC2, AWS takes care of implmntingand maintning the physcal infrstrcture and hardware and instlling the OS of the EC2 instnce. But you're still respnsble for managng the EC2 instnce, managng the database on that host, optmzing queries, and managng customer data. 

This is refrred to as unmanaged database option on AWS. AWS is repsnble for and has ctrl over the hardwre and undrlying infrstrctre and you are respnsble and have ctrl over mgmt of the host and database.

MANAGED DATABASE- 

You- App optmzation. 

AWS- Scaling, High Avalblty, Database backups, DB s/w patches, DB s/w installs, OS patches, OS instlltion, Server maintnance, Rack and stack, Power, HVAC, net.

If you want to shift even more work to AWS use Managed Database service. Sets up both the EC2 instance and the database, and they provide systms for high avalblty, sclblty, patchng, and backups. However you're still respnsble for database tuning, query optmztion, and ensring data is secre. PRvides you ultmate convnience, but you ahve the least amnt of ctrl

Resources:

External Site:
 AWS: What Is a Relational Database?

External Site:
 AWS: Databases on AWS 

### WHAT is AMAZON RDS?- 
Enables you to ceate and manage reltional datbases in the cloud w/out the oprtional burdn of tradtnal database mangmnt. For ex: if you sell healthcare equipmnt and your goal is to be the number-one seller in the Pacific NW, building out a dataabase doesn't drctly help you achve that goal though having a database is necssry to achve the goal. Amazon RDS helps you offload some of this unrlted work of creating and managng a database. you can focus on the tasks that diffrntiate your app, instead of infrstrcture-related tasks such as prvsioning, patchng, scling, and restoring. Amazon RDS spprts most of the popular reltional database mgmt systms, rangng from commrcl optns, open src options, and even an AWS-spcific option. Supported Amazon RDS engines are
  *Commercial: Oracle, SQL Server
  *Open Source: MySQL, PostgreSQL, MariaDB
  *Cloud Native: Amazon Aurora

NOTE:Cloud natve, option, Amazon Aurora is a MySQL and PostgreSQL-compatible database built for the cloud. It is more durable, more available, and prvdes faster prfrmnce than the Amazon RDS version of MySQL and PostgreSQL. See also: Amazon Aurora FAQs

Understand DB Instances- Just like the databases you wold build and manage yourself, Amazon RDS is built off of compute and strage. The compute portion is called the DB (database) instance, which runs the database engine. Depnding on the engine of the DB instance you choose, the engine will have diffrent supprted featres and congigrtions. A DB instance can contain multple databases w/ the same engine and each database can contain multple tables. Under the DB instnce is an EC2 instnce. However this instnce is managed through the Amazon RDS console instead of the Amazon EC2 console. When you create your DB instnce you choose the instnce type and size. Amazon RDS supprts three instance families. 

  *Standard, general purpose instnces
  *Memory Optimized, optimized for memory-intensive apps
  *Burstable Performance, prvides a baseline prfrmnce level, with the ablity to burst to full CPU usage.

The DB instnce you choose affcts how much prcssing powr and memory it has. Not all of the options are avalble to you, depnding on the engine that you choose. You can find more info in rsrcs at end of this reading. Much like a reglar EC2 instnce, the DB instnce uses Amazon Elastic Block Store (EBS) volumes as its strage layer. Can choose bt three types of EBS volume storage. 
  *General purpose (SSD)
  *Provisioned IOPS (SSD)
  *Magnetic storage (not reccmmnded)

WORK WITH AMAZON RDS in an AMAZON VIRTUAL PRIVATE CLOUD

When you create a DB instnce, you slect the Amazon Virtual Private Cloud (VPC) that your databaseswill live in. Then you select the subnets that you wnt the DB instnces to be placed in. Refrred to as a DB subnet group. To create a DB subnet group you specify:
  *The AZs that include the subnets you want to add
  *The subnets in that AZ where your DB instance are placed

The subnets you add should be private so they don't hvae a route to the internet gateway. Ensres your DB instance, and the cat data inside of it, can only be reached by the app backend. Accss to the DB instnce can be further restrcted by using ntwrk accss control lists (ACLs) and secrity groups. With these firewall, you can control, at a granular level, what type of trffic you want to allow into your database. Using these ctrls prvde layers of secrity for your infrstrctre. It reinfrces that only the backend instnces have access to the database.

Use AWS Identity and Access Management (IAM) Policies to secure Amazon RDS- Netwrk aCLs and secrity groups allow you to dictate the flow of trffic. If you want to restrct what actions and resrcs your emplyees can access, you can use IAM policies.

## Back up your DATA-
To take regular backups of your RDS instnce, you can use:
  *Automatic backups
  *Manual snapshots

Automatic Backups- Turned on by default. Backs up your entire DB instnce (not just indvdual databases onthe instnce), and your transaction logs. When you create your DB insntc you set a backup window that is the period of time that automatic backups occur. Typclly you want to set these windows dring a time when your database expriences little actvity bc it can cause incresed latncy and dwntime.

Can retain your autmated backups bt 0 and 35 days. might ask yourself "Why set up automated backups for 0 days?" the 0 days settng actlly disable autmatic backups from happneing. Keep in mind that if you set it to 0, will also delete all existing autmted backups. Not ideal, as the benefit of having autmated backups is having the ablty to do point-in-time recovery.

If you restre data from an autmated backup, you have the ablity to do point-in-time recovery. Point-in-time recovery creates a new DB instance using data restred from a specfic point in time. This restration method prvdes more granulrity by restring the full backup and rolling back transctions up to the spcfied time range. 

Manual Snapshots- If you want to keep your autmated backups longer than 35 days, use manual snapshots. Manual snapshots are similar to taking EBS snapshot, except you manage them in the RDS console. These are backups that you can initiate at any time, that exist until you delte them. For ex: to meet a compliance requrment that mandates you to keep database backups for a year, you would need to use manual snapshots to ensure those backups are retained for that perios of time. If you restore data from a manual snapshot it creates a new DB instnce using the data from the snapshot. 

WHICH BACKUP OPTION SHOULD I USE?- almost always BOTH. Automated backups are beneficial for the point-in-time recovery. Manual snapshots allow you to retain backups for longer than 35 days.

Get Redundancy with Amazon RDS Multi-AZ- When you enable Amazon RDS Multi-AZ, Amazon RDS creates a redndnt copy of your datbase in another AZ. You end up w/ two copies of your datbase: a primry copy in a subnet in one AZ and a stndby copy in a subnet in a second AZ.

The primary copy of your database prvdes accss to your data so that apps can query and display that info. 
The data in the primary copy is synchronously replicated to the standby copy. The standby copy is not considered an active database and does not get queried by apps.
To improve avalblty, Amazon RDS Multi-AZ ensures that you have two copies of your database running and that one of them is in the primary role. If there's and availability issue, such as the primary DB losing connctivity, Amazon RDS trggers an automatic failover.

When you create a DB instance, a domain name system (DNS) name is prvided. AWS uses that DNS name to failover to the standby database. In an automatic failover, the standby databaseis prmoted to the primary role and queries are redirected to the new primary database. 

To ensure that you don't lose Multi-AZ configration, a new standby database is created by either 
  *Demoting the previous pirmary to standby if it's still up and running
  *Or standing up a new standby DB instance

The reason you can selct multple subnets for an Amazon RDS database is bc of the Multi-AZ configrtion. You'll want to ensure that you have used subnets in diff AZs for your primary and standby copies.

Resources:

External Site:
 AWS: Working With Backups

External Site:
 AWS: Amazon RDS Backup and Restore

External Site:
 AWS: Creating and Using an IAM Policy for IAM Database Access

External Site:
 AWS: Amazon Virtual Private Cloud VPCs and Amazon RDS

### INTRO TO DYNAMODB-
 What is Amazon DynamoDB- fully managed NoSQL databse srvc that prvdes fast adn prdctble prfrmnce w seamless sclblty. DynamoDB lets you offload the adminstrtve burdens of operating and scling a distrbted database so you don't have to worry about hardwre prvsning, setup and configrttion, replicacion, software patching, or cluster scaling.

With DynamoDB you can create database tables that can store and retrieve any amount of data and serve any level of request trffic. Can scale up or scle down your tables' throughput capcity w/out downtime or perfrmnce degrdtion. Can use the AWS Management Console to monitor rsrc utlztion and prfrmnce metrics.
DynamoDB autmtclly spreads the data and trffic for your tables over a suffcient number of srvers to hanle your throughput and strage requrmnts, while maintning consistnt and fast prfrmnce. All your data is stored on solid-state disks (SSDs) and is autmtclly replcted acrss multple AZs in AWS Region, prvding built-in high avlblty and data drblty

Core Domponents of Amazon DynamoDB- In DynamoDB, tables, items and attrbutes are the core compnnts that you wrk with. A table is a cllction of items and each item is a cllction of attrbutes. DynamoDB uses prmary keys to uniquely ID each item in a table and secondary indxes to prvde more querying flxblity

Basic DynamoDB components:
  *Tables- Simllar to other databse systms, DynamoDB stres data in tables. A table is a cllction of data. For ex: see the ex table called People that you could use to sotre persnal contct info about friends, family, or anyone else of intrest. Could also have a Cars table to store info about vehicles that people drive

  *Items- Each table contains zero or more items, An item is a group of attrbutes that is unquely idntfble among all other itms. I a People table, each item reps a person. For a Cars table, each item reps one vehcle. Items in DynamoDB are simlar in many ways to rows, records, or tuples in other database systms. In DynamoDB, there is no limit to the num of items you can store in a table.

  *Attributes-Each item is compsed of one or more attrbutes. An attrbute is a fundmntal data elment, somthing that does not need to be broken down any further. For ex. an item in a People table contains attrbtes called PersonID, LastName, FirstName, and so on. For a Department table, an item might have attrbutes such as DepartmentID, Name, Manager, and so on. Attributes in DynamoDB are similar in many ways to fields or columns in other database systems

  Security with Amazon DynamoDB- also offers encrption at rest, which elimntes the oprtional butden and complxity involved in prtcting senstive data. See "DynamoDB Encryption at Rest"

  External Resource: Introduction to Amazon DynamoDB

Choose the Right AWS Database Service- AWS Database Services
AWS has a variety of diff database options for diff use cases. Use the table below to get a quick look at the AWS database portfolio.

1. Database Type: Relational

Use Cases: Traditional applications, ERP, CRM, e-commerce

AWS Service: Amazon RDS, Amazon Aurora, Amazon Redshift

2. Database Type: Key-value

Use Cases: High-traffic, web apps, e-commerce systems, gaming apps

AWS Service: Amazon DynamoDB

3. Database Type: In-memory

Use Cases: Caching, session mangmt, gaming leaderboards, geospatial apps

AWS Service: Amazon ElastiCache for Memcached, Amazon ElastiCache for Redis

4. Database type: Document

Use Cases: Content mgmt, catalogs, user prfiles

AWS Service: Amazon DocumentDB (with MongoDB compatblty)

5. Database type: Wide Column

Use Cases: High-scale industrial apps for equipmnt maintnce, fleet mgmt, and route optmztion

AWS Service: Amazon Keyspaces (for Apache Cassandra)

6. Database Type: Graph

Use Cases: Fraud detection, social netwrking, recommndation engines

AWS Service: Amazon Neptune

7. Database Type: Time Series

Use Cases: IoT apps, DevOps, industrial telemetry

AWS Service: Amazon Timestream

8. Database Type: Ledger

Use Cases: Systems of record, supply chain, registrtions, banking transactions

AWS Service: Amazon QLDB

Breaking up Applications and Databases- As the industry changes, apps and databases change too. Today, with larger apps you no longer see just one database spprting it. Instead, these apps are being broken into smaller servces, each w/ their own purpose-built database spprting it. 

This shift frmoves the idea of a one-size-fits-all database and replces it w/ a complmntry database strtgy. You can give each database the apprpriate fnctnality, prfrmnce, and scale that the workload requres.

Resources: https://aws.amazon.com/products/databases/

https://aws.amazon.com/blogs/database/?nc=sn&loc=4

https://aws.amazon.com/solutions/


# Monitoring on AWS- 

  *How many people are visiting my site day to day?
  *How can I track the number of visitors over time?
  *How will I know if the website is having prfrmnce or avlblty issues?
  *What happens if my Amazon Elastic Compute Cloud (EC2) instance runs out of capacity?
  *Will I be alerted if my website goes down?

Need a way to cllct and anlze dataabout the oprtional health and usage of your rsrcs. The act of cllctng, anlzng, and using data to make decsions or answer questns about your IT rsrcs and systms is called montring. 
Enables you to have a near real-time pulse on your system and answer questions above. Can use the data you cllct to watch for oprtional issues caused by evnts like over-utilztion ooooof rsrcs, applcation flaws, rsrc misconfigrtn, or secrty-related events. Think of the data cllcted through montring as outputs of the system, or metrics.

Use Metrics to Solve Problems-
The rsrcs that host your soltns on AWS all create various frms of data that you might be intrsted in cllctng. You can think of each indvdl data point that is created by a rsrc as a metric. Metrics that are cllcted and anlzed over time become stats, like the ex of average CPU utilztion over time below, showing a spike at 1:30. Consider this: one way to evalte the health of an Amazon EC2 instnce is through CPU utlztion. Genrlly spking, if an EC2 instnce has a high CPU utlztion, it can mean a flood of rqsts. Or it can rflct a prcss that has encntred an error and is consming too much of the CPU. 
When anlzing CPY ytlztion, take a process that exceeds a spcfc threshold for an unusl length of time. Use that abnormal event as a cue to either manlly or autmtclly reslve the issue through actions like scaling th instnce. This is one ex of a metric. Other ex's of metrics EC2 instnces have are netwrk utlztion, disk prfrmnce, memry utlztion, and the logs created by the apps rnning on top of EC2. 

Know the Different Types of Metrics-Diffrnt rsrcs in AWS create diffrnt types of metrcs. An Amazon Simple Storage Service (S3) bucket would not have CPU utlztion like an EC2 instnce does. Instead, S3 creates metrics reltd to the objcts stored in a bucket like the overall size, or the number of objcts in a bucket. S3 also has metrcs reltd to the rqsts made to the buckt such as reading or wrting objcts. Amazon Relation Database Servic (RDS) creates metrics such as database cnnctions, CPU utlztion of an instnce, or disk space consmption. Not a complete list but can see how diffrnt rsrcs create diff metrics. Could be intrsted in a wide varty of metrcs dpnding on the types of rsrcs you are using, the goals you have, or the types of questns you want answered.

Understand the Benefits of Monitoring

Monitring gives you visblty into your rsrcs, but the question now is, "Why is that imprtnt?"- Some benefits of montring...

Respond to operational issues procatvely b4 your end users are aware- It's bad practice to wait for end users to let you knwo your app is exprncing an outage. Through montring, can keep tabs on metrcs like error respnse rate or rqust latency, over time, that help signal that an outage is going to occur. This enables you to autmtclly or manlly perform actions to prevnt the outage from happneing- fising the problem before your end users are aware of it. 

Improve the Performance and reliability of your resrces- Montring the diff rsrcs that comprse your app prvdes you w/ a full pic of how your soltion behaves as a system. Montring, if done well, can illmnte bottlncks and ineffcient archtctres. Enable you to drive prfrmnce and relblty imprvmnt prcsses.

Recognize scrty threats and events. When you monitor rsrcs, evnts, and systms over time, you create what is called a baseline. A baseline dfnes what actvty is normal. Using a baseline, you can spot anomalies like unusu trffic spikes or unusu IP addrsses accssing your rsrcs. When an anomaly occrs, an alert can be sent out or an action can be taken to insvtgte the event.

Make data-driven decsions for your business. Monitring is not only to keep an eye on IT oprtnal healt. It also helps drive business decsions. For ex, say you laundched a new feature for your cat photo app, and want to know whether it's being used. Can cllect applction-level metrcs and view the number of users who use the new feature. With your findings, you decide whether to invest more time into imprving the new feature. 

Create more cost-effctive soltions- Through montring, you can view rsrcs that are being underutlzed and rightsize your rsrcs to your usage This helps you optmze cost and make sur your'e not spending more money than needed. 

Enable Visibility- AWS resrcs create data you can montor through metrics, logs, netwrk trffic, events, and more. This data is coming form compnnts that are distrbted in nature, which can elad to diffclty in cllcting the data you need if you don't avhae a centrlzed plce to review it all. AWS has already done that for you w/ a service called Amazon CloudWatch. 
Amazon CloudWatch is amontring and obsrvblty srvce that cllcts data like those mentioned in this module. CloudWatch prvides actionable insghts into your apps, and enables you to respnd to system-wide prfrmnce cahnges, optmize rsrc utlztion, and get a unified view of oprtional health. This unified view is imprtnt, YOu can use CloudWatch to:
  *Detect anomalous vehavior in your envrnmnts
  *SEt alrms to alert you when something's not right.
  *Visulze logs and metrcs withe the AWS Mangmnt Console
  *Take autmted actions like scaling
  *Troubleshoot issues.

  Resource:

External Site:
 AWS: Amazon CloudWatch




