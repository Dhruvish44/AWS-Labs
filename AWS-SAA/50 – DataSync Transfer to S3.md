# AWS Lab 50 – DataSync Transfer to S3

## 📘 Overview
This lab demonstrates high-speed data copying from on-prem (simulated via EC2) to S3 using **AWS DataSync**.

---

## 🏗️ Architecture Diagram
```text
EC2 Linux (Acting On-Prem)
          │
        DataSync Agent
          │
      DataSync Service
          │
          ▼
           S3 Bucket
```

---

## 🚀 Steps Performed

### 1️⃣ Set Up Source Directory on EC2
```bash
mkdir /datasync-source
echo "File 1" > /datasync-source/file1.txt
```

---

### 2️⃣ Deploy DataSync Agent
Create Agent:
```
Deployment: EC2 Virtual Appliance
```

Activate agent with token from console.

---

### 3️⃣ Create Locations
- Source: NFS endpoint (EC2 path)
- Destination: S3 bucket (`dhruvish-datasync-bucket`)

---

### 4️⃣ Configure DataSync Task
```
Verify: Enabled
Bandwidth: Unlimited
Include: All files
```

Start the task.

---

## 🧩 Verification

List objects in S3:
```bash
aws s3 ls s3://dhruvish-datasync-bucket/
```

Should see:
```
file1.txt
```

---

## 🧠 Key Takeaways
- DataSync automates fast, secure migration.  
- Better than rsync for TB/PB scale workloads.  
- Supports NFS, SMB, S3, EFS, FSx.
