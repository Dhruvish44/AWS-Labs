# 🕵️ AWS Environment Audit Simulation  
**Author:** Dhruvish Rathod  
**Role:** SOC Analyst | Cloud Security Enthusiast  
**Date:** September 2025  

---

## 📌 Objective  
Perform a **basic audit** of AWS IAM, EC2, VPC, CloudWatch, and CloudTrail to ensure compliance with security best practices and governance frameworks.  

---

## 🛠 Tools & Services Used  
- **AWS IAM** — Access controls & policy simulation  
- **Amazon EC2** — Security group inspection  
- **Amazon VPC** — NACL & subnet review  
- **Amazon CloudWatch** — Metrics & alarms  
- **AWS CloudTrail** — Log inspection & evidence collection  

---

## 🌐 Scenario Overview  
- Audited **IAM user permissions** with MFA & policy simulator.  
- Checked **EC2 security groups** for Web Server, Bastion Host, and SQL Server.  
- Validated **VPC ACLs & subnet isolation**.  
- Monitored **CloudWatch metrics (CPU, EBS)** and reviewed alarms.  
- Inspected **CloudTrail JSON logs** inside S3 bucket.  

---

## 🔍 Findings  
- IAM user had **ReadOnlyAccess** → Delete/Modify actions denied.  
- Web server SG restricted to **10.10.10.0/24** instead of open internet → strong security.  
- Bastion Host only allowed **SSH/RDP from management subnet**.  
- SQL Server only accessible through **Bastion + Web server security groups**.  
- CloudTrail logs confirmed traceability of admin & API actions.  

---

## 🛠 Remediation Steps  
1. Captured IAM evidence using **Policy Simulator**.  
2. Documented restrictive SG rules for **tiered architecture**.  
3. Validated **VPC ACL rules** to enforce subnet-level security.  
4. Monitored **CloudWatch CPU + EBS metrics** for system health.  
5. Verified **CloudTrail JSON logs** in S3 for compliance audit trail.  

---

## ✅ Outcome  
- Completed **multi-layer AWS audit** (IAM, EC2, VPC, logging).  
- Ensured environment met **least-privilege & compliance standards**.  
- Demonstrated ability to **collect, analyze, and report audit evidence**.  

---

📄 **Lab PDF:** [View here](https://github.com/Dhruvish44/AWS-Labs/blob/main/Performing%20a%20Basic%20Audit%20of%20your%20AWS%20Environment.pdf)  
