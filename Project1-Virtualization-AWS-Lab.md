# Project 1 — Virtualization & AWS Cloud Lab
**Course:** CMIT 495 — Cybersecurity Technology Capstone | UMGC  
**Author:** Brandy Haynes  

---

## Overview

This hands-on lab covers provisioning and launching an AWS Ubuntu-based EC2 server instance, SSH configuration, Linux commands, and an in-depth analysis of virtualization concepts including hypervisor types, cybersecurity posture, and data center consolidation.

---

## Lab 1 — Provisioning an AWS Ubuntu EC2 Instance

### Step-by-Step: Creating and Launching an AWS Ubuntu Server

1. Log into the **AWS Management Console**
2. Navigate to **EC2** via All Services or the search bar
3. On the EC2 Dashboard, select **Launch Instance**
4. **Name the instance:** `My_Web_Server`
5. **Select AMI:** Ubuntu Server 20.04 LTS (HVM), SSD Volume Type — 64-bit
6. **Instance Type:** `t2.micro` — 1 vCPU, 1 GB RAM
7. **Create a new Key Pair:**
   - Name: `My_Web_Server`
   - Type: RSA
   - Format: `.pem`
   - Save the PEM file in a secure, accessible location
8. **Create a VPC:** Open a duplicate tab, search VPN, select VPC and More, enable Auto-generate
9. **Network Settings:** Select the project VPC from the dropdown, refresh subnet, enable Auto-assign public IP
10. **Security Group:** `launch-wizard1`
    - Change Source Type on Rule 2 to **My IP** to restrict access to your specific device
    - Note: Leaving as `0.0.0.0/0` allows anyone to access the instance
    - Setting up an Elastic IP creates a workaround for a secure static IP address
11. **Configure Storage:** Change from 8 GiB to **30 GiB**
12. **Advanced Details:** Enable resource-based IPv4 (A record) DNS Requests
13. **Review and Launch** — verify Instance State shows **Running** in green

---

## Lab 2 — SSH Connection & Linux Commands

### SSH Connection
```bash
ssh -i "C:\Users\Brandy\Downloads\My_Web_Server.pem" ubuntu@ec2-98-81-105-133.compute-1.amazonaws.com
```
> Note: If you log out and back into your lab the ubuntu@ec2- IP address can change

### Update and Upgrade Commands
```bash
$ sudo apt-get update
$ sudo apt-get upgrade
```

**What these commands do:**
- `sudo apt-get update` — scans configured repositories to find available updates, security patches, and new software versions. Think of it as a Google search for updates — it finds but does not install them
- `sudo apt-get upgrade` — actually installs the updates found by the update command
- Best practice: Use `unattended-upgrades` to automatically install security patches with minimal manual effort
- These commands should be run regularly — at minimum monthly, ideally weekly for security-critical systems

### System Information Commands
```bash
echo 'Brandy Haynes' && echo 'CMIT 495 6383 2252' && date
whoami
ip a show
pwd
ping -c 4 www.google.com
```

---

## Analysis Questions

### Q: What account type does `whoami` reveal?

Linux has two primary account types:
- **Root** — unrestricted administrative access; can manage user accounts, modify file systems, install updates
- **Regular User** — limited permissions; cannot make system-wide changes

The **Principle of Least Privilege** dictates that regular users should only be able to modify their own files — preventing accidental or unauthorized system-wide modifications and enhancing overall security.

---

### Q: Why are IP addresses different between a home network and AWS EC2?

**Home Network (SOHO):**
- Public IP: Assigned by ISP (e.g., `24.245.x.x`)
- Private IP: Assigned by router's DHCP (e.g., `192.168.x.x`)
- Router uses NAT to share one public IP across all LAN devices

**AWS EC2 Instance:**
- Public IP: Assigned by AWS (e.g., `98.81.105.133`)
- Private IP: Assigned within VPC via AWS-managed DHCP (e.g., `10.0.3.234`)
- Public IP is mapped through the VPC Internet Gateway instead of a physical router

**Private IP Ranges (IANA Reserved):**
- `192.168.0.0/16`
- `10.0.0.0/8`

Public IPs are routable over the internet and accessible from anywhere. Private IPs are only accessible within the same internal network.

---

### Q: Benefits of Virtualization in a Cloud Environment

**1. Cost & Resource Efficiency**
Server consolidation, load balancing, and dynamic resource allocation reduce the need for on-site servers, physical space, maintenance, and staffing costs. Pay-per-use pricing means organizations only pay for resources consumed.

**2. Scalability & Flexibility**
Unlike physical servers limited by their hardware, virtual resources can be scaled up or down instantly. A startup can allocate 4 GiB RAM and overprovision to 8 GiB during peak seasons without purchasing new hardware.

**3. High Availability & Load Balancing**
Load balancing distributes network traffic across servers while dynamic resource allocation adjusts based on real-time conditions. If a server fails, workloads automatically transfer to another server — preventing downtime and ensuring consistent performance.

---

### Q: Data Center Consolidation — Benefits & Concerns

**Benefits:**
- Improved physical hardware utilization
- Reduced operational costs and physical space requirements
- Simplified management via centralized tools (VMware, AWS Management Console)

**Concerns During/After Transition:**
- **Migration Complexity** — transferring massive amounts of data, applications, and services without disrupting critical operations requires meticulous planning, extensive testing, and phased implementation
- **Security Risks** — data exposure during transfer if encryption is not enforced; misconfigurations can create hidden vulnerabilities post-migration

**Mitigations:**
- Conduct thorough risk assessments before and after migration
- Apply strong access controls and encryption in transit
- Continuously monitor both environments throughout migration
- Establish clearly defined rollback procedures with date-stamped backup images

---

### Q: Does Virtualization Improve Cybersecurity Posture?

Yes — but it is a double-edged sword. Virtualization expands the attack surface by adding layers including the hypervisor itself and each individual VM.

**Mitigations:**
- **Network Segmentation** — separate virtual networks by function and sensitivity to limit lateral movement
- **Sandboxing** — isolate high-risk applications so a compromise cannot spread to the rest of the environment
- **Snapshot & Rollback** — restore systems to a known-good state following incidents, misconfigurations, or failed patches
- **Centralized Monitoring** — real-time visibility into virtual infrastructure for faster threat response

---

### Q: Type 1 vs Type 2 Hypervisors — Which is More Secure?

| Feature | Type 1 (Bare Metal) | Type 2 (User-Space) |
|---------|--------------------|--------------------|
| Runs on | Directly on hardware | Within host OS |
| Attack surface | Smaller | Larger |
| Performance | Higher | Lower |
| Use case | Production/critical systems | Testing/development |
| Risk | Hypervisor-level compromise | Host OS vulnerability cascades |

**Type 1 is more secure** — it runs directly on physical hardware, reduces dependency on third-party software, and provides tighter VM isolation.

**Hardening Type 1:**
- Implement strict access control policies
- Enable continuous monitoring and log auditing
- Automate regular security patches
- Minimize unnecessary services running on the hypervisor

**Hardening Type 2:**
- Regular host OS hardening
- Disable unnecessary services
- Install antivirus, anti-malware, and host intrusion detection
- Apply network segmentation
- Maintain regular backup and recovery images
