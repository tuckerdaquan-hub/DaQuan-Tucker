# ☁️ Cloud & OS Portfolio

> **Courses:** AWS Cloud Technical Essentials · TryHackMe Linux Fundamentals · TryHackMe Windows Fundamentals
> **Certs in progress:** AWS Solutions Architect Associate · CompTIA Security+
> **Labs completed:** 6 ✅
> **Core skills:** Linux CLI · Windows Administration · IAM · VPC · EC2 · S3 · DynamoDB · ALB · Auto Scaling · Security Groups · SSM Agent · Event Viewer · Resource Monitor

---

## Overview

This portfolio documents six hands-on labs covering the complete skill stack for a cloud operations or junior cloud engineering role — from OS-level Linux and Windows administration, to production-grade AWS infrastructure architecture.

The AWS labs all build around the same **Employee Directory App** — a Node.js web application backed by DynamoDB and S3, running on EC2 inside a custom VPC, scaled automatically behind an Application Load Balancer. The OS labs provide the command-line and system administration foundation that underpins all cloud work.

---

## Labs at a Glance

| Lab | Platform | Focus | Key Skills | Docs |
|---|---|---|---|---|
| [Linux Fundamentals](#linux-fundamentals) | TryHackMe | Linux OS & CLI | Navigation, permissions, processes, cron, HTTP transfer | [README](./Linux_README.md) |
| [Windows Fundamentals](#windows-fundamentals) | TryHackMe | Windows OS & Admin | NTFS, Event Viewer, Resource Monitor, netstat, SSM Agent | [README](./Windows_README.md) |
| [Lab 1 — IAM](#lab-1--iam) | AWS | Identity & access | Users, groups, roles, policy JSON, least privilege | [README](./IAM_README.md) |
| [Lab 2 — EC2 + VPC](#lab-2--ec2--vpc) | AWS | Networking & compute | VPC, subnets, IGW, security groups, User Data | [README](./EC2_VPC_README.md) |
| [Lab 3 — S3 + DynamoDB](#lab-3--s3--dynamodb) | AWS | Storage & database | S3, DynamoDB, bucket policies, service integration | [README](./S3_DynamoDB_README.md) |
| [Lab 4 — Auto Scaling](#lab-4--auto-scaling--high-availability) | AWS | High availability | ALB, Auto Scaling Groups, Launch Templates, multi-AZ | [README](./README.md) |

---

## Full Stack — How Everything Connects

```
┌──────────────────────────────────────────────────────────────────────┐
│  OS Layer                                                           │
│                                                                      │
│  Linux (TryHackMe)              Windows (TryHackMe)                 │
│  ls · cd · chmod · su           ipconfig · netstat · whoami         │
│  ps · top · cron · wget         Event Viewer · Task Scheduler       │
│  python3 -m http.server         Resource Monitor · msconfig         │
│                                 Windows Defender Firewall           │
│                                 SSM Agent (ssm-agent-worker.exe)    │
└────────────────────┬─────────────────────────┬───────────────────────┘
                     │ operates ▼              │ operates ▼
           Linux EC2 instances        Windows EC2 instances
                     │                         │
┌────────────────────▼─────────────────────────▼───────────────────────┐
│  IAM (Lab 1)                                                        │
│  Users → Groups → Policies · EmployeeDirectoryAppRole               │
│  Least privilege · Policy JSON · Resource-based policies            │
└──────────────────────────────┬───────────────────────────────────────┘
                               │ controls access to ▼
┌──────────────────────────────▼───────────────────────────────────────┐
│  Lab VPC  10.10.0.0/16  (Lab 2)                                     │
│                                                                      │
│  IGW → Public Route Table                                           │
│                                                                      │
│  ┌─────────────────────┐    ┌─────────────────────┐                 │
│  │  Public Subnet AZ-a │    │  Public Subnet AZ-b │                 │
│  │  EC2 (Auto Scaled)  │    │  EC2 (Auto Scaled)  │  ← Lab 4       │
│  │  User Data bootstrap│    │  User Data bootstrap│  ← Lab 2       │
│  └─────────────────────┘    └─────────────────────┘                 │
│              │                        │                             │
│              └──────────┬─────────────┘                             │
│                         │                                           │
│              ┌──────────▼──────────┐                                │
│              │  ALB · lab-4        │                                │
│              └──────────┬──────────┘                                │
│                         │ via S3 VPC Endpoint                       │
└─────────────────────────┼────────────────────────────────────────────┘
                          │
             ┌────────────┴────────────┐
             │                         │
    ┌────────▼────────┐      ┌─────────▼───────┐
    │  DynamoDB        │      │  S3 Bucket      │  ← Lab 3
    │  Employees table │      │  Employee photos│
    │  id · name       │      │  + app code     │
    │  photo ──────────┼─────►│  Bucket policy  │
    └──────────────────┘      └─────────────────┘
```

---

## Linux Fundamentals

**[→ Full README](./Linux_README.md)**

**Platform:** TryHackMe Linux Fundamentals Parts 1, 2 & 3 — real VMs over VPN across 3 days.

**What I did:** Filesystem navigation with `ls`, `cd`, `pwd`, `find`. File operations with `touch`, `mv`, `mkdir`. Read permission strings with `ls -lh`, switched users with `su`, changed permissions with `chmod`. Edited files in `nano`. Ran a Python HTTP server on one machine and used `wget` to download from it on a separate machine. Found hidden dotfiles with `ls -a`. Monitored processes with `ps` and `top`. Configured `crontab` with `@reboot`.

**Standout moments:** Two-machine HTTP file transfer (screenshots 5+6) and crontab `@reboot` automation — both directly parallel EC2 User Data and S3 file serving patterns from the AWS labs.

---

## Windows Fundamentals

**[→ Full README](./Windows_README.md)**

**Platform:** TryHackMe Windows Fundamentals Parts 1, 2 & 3 — real Windows 10 VMs over VPN across 2 days.

**What I did:** Read NTFS permissions from `C:\Program Files` Security tab. Managed Administrator vs Standard User accounts. Explored `msconfig` startup modes and tools. Navigated System Properties Advanced tab (environment variables, performance, startup/recovery). Used Computer Management for Task Scheduler (created a basic task) and Event Viewer (Security log with 100,063 entries). Examined Resource Monitor across CPU, Memory, and Network tabs — identified `ssm-agent-worker.exe` as the AWS SSM Agent. Ran `whoami`, `ipconfig`, and `netstat` from an elevated CMD prompt — confirmed `ec2.internal` DNS suffix and live RDP + SSM connections. Explored Windows Security and Defender Firewall domain/private/public profiles.

**Standout moments:** Identifying `ssm-agent-worker.exe` in Resource Monitor and recognising it as the AWS SSM Agent (screenshot 14), and reading `ec2.internal` addresses in both `ipconfig` and Resource Monitor Network output — directly connecting Windows administration to cloud infrastructure.

---

## Lab 1 — IAM

**[→ Full README](./IAM_README.md)**

**What I did:** Configured `EC2-Admin`, `EC2-Support`, and `S3-Support` groups with scoped policies, assigned users, and validated denials by logging in as restricted users. `user-2` (EC2-Support) was blocked from `ec2:StopInstances` — the full ARN and blocked action visible in the error.

**Key concepts:** Users · Groups · Roles · Policy JSON · Least privilege · Default deny · AWS managed vs customer managed policies

---

## Lab 2 — EC2 + VPC

**[→ Full README](./EC2_VPC_README.md)**

**What I did:** Explored VPC with CIDR `10.10.0.0/16`, two public subnets, IGW, S3 VPC endpoint, and scoped outbound security group rules. Launched EC2 (Amazon Linux 2023, t3.micro) with User Data that installs Node.js and deploys the app from S3 on first boot.

**Key concepts:** VPC · CIDR · Subnets · IGW · Route tables · Security groups · S3 VPC Endpoint · AMI · User Data · IMDS · Instance profiles

---

## Lab 3 — S3 + DynamoDB

**[→ Full README](./S3_DynamoDB_README.md)**

**What I did:** Created S3 bucket, wrote JSON bucket policy scoping access to `EmployeeDirectoryAppRole` ARN, uploaded 10 photos. Created DynamoDB `Employees` table with partition key `id`, inserted records with `photo` attribute referencing S3 keys. Verified end-to-end data flow.

**Key concepts:** S3 · Bucket policies · Resource-based vs identity-based policies · DynamoDB · Partition keys · Schemaless NoSQL · Service integration patterns

---

## Lab 4 — Auto Scaling & High Availability

**[→ Full README](./README.md)**

**What I did:** Built Target Group, ALB, Launch Template, and Auto Scaling Group across two AZs. Stress-tested the app and confirmed a second EC2 instance launched automatically with a different Instance ID.

**Key concepts:** ALB · Target groups · Launch Templates · Auto Scaling Groups · Health checks · Multi-AZ · Scaling policies

---

## Skills Demonstrated Across All Labs

| Skill Area | Labs | What I Did |
|---|---|---|
| **Linux CLI** | THM Linux | Navigation, permissions, processes, cron, HTTP transfer between machines |
| **Windows Administration** | THM Windows | NTFS, user accounts, Event Viewer, Resource Monitor, CMD networking, SSM Agent |
| **Identity & Access** | 1, 3 | Least-privilege groups, policy JSON, resource-based bucket policies |
| **Networking** | 2, 4 | VPC, subnets, IGW, route tables, security groups, VPC endpoints |
| **Compute** | 2, 4 | EC2 launch, AMI, User Data scripting, Launch Templates, Auto Scaling |
| **Storage** | 3 | S3 bucket, object upload, resource-based access policy |
| **Database** | 3 | DynamoDB table + partition key, item insertion, NoSQL patterns |
| **High Availability** | 4 | Multi-AZ ALB, ASG, live stress test validation |
| **Security** | All | File permissions, IAM least privilege, SG rules, Defender Firewall, no hardcoded credentials |
| **Automation** | THM Linux, 2, 4 | Cron, User Data bootstrap, Task Scheduler, Launch Templates |
| **Monitoring** | THM Windows, AWS | Resource Monitor, Event Viewer, `ps`/`top`, CloudWatch awareness |
| **JSON / Policy Authoring** | 1, 3 | IAM policy JSON, S3 bucket policy with Principal and Resource arrays |

---

## What I've Done

> "I've built and can operate a complete cloud environment at every layer. At the OS level I'm comfortable in both Linux and Windows — I can navigate filesystems, read permission strings, monitor processes, run networking diagnostics, and interpret what the output tells me about the system. In Linux I understand cron, dotfiles, and inter-machine file transfer. In Windows I can read Event Viewer Security logs, identify processes in Resource Monitor including the AWS SSM Agent, and troubleshoot with ipconfig and netstat from an elevated prompt. On top of that OS foundation I've built a full AWS stack: secured with IAM least-privilege policies, networked with a custom VPC and S3 VPC endpoint, backed by DynamoDB and S3 with resource-based access policies, and made resilient with an Application Load Balancer and Auto Scaling Group I validated with a live stress test. Every layer from the OS up to the cloud infrastructure."

---

## Platforms & Courses

- [AWS Cloud Technical Essentials](https://www.coursera.org/learn/aws-cloud-technical-essentials) — Coursera / AWS Skill Builder
- [TryHackMe Linux Fundamentals](https://tryhackme.com/module/linux-fundamentals) — Parts 1, 2 & 3
- [TryHackMe Windows Fundamentals](https://tryhackme.com/module/windows-fundamentals) — Parts 1, 2 & 3
