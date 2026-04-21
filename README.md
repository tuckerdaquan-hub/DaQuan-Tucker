# Hello, I'm DaQuan

---

I'm a self-starter with a profound interest in technology and dedicated to solving complex problems. 

--- 
## Objective

My journey in technology has led me to develop a passion for cybersecurity, and I eager to transition into the field, specifically aiming to work my way up to be in cloud security.

---

## Labs at a Glance

| Lab | Platform | Focus | Key Skills | Docs |
|---|---|---|---|---|
| Linux Fundamentals | TryHackMe | Linux OS & CLI | Navigation, permissions, processes, cron, HTTP transfer | [README](https://github.com/tuckerdaquan-hub/Linux-Lab/tree/main) |
| Windows Fundamentals | TryHackMe | Windows OS & Admin | NTFS, Event Viewer, Resource Monitor, netstat, SSM Agent | [README](https://github.com/tuckerdaquan-hub/Windows-Lab/tree/main) |
| Lab 1 — IAM | AWS | Identity & access | Users, groups, roles, policy JSON, least privilege | [README](https://github.com/tuckerdaquan-hub/IAM-Polices/tree/main) |
| Lab 2 — EC2 + VPC | AWS | Networking & compute | VPC, subnets, IGW, security groups, User Data | [README] |
| Lab 3 — S3 + DynamoDB | AWS | Storage & database | S3, DynamoDB, bucket policies, service integration | [README] |
| Lab 4 — Auto Scaling | AWS | High availability | ALB, Auto Scaling Groups, Launch Templates, multi-AZ | [README] |

---

## Linux Fundamentals

**[→ Full README][(./Linux_README.md)](https://github.com/tuckerdaquan-hub/Linux-Lab/tree/main)**

**What I did:** Filesystem navigation with `ls`, `cd`, `pwd`, `find`. File operations with `touch`, `mv`, `mkdir`. Read permission strings with `ls -lh`, switched users with `su`, changed permissions with `chmod`. Edited files in `nano`. Ran a Python HTTP server on one machine and used `wget` to download from it on a separate machine. Found hidden dotfiles with `ls -a`. Monitored processes with `ps` and `top`. Configured `crontab` with `@reboot`.

---

## Windows Fundamentals

**[→ Full README](https://github.com/tuckerdaquan-hub/Windows-Lab/tree/main)**

**What I did:** Read NTFS permissions from `C:\Program Files` Security tab. Managed Administrator vs Standard User accounts. Explored `msconfig` startup modes and tools. Navigated System Properties Advanced tab (environment variables, performance, startup/recovery). Used Computer Management for Task Scheduler (created a basic task) and Event Viewer (Security log with 100,063 entries). Examined Resource Monitor across CPU, Memory, and Network tabs — identified `ssm-agent-worker.exe` as the AWS SSM Agent. Ran `whoami`, `ipconfig`, and `netstat` from an elevated CMD prompt — confirmed `ec2.internal` DNS suffix and live RDP + SSM connections. Explored Windows Security and Defender Firewall domain/private/public profiles.

---

## Lab 1 — IAM

**[→ Full README][(./IAM_README.md)](https://github.com/tuckerdaquan-hub/IAM-Polices/tree/main)**

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

## What I've Done

> "I've built and can operate a complete cloud environment at every layer. At the OS level I'm comfortable in both Linux and Windows — I can navigate filesystems, read permission strings, monitor processes, run networking diagnostics, and interpret what the output tells me about the system. In Linux I understand cron, dotfiles, and inter-machine file transfer. In Windows I can read Event Viewer Security logs, identify processes in Resource Monitor including the AWS SSM Agent, and troubleshoot with ipconfig and netstat from an elevated prompt. On top of that OS foundation I've built a full AWS stack: secured with IAM least-privilege policies, networked with a custom VPC and S3 VPC endpoint, backed by DynamoDB and S3 with resource-based access policies, and made resilient with an Application Load Balancer and Auto Scaling Group I validated with a live stress test. Every layer from the OS up to the cloud infrastructure."

---

## Tools

---

## Certifications
