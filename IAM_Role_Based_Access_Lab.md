# AWS IAM Role-Based Access Control – Identity & Access Simulation  
Author: Dhruvish Rathod  
Role: SOC Analyst | Cloud Security Enthusiast  
Date: September 2025  

---

📌 **Objective**  
Implement and test IAM Users, Groups, and Policies in AWS. Key goals:  
- Configure least-privilege access via group membership.  
- Differentiate between **managed** and **inline** policies.  
- Validate access restrictions by signing in as different users.  

---

🛠 **Tools & Services Used**  
- AWS Identity & Access Management (IAM)  
- Amazon EC2 (test access)  
- Amazon S3 (test access)  

---

🌐 **Scenario Overview**  
A company requires role-based access for staff:  
- **user-1** → S3-Support (read-only S3 access)  
- **user-2** → EC2-Support (read-only EC2 access)  
- **user-3** → EC2-Admin (view + start/stop EC2 instances)  

IAM groups and policies were already defined:  
- `AmazonS3ReadOnlyAccess` (managed policy)  
- `AmazonEC2ReadOnlyAccess` (managed policy)  
- `EC2-Admin-Policy` (inline policy with Start/Stop permissions)  

---

🔍 **Findings**  
- **user-1** could list and view S3 buckets but was denied EC2 access.  
- **user-2** could describe EC2 instances but was denied Start/Stop actions and denied S3 access.  
- **user-3** successfully started/stopped EC2 instances, validating admin permissions.  

---

🛠 **Remediation / Best Practices**  
1. Use **managed policies** for scalable roles (support staff).  
2. Apply **inline policies** sparingly for one-off scenarios.  
3. Always validate IAM permissions by testing with actual user logins.  
4. Document IAM sign-in URLs for operational readiness.  

---

✅ **Outcome**  
- Successfully enforced least-privilege access.  
- Validated policy scope using real user login tests.  
- Demonstrated IAM group-based access as a scalable security model.  

---

📊 **Lessons Learned**  
- IAM policies must always be tested — documentation alone is insufficient.  
- Support roles benefit from managed policies; admin tasks often need inline policies.  
- Principle of Least Privilege is easiest to maintain at the **group level**.  

---

📎 **References**  
- [Original Lab PDF](https://github.com/Dhruvish44/AWS-Labs/blob/main/Introduction%20to%20AWS%20Identity%20and%20Access%20Management%20(IAM).pdf)  
