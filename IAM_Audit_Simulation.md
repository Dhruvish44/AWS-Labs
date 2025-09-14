# IAM Audit Simulation – AWS Environment

**Author:** Dhruvish Rathod  
**Role:** SOC Analyst (Aspiring Cloud Security)  
**Date:** August 2025  

---

## 📌 Objective
To perform a mock IAM access audit in a simulated AWS environment, identify over-privileged accounts and roles, detect risky access patterns, and enforce least privilege without breaking functionality.

---

## 🛠 Tools & Services Used
- **AWS IAM Console** – User and role policy review  
- **CloudTrail** – Activity logging and anomaly detection  
- **IAM Policy Simulator** – Testing and validating policy changes  
- **Visual Studio Code** – Editing JSON IAM policies  

---

## 🌐 Scenario Overview
During a routine IAM audit in a mock AWS environment, I identified the following issues:

1. **User: `devops_temp`**
   - Had full admin access (`"Action": "*", "Resource": "*"`).
   - Risk: Over-privileged for a contractor role.  
   - CloudTrail logs showed **S3:PutObject** actions on a production bucket during off-hours.

2. **Role: `EC2Admin`**
   - Inline policies included full RDS permissions.
   - Risk: Misaligned with job function (role should be limited to EC2 only).  

---

## 🔍 Findings

| **Entity**   | **Issue**                                   | **Risk Level** | **Evidence**                   |
|--------------|---------------------------------------------|----------------|--------------------------------|
| `devops_temp` | Full `*:*` permissions                      | Critical       | CloudTrail off-hours S3 access |
| `EC2Admin`   | Inline RDS full permissions                 | High           | Role permissions misaligned    |

---

## 🛠 Remediation Steps

1. **Restrict Contractor Permissions**  
   Created a custom IAM policy restricting `devops_temp` to S3 access for specific project buckets only.

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "s3:ListBucket",
           "s3:GetObject",
           "s3:PutObject"
         ],
         "Resource": [
           "arn:aws:s3:::project-data-bucket",
           "arn:aws:s3:::project-data-bucket/*"
         ]
       }
     ]
   }

2. Replace Inline RDS Permissions

Removed inline RDS full access from the EC2Admin role and attached the AWS-managed ReadOnlyAccess policy instead.

3. Enforce MFA

Enabled MFA for all IAM users to reduce account takeover risks and strengthen authentication.

✅ Outcome

Reduced attack surface by eliminating unnecessary admin privileges.

Implemented least privilege access aligned with job roles.

Maintained business continuity without breaking functionality.

Improved audit readiness and compliance posture.

📊 Lessons Learned

Contractor accounts should never have wildcard permissions.

Inline policies create policy drift risk → prefer managed/custom policies.

CloudTrail is essential for detecting abnormal access behavior.

MFA enforcement should be a baseline requirement.
