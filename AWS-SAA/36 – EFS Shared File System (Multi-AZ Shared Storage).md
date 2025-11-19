# AWS Lab 36 – EFS Shared File System (Multi-AZ Shared Storage)

## 📘 Overview
This lab deploys an **EFS file system** and mounts it across **two EC2 instances in different AZs**, demonstrating shared POSIX-compliant storage.

**Goal →** Show how EFS enables multiple EC2 instances to share the same file system.

---

## 🏗️ Architecture Diagram
```text
EC2-A (AZ a) ─┐
              │
           EFS Mount Target (Multi-AZ)
              │
EC2-B (AZ b) ─┘
```

---

## 🚀 Steps Performed

### 1️⃣ Create EFS File System
```
Name: dhruvish-efs
Performance: General Purpose
Throughput: Bursting
Lifecycle: Enable IA transitions
```

### 2️⃣ Enable Multi-AZ Mount Targets
EFS automatically creates:
- Mount target in ap-south-1a  
- Mount target in ap-south-1b  

---

### 3️⃣ Launch Two EC2 Instances
```
EC2-A → subnet in ap-south-1a
EC2-B → subnet in ap-south-1b
AMI: Amazon Linux 2
SG: Allow NFS (port 2049) from EC2 SG
```

---

### 4️⃣ Install NFS Utils
SSH into each instance:
```bash
sudo yum install -y amazon-efs-utils
```

---

### 5️⃣ Mount EFS on Both Instances
Mount command:
```bash
sudo mkdir /efs
sudo mount -t efs <FileSystemID>:/ /efs
```

---

### 6️⃣ Test Shared Write
On EC2-A:
```bash
echo "Hello from A" | sudo tee /efs/testfile.txt
```

On EC2-B:
```bash
cat /efs/testfile.txt
```

Should output:
```
Hello from A
```

---

## 🧩 Verification
Check mounted file system:
```bash
df -h
```

Test read/write across instances:
```bash
touch /efs/test-B.txt
```

---

## 🧠 Key Takeaways
- EFS = shared, scalable, multi-AZ file system.  
- Perfect for web servers, content-sharing, and Linux apps.  
- Supports Lifecycle → EFS → EFS-IA to reduce cost.
