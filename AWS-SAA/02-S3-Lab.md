# AWS Lab 02 – Amazon S3 Secure Bucket Configuration

## 📘 Overview
This lab explores how to create and secure an S3 bucket using IAM policies, bucket policies, and encryption.  
Goal →  Store objects securely and apply least-privilege access for different users.

---

## 🏗️ Architecture Diagram
```text
[AdminUser] (full S3 access)  
 ↳ Bucket: dhruvish-day1-lab  
  • Public Access Blocked  
  • Versioning Enabled  
  • Encryption SSE-S3 Active  
  • Object: sample.txt  
[DevUser] (S3 ReadOnly access via IAM policy)
```


---

## 🚀 Steps Performed
1. **Create Bucket** `dhruvish-day1-lab` in `ap-south-1`.  
2. **Block Public Access** (all options ON).  
3. **Enable Versioning** & **Default Encryption (SSE-S3)**.  
4. **Upload** `sample.txt`.  
5. **Generate Pre-Signed URL** (valid 5 minutes) → tested download.  
6. **Sign in as dev-user** → read-only verified; no delete rights.  
7. **Add Lifecycle Rule** → transition to S3-IA after 30 days.

---

## 🔒 Security Controls Applied
| Control | Purpose |
|:--|:--|
| Block Public Access | Prevents public exposure |
| Versioning | Enables object recovery |
| SSE-S3 Encryption | Protects data at rest |
| IAM Policy | Grants least privilege access |
| Pre-Signed URL | Temporary object sharing |
| Lifecycle Rule | Automates cost optimization |

---

## ✅ Results
- Bucket and objects are private and encrypted.  
- IAM permissions function as expected.  
- Lifecycle rule active for archival policy.

---

## 🧠 Key Takeaways
- Combine IAM and Bucket Policies for fine-grained control.  
- Always enable encryption and block public access.  
- Versioning + Lifecycle Rules protect and save cost.  
- Pre-Signed URLs enable secure, temporary access.

---

## 📚 References
- [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)  
- [S3 Security Best Practices](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)

