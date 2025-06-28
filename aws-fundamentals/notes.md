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

_These notes will be updated continuously as I progress._
