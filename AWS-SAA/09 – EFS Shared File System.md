# AWS Lab 09 – EFS Shared File System

## 📘 Overview
Set up EFS for shared storage between two EC2 instances.

---

## 🚀 Steps Performed
```text
1️⃣ Create EFS File System
- EFS → Create File System → VPC: default or custom
- Enable Encryption with KMS
```

```text
2️⃣ Add Mount Targets
- One in each AZ used by EC2s.
```

```text
3️⃣ Launch Two EC2 Instances
- Same VPC, different subnets.  
- Install NFS client:
sudo yum install -nfs-utils -y
```

```text
4️⃣ Mount EFS
sudo mkdir /shared
sudo mount -t nfs4 <efs-dns>:/ /shared
touch /shared/test.txt
✅ File visible from both instances.
```

---

## 🧠 Key Takeaways
- EFS supports multi-instance mounts.  
- Automatically replicated across AZs.  
- Ideal for web apps or shared config storage.
