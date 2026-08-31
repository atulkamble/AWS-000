# AWS Introduction

A good **first AWS session** should focus on cloud fundamentals, AWS global infrastructure, account basics, IAM, EC2, networking, storage, and a simple hands-on web-server deployment.

## 1. What is Cloud Computing?

**Cloud computing** means using IT resources such as servers, storage, databases, networking, and software over the internet instead of purchasing and maintaining physical infrastructure.

```text
Traditional Infrastructure

User
  |
  v
Company Data Center
  |
  +-- Physical Servers
  +-- Storage
  +-- Networking
  +-- Database
  +-- Security
```

```text
Cloud Infrastructure

User
  |
  | Internet
  v
+-----------------------+
|         AWS           |
+-----------------------+
| EC2       -> Servers  |
| S3        -> Storage  |
| RDS       -> Database |
| VPC       -> Network  |
| IAM       -> Security |
+-----------------------+
```

### Why Cloud?

* No need to purchase physical servers
* Pay only for resources you consume
* Resources can be created quickly
* Easy scalability
* Global infrastructure
* High availability
* Backup and disaster-recovery options
* Automation using CLI, APIs, IaC and DevOps tools

---

# 2. What is AWS?

Amazon Web Services (AWS) is a cloud computing platform that provides infrastructure and managed services over the internet.

[AWS official website](https://aws.amazon.com/?utm_source=chatgpt.com)

```text
                 AWS
                  |
      +-----------+-----------+
      |           |           |
    Compute     Storage    Database
      |           |           |
     EC2          S3          RDS
      |
      +---------- Networking
      |              |
      |             VPC
      |
      +---------- Security
                     |
                    IAM
```

### Important AWS Services

| Category       | Service        | Purpose                           |
| -------------- | -------------- | --------------------------------- |
| Compute        | EC2            | Virtual machines                  |
| Storage        | S3             | Object storage                    |
| Database       | RDS            | Managed relational databases      |
| Networking     | VPC            | Virtual network                   |
| Security       | IAM            | Users, roles and permissions      |
| DNS            | Route 53       | DNS service                       |
| Load Balancing | ELB            | Distribute traffic                |
| Monitoring     | CloudWatch     | Metrics, logs and alarms          |
| Serverless     | Lambda         | Run code without managing servers |
| Containers     | ECS / EKS      | Container orchestration           |
| IaC            | CloudFormation | Infrastructure as Code            |

---

# 3. Cloud Service Models

Three fundamental models:

```text
                  Cloud Services
                       |
          +------------+------------+
          |            |            |
         IaaS         PaaS         SaaS
          |            |            |
     Infrastructure  Platform     Software
          |            |            |
         EC2       App Platform    Gmail
```

### IaaS — Infrastructure as a Service

AWS provides infrastructure; we manage the OS and applications.

Example:

```text
EC2
 |
 +-- CPU
 +-- RAM
 +-- Disk
 +-- Network
 +-- Operating System
```

### PaaS — Platform as a Service

Developer focuses primarily on application/code while much of the underlying infrastructure is managed.

Examples include managed application platforms.

### SaaS — Software as a Service

Ready-to-use software delivered over the internet.

Examples:

```text
Gmail
Microsoft 365
Zoom
Salesforce
```

---

# 4. Cloud Deployment Models

```text
                 Cloud
                   |
       +-----------+-----------+
       |           |           |
     Public      Private      Hybrid
      Cloud       Cloud        Cloud
```

### Public Cloud

Infrastructure is operated by a cloud provider.

Examples:

```text
AWS
Microsoft Azure
Google Cloud
```

### Private Cloud

Cloud infrastructure dedicated to a single organization.

### Hybrid Cloud

Combination of:

```text
On-Premises
     |
     | VPN / Dedicated Connection
     |
     v
   Cloud
```

---

# 5. Traditional Data Center vs AWS

```text
Traditional

Company
   |
   v
Purchase Server
   |
   v
Install Hardware
   |
   v
Install OS
   |
   v
Configure Network
   |
   v
Deploy Application
```

AWS:

```text
AWS Account
    |
    v
Select Service
    |
    v
Configure Resource
    |
    v
Create
    |
    v
Resource Available
```

Cloud provisioning can often reduce infrastructure provisioning from weeks or days to minutes, depending on the resource and organizational controls.

---

# 6. CapEx vs OpEx

### CapEx — Capital Expenditure

Upfront infrastructure investment.

```text
Buy Server
   +
Buy Storage
   +
Networking
   +
Data Center
   +
Maintenance
```

### OpEx — Operational Expenditure

Pay for services as they are consumed.

```text
Use AWS Resource
       |
       v
Usage / Pricing Model
       |
       v
AWS Bill
```

---

# 7. AWS Global Infrastructure

One of the most important first-session concepts:

```text
                 AWS Global Infrastructure
                           |
              +------------+------------+
              |                         |
            Region               Edge Locations
              |
       +------+------+
       |      |      |
      AZ-1   AZ-2   AZ-3
```

### Region

A **Region** is a geographic area where AWS operates infrastructure.

Examples:

```text
us-east-1
US East (N. Virginia)

ap-south-1
Asia Pacific (Mumbai)

ap-south-2
Asia Pacific (Hyderabad)
```

### Availability Zone — AZ

A Region contains multiple Availability Zones.

```text
AWS Region
ap-south-1
     |
 +---+---+---+
 |       |   |
AZ-A   AZ-B AZ-C
 |       |   |
DC      DC   DC
```

Deploying across multiple AZs is a common way to design for higher availability.

### Edge Location

Edge locations help deliver content and certain AWS services closer to users.

A common example is CloudFront.

```text
User
 |
 v
Nearest Edge Location
 |
 v
CloudFront
 |
 v
Origin
```

---

# 8. AWS Account

Typical learning flow:

```text
AWS Account
    |
    +-- Root User
    |
    +-- IAM
    |    |
    |    +-- Users
    |    +-- Groups
    |    +-- Roles
    |    +-- Policies
    |
    +-- AWS Services
```

### Root User

The root user is created when the AWS account is created and has broad account-level access.

Best practice:

```text
Root User
   |
   +-- Enable MFA
   +-- Don't use for daily work
   +-- Protect credentials
```

---

# 9. IAM — Identity and Access Management

IAM controls **who can access AWS and what they are allowed to do**.

```text
                  IAM
                   |
       +-----------+-----------+
       |           |           |
     Users       Groups       Roles
       |           |           |
       +-----------+-----------+
                   |
                Policies
                   |
              Permissions
```

### Example

```text
User: student
       |
       v
Group: developers
       |
       v
Policy
       |
       v
EC2 Permissions
```

Basic terms:

| Component | Purpose                                             |
| --------- | --------------------------------------------------- |
| User      | Identity for a person/application where appropriate |
| Group     | Collection of IAM users                             |
| Policy    | Permission document                                 |
| Role      | Assumable identity with permissions                 |
| MFA       | Additional authentication factor                    |

---

# 10. Shared Responsibility Model

AWS security responsibilities are shared between AWS and the customer.

```text
+--------------------------------+
|          CUSTOMER              |
| Security IN the Cloud          |
|                                |
| Data                           |
| IAM configuration              |
| Applications                   |
| OS configuration*              |
| Network configuration          |
+--------------------------------+
              |
+--------------------------------+
|             AWS                |
| Security OF the Cloud          |
|                                |
| Physical facilities            |
| Hardware                       |
| Core infrastructure            |
| Managed cloud foundation       |
+--------------------------------+

*Responsibility varies by service.
```

This distinction changes depending on whether you're using EC2, RDS, Lambda, S3, etc.

---

# 11. EC2 — Elastic Compute Cloud

**Amazon EC2** provides virtual compute instances.

Think of it as:

```text
Physical Computer
       |
       v
Virtualization
       |
       v
+----------------+
| EC2 Instance   |
+----------------+
| CPU            |
| RAM            |
| Storage        |
| Network        |
| OS             |
+----------------+
```

Example EC2 configuration:

```text
Name       : webserver
OS         : Amazon Linux
Type       : t3.micro
Storage    : EBS
Network    : VPC
Public IP  : Enabled
```

---

# 12. AMI — Amazon Machine Image

AMI provides the software image used to launch an EC2 instance.

```text
AMI
 |
 +-- Operating System
 |
 +-- Configuration / software
 |
 v
EC2 Instance
```

Examples include:

```text
Amazon Linux
Ubuntu
Red Hat Enterprise Linux
Windows Server
```

---

# 13. EC2 Instance Types

Instance families are optimized for different workloads.

```text
EC2 Instance Types
        |
 +------+------+-------+
 |      |      |       |
General Compute Memory Accelerated
Purpose Optimized Optimized Computing
```

Examples:

```text
T family -> Burstable/general workloads
M family -> General purpose
C family -> Compute optimized
R family -> Memory optimized
G/P      -> Accelerated computing
```

---

# 14. VPC — Virtual Private Cloud

A VPC is a logically isolated virtual network in AWS.

```text
AWS
 |
 v
+----------------------------------+
| VPC                              |
|                                  |
|  +------------+  +------------+  |
|  | Subnet A   |  | Subnet B   |  |
|  |            |  |            |  |
|  | EC2        |  | Database   |  |
|  +------------+  +------------+  |
|                                  |
+----------------------------------+
```

Networking concepts students should know:

```text
VPC
 |
 +-- CIDR
 +-- Subnet
 +-- Route Table
 +-- Internet Gateway
 +-- Security Group
 +-- Network ACL
```

---

# 15. Public and Private Subnets

```text
                    Internet
                       |
                       v
                Internet Gateway
                       |
               +-------+-------+
               |      VPC      |
               |               |
        +------+-----+   +-----+------+
        | Public     |   | Private    |
        | Subnet     |   | Subnet     |
        |            |   |            |
        | Web Server |   | Database   |
        +------------+   +------------+
```

A public subnet normally has routing to an Internet Gateway. A private subnet does not directly route to the Internet Gateway.

---

# 16. Security Group

A Security Group acts as a **stateful virtual firewall** for resources such as EC2 network interfaces.

Example:

```text
Internet
   |
   | HTTP : 80
   | HTTPS: 443
   | SSH  : 22
   v
+----------------+
| Security Group |
+----------------+
        |
        v
+----------------+
| EC2 Web Server |
+----------------+
```

Common ports:

| Service    | Port |
| ---------- | ---: |
| SSH        |   22 |
| HTTP       |   80 |
| HTTPS      |  443 |
| RDP        | 3389 |
| MySQL      | 3306 |
| PostgreSQL | 5432 |

---

# 17. Storage Services

```text
              AWS Storage
                   |
        +----------+----------+
        |          |          |
       S3         EBS        EFS
        |          |          |
      Object      Block      File
     Storage     Storage    Storage
```

### S3

Amazon Simple Storage Service provides object storage.

```text
S3
 |
 v
Bucket
 |
 +-- image.jpg
 +-- index.html
 +-- backup.zip
 +-- report.pdf
```

### EBS

Block storage commonly attached to EC2.

```text
EC2
 |
 v
EBS Volume
 |
 +-- OS
 +-- Applications
 +-- Data
```

### EFS

Managed shared file storage.

```text
        EFS
       / | \
      /  |  \
    EC2 EC2 EC2
```

---

# 18. Database Services

```text
AWS Databases
     |
     +-- RDS
     |
     +-- DynamoDB
     |
     +-- Aurora
```

### RDS

Managed relational database service supporting engines such as MySQL, PostgreSQL and SQL Server.

```text
Application
     |
     v
    RDS
     |
 +---+---------+
 |             |
MySQL      PostgreSQL
```

### DynamoDB

Managed NoSQL database.

---

# 19. Basic Three-Tier AWS Architecture

A useful diagram to introduce students to real-world architecture:

```text
                     Internet
                        |
                        v
                  Load Balancer
                        |
              +---------+---------+
              |                   |
           Web/App             Web/App
            EC2                  EC2
              |                   |
              +---------+---------+
                        |
                        v
                       RDS
                    Database
```

A more realistic network layout:

```text
+------------------------------------------------+
| VPC                                            |
|                                                |
|  Public Subnets                               |
|  +-------------+       +-------------+         |
|  | Load        |       | Load        |         |
|  | Balancer    |       | Balancer    |         |
|  +-------------+       +-------------+         |
|                                                |
|  Private Application Subnets                  |
|  +-------------+       +-------------+         |
|  | App / EC2   |       | App / EC2   |         |
|  +-------------+       +-------------+         |
|                                                |
|  Private Database Subnets                     |
|          +--------------------+                |
|          | RDS Database       |                |
|          +--------------------+                |
+------------------------------------------------+
```

---

# 20. AWS Management Methods

There are several ways to interact with AWS:

```text
                 AWS
                  |
       +----------+----------+
       |          |          |
    Console      CLI        SDK/API
       |          |          |
     Browser    Terminal    Program
```

Later, DevOps students can add Infrastructure as Code:

```text
Developer
   |
   +-- AWS CLI
   |
   +-- CloudFormation
   |
   +-- Terraform
   |
   v
  AWS
```

---

# 21. First Hands-On Lab — Launch EC2

### Objective

Create a Linux EC2 instance and connect using SSH.

```text
Laptop
  |
  | SSH : 22
  v
Internet
  |
  v
Security Group
  |
  v
EC2
Amazon Linux
```

### Configuration

```text
AWS Console
   |
   v
EC2
   |
   v
Instances
   |
   v
Launch Instance
```

Use:

```text
Name        : server
AMI         : Amazon Linux
Type        : t3.micro
Key Pair    : key.pem
VPC         : Default
Public IP   : Enabled

Security Group:
SSH         : 22
HTTP        : 80
HTTPS       : 443

Storage     : Default
```

---

# 22. Connect to EC2

Navigate to the directory containing the key:

```bash
cd Downloads
```

Linux/macOS:

```bash
chmod 400 key.pem
```

Connect:

```bash
ssh -i "key.pem" ec2-user@<PUBLIC-IP>
```

Example architecture:

```text
Student Laptop
     |
     | key.pem
     |
     | SSH : 22
     v
+----------------+
| EC2            |
| Amazon Linux   |
+----------------+
```

---

# 23. Basic Linux Commands

After connecting:

```bash
whoami
hostname
pwd
date
uname
uname -a
cat /etc/os-release
lscpu
free -h
df -h
```

Update packages:

```bash
sudo dnf update -y
```

---

# 24. Install Apache Web Server

```bash
sudo dnf install httpd -y

sudo systemctl start httpd

sudo systemctl enable httpd

sudo systemctl status httpd
```

Architecture:

```text
Browser
   |
   | HTTP : 80
   v
Security Group
   |
   v
EC2
   |
   v
Apache HTTP Server
   |
   v
index.html
```

---

# 25. Create First Website

```bash
cd /var/www/html

sudo nano index.html
```

Add:

```html
<h1>Hello AWS</h1>
<h2>My First AWS EC2 Web Server</h2>
```

Open:

```text
http://<EC2-PUBLIC-IP>
```

Flow:

```text
Student Browser
      |
      | HTTP : 80
      v
   Internet
      |
      v
Security Group
      |
      v
EC2 Public IP
      |
      v
Apache : 80
      |
      v
index.html
      |
      v
Hello AWS
```

---

# 26. Complete First-Session Architecture

```text
                        AWS Cloud
+------------------------------------------------------+
|                                                      |
|                     Region                           |
|                                                      |
|   +------------------------------------------------+ |
|   | VPC                                            | |
|   |                                                | |
|   |      Public Subnet                             | |
|   |                                                | |
|   |      +----------------------+                  | |
|   |      | Security Group       |                  | |
|   |      | 22  - SSH            |                  | |
|   |      | 80  - HTTP           |                  | |
|   |      | 443 - HTTPS          |                  | |
|   |      +----------+-----------+                  | |
|   |                 |                              | |
|   |                 v                              | |
|   |      +----------------------+                  | |
|   |      | EC2                  |                  | |
|   |      | Amazon Linux         |                  | |
|   |      | Apache HTTP Server   |                  | |
|   |      | index.html           |                  | |
|   |      +----------+-----------+                  | |
|   |                 |                              | |
|   |                EBS                             | |
|   +------------------------------------------------+ |
+------------------------------------------------------+
                         ^
                         |
                    Internet
                         |
                 +-------+-------+
                 | Student       |
                 | Laptop        |
                 +---------------+
```

# 27. AWS + DevOps Introduction

Since this is the foundation for AWS DevOps training, finish the first session by showing where DevOps fits.

```text
Developer
    |
    v
   Git
    |
    v
 GitHub
    |
    v
 Jenkins / CI-CD
    |
    v
 Docker
    |
    v
 Kubernetes / EKS
    |
    v
 AWS Infrastructure
```

Infrastructure automation:

```text
Terraform
    |
    v
AWS
 |
 +-- VPC
 +-- EC2
 +-- S3
 +-- RDS
 +-- EKS
```

Monitoring:

```text
Application
     |
     v
AWS Infrastructure
     |
     v
CloudWatch
     |
     +-- Metrics
     +-- Logs
     +-- Alarms
```

## Recommended 2-Hour First Session Flow

| Time        | Topic                               |
| ----------- | ----------------------------------- |
| 0–15 min    | Cloud Computing introduction        |
| 15–25 min   | IaaS, PaaS, SaaS                    |
| 25–35 min   | Public, Private & Hybrid Cloud      |
| 35–50 min   | AWS introduction & major services   |
| 50–65 min   | Regions, AZs & Edge Locations       |
| 65–80 min   | AWS Account, IAM & Security         |
| 80–95 min   | EC2, AMI, instance types, EBS       |
| 95–105 min  | VPC, subnet & Security Group        |
| 105–115 min | Launch EC2 + SSH                    |
| 115–120 min | Apache website + AWS/DevOps roadmap |

**Student outcome:** By the end of Session 1, students should understand basic cloud terminology, AWS infrastructure and core services, and should be able to explain and deploy the simple path **Internet → Security Group → EC2 → Apache → Website**.
