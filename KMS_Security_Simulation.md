# 🔑 AWS KMS Security & Encryption Simulation  
**Author:** Dhruvish Rathod  
**Role:** SOC Analyst | Cloud Security Enthusiast  
**Date:** September 2025  

---

## 📌 Objective  
Set up **AWS Key Management Service (KMS)** to create and manage encryption keys, integrate with **S3 + CloudTrail**, and monitor encryption usage logs for compliance.  

---

## 🛠 Tools & Services Used  
- **AWS KMS** — Key creation & management  
- **Amazon S3** — Encrypted object storage  
- **AWS CloudTrail** — Key usage monitoring & logging  

---

## 🌐 Scenario Overview  
- Created **symmetric customer-managed key** (`myFirstKey`).  
- Configured **CloudTrail** to log activity into a new S3 bucket.  
- Encrypted an uploaded object with **SSE-KMS**.  
- Verified **access control restrictions** (Access Denied for public requests).  
- Monitored **CloudTrail logs** for encryption key usage.  
- Modified **key user permissions** to simulate access control.  

---

## 🔍 Findings  
- S3 encryption worked only for authorized IAM roles using **AWS Signature v4**.  
- Public link access failed → proving default restriction of SSE-KMS.  
- CloudTrail captured **encryption events with Key ID and file name**.  
- Removing/adding IAM users to key policies immediately impacted access.  

---

## 🛠 Remediation Steps  
1. Created and described **KMS master key**.  
2. Configured **CloudTrail trail → S3 bucket** for logging.  
3. Applied **SSE-KMS** encryption at object upload.  
4. Validated **Access Denied** for public attempts.  
5. Reviewed **CloudTrail logs** for compliance audit.  
6. Tested **key user removal and re-addition** to confirm fine-grained access control.  

---

## ✅ Outcome  
- Demonstrated secure key management lifecycle.  
- Proved **compliance readiness** via CloudTrail monitoring.  
- Strengthened **least-privilege IAM practices**.  

---

📄 **Lab PDF:** [View here](https://github.com/Dhruvish44/AWS-Labs/blob/main/Introduction%20to%20AWS%20Key%20Management%20Service.pdf)  
