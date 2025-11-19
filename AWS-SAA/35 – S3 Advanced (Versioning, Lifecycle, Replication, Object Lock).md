# AWS Lab 35 – S3 Advanced (Versioning, Lifecycle, Replication, Object Lock)

## 📘 Overview
This lab teaches advanced S3 configurations used in real-world architectures:  
Versioning → Lifecycle policies → Replication → Object Lock.

**Goal →** Build an enterprise-grade S3 bucket with compliance, automation, and data protection.

---

## 🏗️ Architecture Diagram
```text
S3 Source Bucket (Versioning + Object Lock)
     │
     ├── Lifecycle → move to IA/Glacier
     │
     └── Replication → S3 Destination Bucket (CRR/SRR)
```

---

## 🚀 Steps Performed

### 1️⃣ Create Source Bucket
```text
Bucket: dhruvish-source-adv
Region: ap-south-1
Enable: Versioning
Enable: Server-side Encryption (SSE-S3)
Block Public Access: ON
```

### 2️⃣ Enable Object Lock (must enable at bucket creation)
```text
Object Lock: ENABLED
Mode: Governance
Retention: 14 days
```

### 3️⃣ Create Lifecycle Policy
Lifecycle → Create Rule:
```
Transition after 30 days: Standard → IA
Transition after 90 days: IA → Glacier
Expire Delete Markers: After 120 days
```

### 4️⃣ Create Destination Bucket for Replication
```text
Bucket: dhruvish-destination-adv
Enable: Versioning
```

### 5️⃣ Configure Replication Rule
```
Source: dhruvish-source-adv
Destination: dhruvish-destination-adv
Options:
- Replicate delete markers
- Replicate existing objects (optional)
- KMS encryption support: ENABLED
```

### 6️⃣ Upload Test Files
Upload:
```
file1.txt
file2.txt
```

Modify file1.txt → trigger versioning  
Delete file2.txt → creates delete marker

---

## 🧩 Verification
Check Replication:
```bash
aws s3 ls s3://dhruvish-destination-adv/
```

Check Object Lock:
```bash
aws s3api get-object-retention --bucket dhruvish-source-adv --key file1.txt
```

Check Versions:
```bash
aws s3api list-object-versions --bucket dhruvish-source-adv
```

---

## 🧠 Key Takeaways
- Versioning + Object Lock = Compliance + Protection.  
- Lifecycle reduces storage costs.  
- Replication requires **versioning**.  
- Governance mode can be overridden; Compliance cannot.
