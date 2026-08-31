For students starting **AWS + DevOps**, I’d cover these prerequisites before going deeper into EC2, VPC, Docker, Kubernetes, and CI/CD.

# Basic OS, Linux & Networking Concepts for AWS/DevOps

## 1. Operating System Basics

An **Operating System (OS)** is system software that manages hardware resources and provides an environment where applications can run.

```text
User
  |
  v
Applications
  |
  v
Operating System
  |
  +-- CPU
  +-- RAM
  +-- Disk
  +-- Network
  |
  v
Hardware
```

### Common Operating Systems

```text
Operating Systems
       |
  +----+----------------+
  |                     |
Windows                Linux
  |                     |
Windows 10/11          Ubuntu
Windows Server         RHEL
                      Amazon Linux
                      Fedora
                      SUSE
```

For AWS/DevOps, students should be comfortable with **Linux server operating systems**.

---

# 2. Hardware Basics

Before understanding cloud VMs, know these components:

| Component  | Meaning                            | Example              |
| ---------- | ---------------------------------- | -------------------- |
| CPU        | Processes instructions             | 2 vCPU               |
| RAM        | Temporary working memory           | 4 GB                 |
| Disk       | Persistent storage                 | 30 GB SSD            |
| NIC        | Network interface                  | Ethernet/virtual NIC |
| IP Address | Network address                    | `192.168.1.10`       |
| OS         | Controls system                    | Linux                |
| Process    | Running program                    | Apache               |
| Port       | Application communication endpoint | 80                   |

In AWS:

```text
Physical Server
      |
 Virtualization
      |
      v
+------------------+
| EC2 Instance     |
|------------------|
| vCPU             |
| RAM              |
| EBS Disk         |
| Network          |
| Linux / Windows  |
+------------------+
```

---

# 3. Physical Server vs Virtual Machine

### Physical Server

Actual hardware installed in a data center.

```text
Physical Server
 |
 +-- CPU
 +-- RAM
 +-- SSD
 +-- NIC
 +-- Operating System
```

### Virtual Machine

Software-defined computer running on virtualized infrastructure.

```text
Physical Server
      |
      v
Hypervisor
      |
 +----+----+----+
 |         |    |
VM1       VM2  VM3
Linux   Windows Linux
```

In AWS:

```text
Virtual Machine
      =
EC2 Instance
```

---

# 4. Client and Server

This is one of the most important concepts.

A **client** requests a service.

A **server** provides the service.

```text
Client                         Server
Laptop                         EC2
  |                             |
  |------ HTTP Request -------->|
  |                             |
  |<----- HTTP Response --------|
```

Example:

```text
Chrome Browser
      |
      | HTTP : 80
      v
Apache Web Server
```

---

# 5. Linux Basics

Linux is an open-source Unix-like operating system widely used for cloud servers, containers, DevOps tooling, and infrastructure.

Linux was created by **Linus Torvalds** starting in 1991.

```text
Linux
 |
 +-- Open Source
 +-- Multi-user
 +-- Multi-tasking
 +-- Secure permissions
 +-- Strong networking
 +-- CLI friendly
 +-- Automation friendly
```

---

# 6. Linux Distributions

Linux has many distributions.

```text
Linux
 |
 +-- Debian Family
 |      |
 |      +-- Debian
 |      +-- Ubuntu
 |
 +-- Red Hat Family
 |      |
 |      +-- RHEL
 |      +-- Fedora
 |
 +-- Amazon Linux
 |
 +-- SUSE
```

For AWS training, focus primarily on:

```text
Amazon Linux
Ubuntu
RHEL
```

---

# 7. Linux Package Managers

Package managers install and manage software.

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install apache2 -y
```

### Amazon Linux / RHEL family

```bash
sudo dnf update -y
sudo dnf install httpd -y
```

Older systems may also use:

```bash
yum
```

Basic relationship:

```text
Linux Distribution
       |
       +-- Ubuntu ------> apt
       |
       +-- RHEL --------> dnf
       |
       +-- Amazon Linux -> dnf
```

---

# 8. Linux Shell

A **shell** interprets commands entered by a user.

```text
User
 |
 v
Terminal
 |
 v
Shell
 |
 v
Linux Kernel
 |
 v
Hardware
```

Common shells:

```text
sh
bash
zsh
```

Check your shell:

```bash
echo $SHELL
```

---

# 9. Linux File System

Unlike Windows drive letters such as `C:`, Linux starts from:

```text
/
```

Important directories:

```text
/
|
+-- home
|    |
|    +-- ec2-user
|
+-- root
|
+-- etc
|
+-- var
|    |
|    +-- log
|    +-- www
|
+-- usr
|
+-- tmp
|
+-- opt
```

Students should know:

| Directory  | Purpose                   |
| ---------- | ------------------------- |
| `/`        | Root filesystem           |
| `/home`    | User home directories     |
| `/root`    | Root user's home          |
| `/etc`     | Configuration             |
| `/var`     | Variable application data |
| `/var/log` | Logs                      |
| `/tmp`     | Temporary files           |
| `/opt`     | Optional applications     |
| `/usr`     | Programs/libraries        |

---

# 10. Essential Linux Commands

### Navigation

```bash
pwd
ls
ls -l
ls -la
cd /etc
cd ..
cd ~
```

### Files

```bash
touch file.txt
cat file.txt
nano file.txt
cp file.txt backup.txt
mv file.txt newfile.txt
rm file.txt
```

### Directories

```bash
mkdir project
cd project
rmdir project
rm -rf project
```

### System information

```bash
whoami
hostname
uname
uname -a
cat /etc/os-release

lscpu
free -h
df -h
uptime
date
```

---

# 11. Linux Users

Linux is a **multi-user operating system**.

```text
Linux
 |
 +-- root
 |
 +-- ec2-user
 |
 +-- ubuntu
 |
 +-- developer
 |
 +-- webadmin
```

`root` is the administrative/superuser account.

Commands:

```bash
whoami

id

sudo useradd developer

sudo passwd developer

id developer
```

---

# 12. Linux Permissions

Linux permissions:

```text
r = Read
w = Write
x = Execute
```

Numeric values:

```text
r = 4
w = 2
x = 1

rwx = 7
rw- = 6
r-x = 5
```

Example:

```text
rwxr-xr-x

User   = rwx = 7
Group  = r-x = 5
Others = r-x = 5

755
```

Commands:

```bash
ls -l

chmod 755 deploy.sh

chmod +x deploy.sh
```

This becomes particularly important when working with scripts, SSH keys, web servers, Docker, and CI/CD agents.

---

# 13. Process Basics

A **process** is a running program.

```text
Program
   |
   | Execute
   v
Process
```

Examples:

```text
Apache
MySQL
Jenkins
Docker
SSH
```

Commands:

```bash
ps

ps aux

top

kill <PID>
```

---

# 14. Linux Services

Server applications commonly run as services.

```text
Linux
 |
 +-- sshd
 +-- httpd
 +-- docker
 +-- jenkins
```

Using `systemd`:

```bash
sudo systemctl start httpd

sudo systemctl stop httpd

sudo systemctl restart httpd

sudo systemctl status httpd

sudo systemctl enable httpd
```

Difference:

```text
start
  |
Run service NOW

enable
  |
Start service automatically at boot
```

---

# 15. Networking Basics

Networking allows computers and applications to communicate.

Basic model:

```text
Laptop
  |
  | Wi-Fi / Ethernet
  v
Router
  |
  v
Internet
  |
  v
AWS
  |
  v
EC2 Server
```

Students should understand:

```text
IP Address
Subnet
Subnet Mask / CIDR
Gateway
Router
DNS
MAC Address
Protocol
Port
Firewall
Public IP
Private IP
```

---

# 16. What is an IP Address?

An **IP address** identifies a network interface on an IP network.

Example IPv4:

```text
192.168.1.10
```

IPv4 contains 32 bits.

```text
192 . 168 . 1 . 10

 8     8     8    8
bits  bits  bits bits

Total = 32 bits
```

---

# 17. Public IP vs Private IP

### Private IP

Used inside private networks.

Common IPv4 private ranges:

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

Example:

```text
EC2 Private IP

10.0.1.10
```

### Public IP

Used for communication over the public internet when routing and security permit.

```text
Laptop
   |
Internet
   |
Public IP
   |
EC2
   |
Private IP
```

In AWS, this distinction is fundamental to understanding VPC design.

---

# 18. What is a Subnet?

A subnet divides an IP network into smaller networks.

Example:

```text
VPC
10.0.0.0/16
      |
      +------------------+
      |                  |
10.0.1.0/24          10.0.2.0/24
Public Subnet        Private Subnet
      |                  |
     EC2                Database
```

---

# 19. CIDR Basics

Example:

```text
192.168.1.0/24
```

`/24` indicates that the first 24 bits are the network prefix.

Common introductory examples:

| CIDR  | Total IPv4 addresses |
| ----- | -------------------: |
| `/16` |               65,536 |
| `/24` |                  256 |
| `/25` |                  128 |
| `/26` |                   64 |
| `/27` |                   32 |
| `/28` |                   16 |

AWS reserves some addresses in each subnet, so **total CIDR addresses and usable AWS addresses are not always the same**.

---

# 20. Gateway

A gateway provides a path from one network toward another.

```text
PC
 |
192.168.1.10
 |
 v
Gateway
192.168.1.1
 |
 v
Internet
```

AWS equivalent concept:

```text
EC2
 |
Subnet
 |
Route Table
 |
Internet Gateway
 |
Internet
```

---

# 21. Router and Routing

A router forwards packets between networks.

```text
Network A
10.0.1.0/24
     |
     v
   Router
     |
     v
Network B
10.0.2.0/24
```

The router uses a **routing table** to determine where traffic should go.

---

# 22. DNS

DNS stands for **Domain Name System**.

Humans prefer:

```text
amazon.com
```

Computers communicate using IP addresses.

Conceptually:

```text
User
 |
 | amazon.com
 v
DNS Server
 |
 | IP Address
 v
User
 |
 v
Web Server
```

AWS DNS service:

```text
Amazon Route 53
```

---

# 23. Ports

An IP identifies the machine/network interface.

A **port** identifies a network service/application endpoint.

```text
Server IP
10.0.1.10
     |
     +-- 22   SSH
     +-- 80   HTTP
     +-- 443  HTTPS
     +-- 3306 MySQL
```

Important ports:

| Service    | Port |
| ---------- | ---: |
| SSH        |   22 |
| HTTP       |   80 |
| HTTPS      |  443 |
| DNS        |   53 |
| RDP        | 3389 |
| MySQL      | 3306 |
| PostgreSQL | 5432 |
| Jenkins    | 8080 |

---

# 24. Protocol Basics

A protocol defines rules for communication.

Important protocols:

```text
TCP
UDP
IP
HTTP
HTTPS
SSH
DNS
```

### TCP

Connection-oriented and reliable transport.

Examples:

```text
SSH
HTTP/HTTPS
```

### UDP

Connectionless transport with lower overhead.

Commonly used by services such as DNS, though DNS can use both UDP and TCP.

---

# 25. HTTP and HTTPS

HTTP:

```text
Browser
   |
   | HTTP : 80
   v
Web Server
```

HTTPS:

```text
Browser
   |
   | HTTPS : 443
   | TLS Encryption
   v
Web Server
```

---

# 26. SSH

SSH stands for **Secure Shell**.

It is commonly used for remote Linux administration.

```text
Laptop
 |
 | SSH
 | TCP 22
 |
 v
Linux Server
```

Example:

```bash
ssh ec2-user@<IP>
```

With EC2 key:

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

---

# 27. Firewall Basics

A firewall controls allowed and denied network traffic.

```text
Internet
   |
   v
Firewall
   |
   | Allow 80
   | Allow 443
   | Restricted 22
   v
Web Server
```

In AWS, students will quickly encounter:

```text
Security Groups
Network ACLs
```

---

# 28. Basic Networking Commands

Linux:

```bash
ip addr

ip route

hostname

hostname -I

ping google.com

curl google.com

ss -tulnp
```

DNS:

```bash
nslookup google.com
```

or:

```bash
dig google.com
```

Route/path troubleshooting:

```bash
traceroute google.com
```

Some utilities may need to be installed depending on the Linux distribution.

---

# 29. How a Website Actually Works

This diagram ties OS + Linux + networking + AWS together.

```text
User
 |
 | Enter:
 | www.example.com
 |
 v
DNS
 |
 | Resolve Domain
 v
Public IP
 |
 v
Internet
 |
 v
Firewall / Security Group
 |
 | TCP 443
 v
Linux Server
 |
 v
Apache / Nginx
 |
 v
Application
 |
 v
Database
 |
 v
Response
 |
 v
User Browser
```

Students who understand this flow will find **VPC, EC2, Load Balancers, Route 53, Docker and Kubernetes networking** much easier.

# 30. Connect These Concepts to AWS

```text
BASIC CONCEPT                 AWS

Physical Server
      |
      +---------------------> AWS Infrastructure

Virtual Machine
      |
      +---------------------> EC2

Disk
      |
      +---------------------> EBS

Network
      |
      +---------------------> VPC

Network Range
      |
      +---------------------> CIDR

Smaller Network
      |
      +---------------------> Subnet

Firewall
      |
      +---------------------> Security Group / NACL

Router / Routing
      |
      +---------------------> Route Table

Internet Gateway
      |
      +---------------------> IGW

DNS
      |
      +---------------------> Route 53

Load Distribution
      |
      +---------------------> ELB

Linux Server
      |
      +---------------------> EC2 Linux

Shared Files
      |
      +---------------------> EFS

Object Storage
      |
      +---------------------> S3
```

## Minimum Prerequisites Before Starting AWS

For a beginner batch, students don't need to master networking or Linux first. They should at least understand **OS → CPU/RAM/Disk → Linux → files/directories → users/permissions → processes/services → client/server → IP → public/private IP → subnet/CIDR → gateway → DNS → ports/protocols → firewall → SSH**.

Then start AWS in this sequence:

```text
Computer/OS Basics
        |
        v
Linux Basics
        |
        v
Networking Basics
        |
        v
Cloud Computing
        |
        v
AWS Global Infrastructure
        |
        v
IAM
        |
        v
EC2
        |
        v
EBS
        |
        v
VPC
        |
        v
S3 / RDS
        |
        v
AWS + DevOps
```

This gives students enough foundation to understand **why** AWS resources are configured the way they are, instead of simply memorizing console steps.
