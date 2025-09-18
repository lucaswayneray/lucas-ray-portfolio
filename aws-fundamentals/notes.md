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

 8. Permissions- Vergy the prmssions and roles attched to your EC2 instnce. Ensre the instnce has the necssr IAM roles and polcies to access any requred AWS services, such as S3, DynamoDB, or RDS

 9. Personal network permissions- Ensre that your persnal or coprrate netwrk does not have restrctions blocking access to the public IP address of your EC2 instnce. Some ntwrks might have frewlls or prxy settngs that could block outbound trffic to certain IP ranges or ports.

 10. Application- ensure that your app code is crrctly deplyed and running. Check the application's logs to diagnose any runtime errors. Also, make sure the web server (e.g., Apache, Nginx) is installed and rnning.

 