# AWS Lab 04 – EC2 Instance Setup & Management

## 📘 Overview
This lab demonstrates how to launch, configure, and manage EC2 instances — the fundamental compute service in AWS.  
You will create an EC2 instance, connect via SSH, attach an EBS volume, and understand snapshots and Elastic IPs.  

**Goal →** Deploy and manage a secure and persistent virtual machine in AWS.

---

## 🏗️ Architecture Diagram
```text
VPC (Default)
│
├── EC2 Instance (Public Subnet)
│     ├── Security Group → Allows SSH (22)
│     ├── Key Pair → dhruvish-key.pem
│     └── EBS Volume (root + attached /data)
│
└── Internet Gateway (for SSH & updates)
```

---

## 🚀 Steps Performed
```text
1️⃣ Launch an EC2 Instance

- Service: EC2 → Launch Instance
- Name: dhruvish-ec2-lab
- AMI: Amazon Linux 2
- Instance Type: t2.micro
- Key Pair: Create/download dhruvish-key.pem
- Network: Default VPC, Public Subnet
- Security Group: Allow SSH (22) from your IP
- Storage: 8 GB gp3
- Launch the instance

✅ Result: Instance running and visible in EC2 dashboard.
```

```text
2️⃣ Connect to EC2 via SSH

chmod 400 dhruvish-key.pem
ssh -i dhruvish-key.pem ec2-user@<Public-IP>

✅ You are now inside your EC2 Linux instance.
```

```text
3️⃣ Attach an EBS Volume

- EC2 → Volumes → Create Volume (8GB gp3)
- Attach it to your EC2 instance

Commands to format and mount:
sudo lsblk
sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data

✅ Volume mounted and ready for use.
```

```text
4️⃣ Create an AMI Snapshot

- Select instance → Actions → Create Image
✅ Snapshot and AMI created for disaster recovery.
```

```text
5️⃣ Stop & Start Instance

- Stop → Start → Check new Public IP
✅ Demonstrates ephemeral public IP behavior.
```

---

## 🔐 Security Configurations
| Control | Purpose |
|:--|:--|
| Security Group | Allows controlled inbound SSH access |
| Key Pair | Secure SSH authentication |
| IAM Role (optional) | Granular instance permissions |
| Elastic IP | Static IP for persistent servers |
| EBS Encryption | Data protection at rest |

---

## 🧠 Key Takeaways
```text
- EC2 is AWS’s main compute engine.
- Security Groups act as virtual firewalls (stateful).
- EBS provides persistent, encrypted block storage.
- Elastic IPs maintain consistent connectivity.
- Snapshots enable quick backup and recovery.
```

---

## 🧩 Verification Commands (CLI)
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]"
aws ec2 describe-volumes
aws ec2 describe-images --owners self
```

---

## ✅ Results
- EC2 instance successfully launched and configured.
- SSH access verified via key pair.
- EBS volume attached, formatted, and mounted.
- AMI snapshot created for backup.
- Elastic IP and security rules confirmed functional.
