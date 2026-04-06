# Project 2 — Cloud Computing & AWS Infrastructure Lab
**Course:** CMIT 495 — Cybersecurity Technology Capstone | UMGC  
**Author:** Brandy Haynes  

---

## Overview

This hands-on lab covers launching a Windows VM on AWS EC2, provisioning an Ubuntu Linux server via SSH, creating and mounting an Amazon EFS network file system, creating an S3 bucket, IP subnetting calculations, and a full comparative analysis of AWS, Google Cloud, and Microsoft Azure.

---

## Lab 1 — Launching a Windows Virtual Machine on AWS EC2

### Step-by-Step: Microsoft Windows Server 2019 on EC2

**Step 1 — Log into AWS Lab Console**
- Navigate to the EC2 Management page
- Click the blue **Launch Instance** button to start the setup wizard

**Step 2 — Configure the Instance**
- **Instance Name:** `Microsoft_Windows_Server`
- **AMI:** Microsoft Windows Server 2019 Base 64-bit (x86)
- **Instance Type:** `t2.micro`
- **Key Pair:** Create New — Name: `Microsoft_Windows_Server`, RSA, .pem format
- Securely save the .pem file

**Step 3 — Create a New VPC**
- Open a duplicate tab and navigate to Create VPC
- Name: `Microsoft_Windows_Server`
- Wait for Running status before returning to instance setup

**Step 4 — Network Settings**
- Select the new VPC from the dropdown
- Refresh subnet to show project VPC subnet
- Enable **Auto-assign public IP**
- **Security Group:** `launch-wizard-1`
- **Inbound Rule:** Type: RDP | Protocol: TCP | Port: 3389 | Source: My IP
- **Configure Storage:** 30 GiB
- Review and **Launch Instance** — wait for Running status

**Step 5 — Connect via RDP**
- From EC2 console, select **Connect → RDP Client**
- Download the remote desktop file
- Copy Public DNS: `ec2-3-230-123-221.compute-1.amazonaws.com`
- Click **Get Password** → upload `.pem` file → **Decrypt Password**
- Open the `.rdp` file and enter credentials
- **Troubleshooting Note:** If RDP connection fails, verify that RDP remote access is enabled on your local computer via PowerShell

---

## Lab 2 — Ubuntu Linux Server & SSH

### Provisioning Ubuntu EC2 and SSH Connection

Following the same steps as Project 1, launched a new Ubuntu EC2 instance and connected via SSH:

```bash
ssh -i "C:\Users\Brandy\Downloads\Ubuntu_Server (1).pem" ubuntu@ec2-44-203-33-170.compute-1.amazonaws.com
```

> **Note:** This IP address changes dynamically if an Elastic IP address is not allocated to the EC2 instance.

---

## Lab 3 — Amazon EFS (Elastic File System)

### Creating and Mounting a Network File System

Created an Amazon EFS network file system and attached it to the running Ubuntu Server instance. Verified the mount and created a test file using the `dd` command to generate a 1 GiB file in the new directory.

### Value of a Network File System

The value of a network file system like Amazon EFS lies within its ability to provide:

- **Secure, scalable, and easily accessible resource management**
- Properly managed storage and data retrieval systems
- A strictly managed Identity and Access Management (IAM) system
- Real-time performance scaling based on current needs
- Consistent high-availability for cloud environments

Being able to easily locate and manage resources and files is imperative for a stable and well-optimized cloud environment.

---

## Lab 4 — Amazon S3 Bucket

Created an S3 bucket and successfully uploaded a file, verified via screenshot in the AWS Console.

---

## Cloud Provider Comparative Analysis

### Recommendation to CTO: AWS for PaaS Needs

**AWS (Amazon Web Services)** is the recommended provider for the organization's Platform as a Service (PaaS) needs.

AWS has emerged as the most established cloud provider with the largest and most extensive global infrastructure, near-unbeatable levels of scalability, and an immense range of services. AWS's ecosystem was designed with all sizes of organizations in mind — from robust security features, scalable pricing models, and flexible integrations across operating systems and programs.

### AWS PaaS Recommendation — Elastic Beanstalk

AWS Elastic Beanstalk offers simplified deployments and management with the following advantages:
- Ease of use
- Automated deployments
- Customization options
- Instant scalability
- Cost efficiency
- Built-in monitoring metrics
- Support for multiple languages
- Seamless platform integrations

---

### Full Cloud Provider Comparison

| Feature | AWS Amazon | GCP Google Cloud | Microsoft Azure |
|---------|-----------|-----------------|-----------------|
| **Pricing** | Pay-as-you-go, per-hour billing, Spot Instances, Reserved Instance discounts | Per-second billing, sustained-use discounts, strong AI/ML cost savings | Free tier 12 months, enterprise pricing, more expensive for non-Microsoft workloads |
| **PaaS Services** | Elastic Beanstalk, Lambda, App Runner | App Engine, Cloud Run, Cloud Functions | Azure App Service, AKS, Azure Functions |
| **Advantages** | Best scalability, strongest security, best integrations, cost-effective | Multi-cloud support, Big Data & AI/ML capabilities, cost optimization | Seamless Microsoft integration, great hybrid cloud, enterprise-friendly |
| **Challenges** | Steep learning curve for new users | Complex IAM management, fewer global data centers | Limited flexibility outside Microsoft ecosystem |
| **Global Reach** | 32 Regions, 102 Availability Zones | 40 Regions, 121 Zones globally | 60+ Regions, 90+ Availability Zones |
| **Compute** | EC2, Lambda, ECS, Fargate | Compute Engine, GKE, Cloud Run | Functions, AKS, Virtual Machines |
| **Database** | DynamoDB, RDS, Aurora | BigQuery, Firestore, Cloud SQL | SQL Server, CosmosDB, PostgreSQL |
| **Security** | Best IAM, most compliance certifications, granular controls | Secure by design, Zero-Trust, AI-driven security | Best for hybrid security & Active Directory integration |
| **Best Uses** | Large-scale apps, microservices, flexibility & scalability | AI/ML apps, Big Data analytics, containerized microservices | Microsoft-based organizations, hybrid cloud, enterprise/government |

---

## IP Subnetting — VPC Network Configuration

### Subnet A — Developers

- **CIDR:** `146.38.70.105/20`
- **Subnet Mask:** `255.255.240.0` (first 20 bits = `11111111.11111111.11110000.00000000`)

**Network Address Calculation:**
```
146.38.70.105  AND  255.255.240.0
10010010.00100110.01000110.01101001
AND
11111111.11111111.11110000.00000000
= 10010010.00100110.01000000.00000000
= 146.38.64.0
```

**Broadcast Address Calculation:**
```
Network: 10010010.00100110.01000000.00000000
Set all 12 host bits to 1:
10010010.00100110.01001111.11111111
= 146.38.79.255
```

| Field | Value |
|-------|-------|
| Network Address | `146.38.64.0` |
| Broadcast Address | `146.38.79.255` |
| Subnet Mask | `255.255.240.0` |

---

### Subnet B — Marketing

- **CIDR:** `172.31.0.0/16`
- **Subnet Mask:** `255.255.0.0` (first 16 bits = all 1's)

**Network Address Calculation:**
```
172.31.0.0  AND  255.255.0.0
10101100.00011111.00000000.00000000
AND
11111111.11111111.00000000.00000000
= 10101100.00011111.00000000.00000000
= 172.31.0.0
```

**Broadcast Address Calculation:**
```
Network: 10101100.00011111.00000000.00000000
Set all 16 host bits to 1:
10101100.00011111.11111111.11111111
= 172.31.255.255
```

| Field | Value |
|-------|-------|
| Network Address | `172.31.0.0` |
| Broadcast Address | `172.31.255.255` |
| Subnet Mask | `255.255.0.0` |

---

## Key Concepts

**CIDR (Classless Inter-Domain Routing)** — A condensed notation representing an IP address and its subnet mask. Introduced to improve address space utilization as the Internet grew. Moves away from traditional IP classes (A, B, C) toward more efficient address allocation.

**Amazon VPC** — The key benefit of a Virtual Private Cloud is that internal network devices are not openly accessible via the Internet and can only be accessed from within a secure network, keeping proprietary applications and data protected.

---

*Lab confirmed complete — all instances stopped and terminated, EFS file system deleted, S3 bucket contents deleted and bucket removed.*  
**Confirmed by:** Brandy Haynes
