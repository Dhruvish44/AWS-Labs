# Amazon S3 Security & Bucket Policy Simulation  
**Author:** Dhruvish Rathod  
**Role:** SOC Analyst | Cloud Security Enthusiast  
**Date:** September 2025  

---

## 📌 Objective  
Set up and secure an **Amazon S3 bucket** to store EC2 report data. Configure permissions, test public vs private access, apply bucket policies, and enable versioning for accidental deletion protection.  

---

## 🛠 Tools & Services Used  
- **Amazon S3** — Object storage  
- **AWS IAM** — Roles & permissions  
- **Amazon EC2** — Connectivity test  
- **AWS Systems Manager** — Session Manager access  

---

## 🌐 Scenario Overview  
- Created an S3 bucket named `reportbucket-<AccountID>`.  
- Uploaded objects and tested default access (private).  
- Applied **ACLs** and **bucket policy** for role-based permissions.  
- Enabled **versioning** to preserve deleted/modified files.  

---

## 🔍 Findings  
- Objects are private by default (Access Denied without permissions).  
- Bucket needed explicit **PutObject + GetObject** permissions for EC2 role.  
- Public access blocked until BPA (Block Public Access) was turned off.  
- Versioning allowed rollback after accidental deletion.  

---

## 🛠 Remediation Steps  
1. Created IAM role `EC2InstanceProfileRole` with S3 access.  
2. Applied bucket policy:  

```json
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Principal": {"AWS": "arn:aws:iam::<AccountID>:role/EC2InstanceProfileRole"},
     "Action": ["s3:GetObject","s3:PutObject"],
     "Resource": "arn:aws:s3:::reportbucket-<AccountID>/*"
   }
 ]
}
```
3. Enabled bucket versioning.

✅ Outcome
Controlled least-privilege access with IAM roles.

Prevented accidental data loss with versioning.

Documented bucket security posture in GitHub for audit-ready proof.

📄 **Lab PDF:** [View here](https://github.com/Dhruvish44/AWS-Labs/blob/main/Introduction%20to%20Amazon%20Simple%20Storage%20Service%20(S3).pdf)  
