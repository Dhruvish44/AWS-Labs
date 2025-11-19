# AWS Lab 37 – FSx for Windows + FSx for Lustre (Enterprise File Systems)

## 📘 Overview
This lab demonstrates provisioning two enterprise file systems:

- **FSx for Windows** (SMB, Active Directory integration)  
- **FSx for Lustre** (HPC + S3 integration)

**Goal →** Understand FSx behavior, protocol support, and integration patterns.

---

## 🏗️ Architecture Diagram
```text
EC2 Windows Instance ─── SMB ──▶ FSx for Windows
EC2 Linux Instance   ─── Lustre ──▶ FSx for Lustre ──▶ S3 (data lake)
```

---

## 🚀 Steps Performed

### 1️⃣ FSx for Windows File System
```
Name: dhruvish-fsx-win
Storage: 32 GiB
Throughput: 8 MB/s
Join to AD: AWS Managed AD
Backup: Daily
```

Mount from Windows EC2:
```powershell
net use Z: \\amznfsx\share
```

---

### 2️⃣ FSx for Lustre
```
Name: dhruvish-fsx-lustre
Deployment Type: Scratch 1
Storage: 1200 GiB
Linked S3 Bucket: s3://dhruvish-lustre-data
```

Mount from Linux EC2:
```bash
sudo mkdir /fsx
sudo mount -t lustre <dns-name>@tcp:/fsx /fsx
```

Write file:
```bash
echo "test" | sudo tee /fsx/file1.txt
```

---

## 🧩 Verification
List files:
```bash
ls -l /fsx
```

Check S3 import/export:
```bash
aws s3 ls s3://dhruvish-lustre-data
```

---

## 🧠 Key Takeaways
- FSx Windows → SMB + AD, Windows workloads.  
- FSx Lustre → HPC, ML, big data, S3 integration.  
- Both offer high performance + enterprise features.
