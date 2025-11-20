# AWS Lab 40 – AWS Organizations + Service Control Policies (SCP)

## 📘 Overview
This lab configures a multi-account environment using AWS Organizations and applies SCPs to enforce governance rules.

**Goal →** Restrict regions, protect CloudTrail, and control account-level permissions.

---

## 🏗️ Architecture Diagram
```text
Management Account
   │
   ├── Security OU (SCPs applied)
   │       ├── Prod Account
   │       └── Dev Account
   │
   └── Sandbox OU (less restrictive)
```

---

## 🚀 Steps Performed

### 1️⃣ Create AWS Organization
Console → AWS Organizations  
```
Create Organization → Enable All Features
```

---

### 2️⃣ Create Organizational Units
```
OU-1: Security
OU-2: Sandbox
```

Move accounts into respective OUs.

---

### 3️⃣ Create SCP — Deny Non-AP-South-1 Regions
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestedRegion": "ap-south-1"
        }
      }
    }
  ]
}
```

Attach to **Security OU**.

---

### 4️⃣ Create SCP — Prevent Modifying CloudTrail
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "cloudtrail:DeleteTrail",
        "cloudtrail:StopLogging"
      ],
      "Resource": "*"
    }
  ]
}
```

Attach to **Root** or **Security OU**.

---

### 5️⃣ Create SCP — Prevent Leaving Organization
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Deny",
    "Action": "organizations:LeaveOrganization",
    "Resource": "*"
  }]
}
```

---

## 🧩 Verification
Try switching to a member account and perform:

```bash
aws ec2 describe-instances --region us-east-1
```
Should fail.

Try deleting CloudTrail:
```bash
aws cloudtrail delete-trail --name <trail>
```
Should fail.

---

## 🧠 Key Takeaways
- SCPs override IAM.  
- SCPs apply to **root user** of member accounts.  
- SCPs do NOT grant permissions — only restrict.
