# AWS Lab 01 – Identity and Access Management (IAM)

## 📘 Overview
This lab demonstrates how AWS Identity and Access Management (IAM) controls access through **users**, **groups**, **roles**, and **policies**.  
Goal →  Implement least-privilege access and enable MFA for admin accounts.

---

## 🏗️ Architecture Diagram
```text
[Root Account]  
 ├── Group: Admins (AdministratorAccess)  
 │  └── User: dhruvish-admin ✅ MFA enabled  
 └── Group: Developers (AmazonS3ReadOnlyAccess)  
    └── User: dev-user

```
---

## 🚀 Steps Performed
1. **Create Groups** – `Admins`, `Developers`.  
2. **Attach Policies** – `AdministratorAccess` → Admins; `AmazonS3ReadOnlyAccess` → Developers.  
3. **Create Users** – `dhruvish-admin`, `dev-user`; assign to groups.  
4. **Enable MFA** for `dhruvish-admin` (Google Authenticator).  
5. **Sign in as dev-user** → verify read-only S3 permissions.  
6. **Sign in as dhruvish-admin** → verify full access.

---

## 🔐 Security Best Practices Applied
- Root account locked with MFA.  
- Individual IAM users (no shared accounts).  
- MFA on admin user.  
- Policies grant only required permissions.  
- Access keys not generated for console-only users.

---

## ✅ Results
- IAM hierarchy working as intended.  
- Least-privilege principle enforced.  
- MFA successfully protects admin access.

---

## 🧠 Key Takeaways
- IAM is **global** – not region-specific.  
- Always use groups and roles instead of user-attached policies.  
- Combine IAM policies + MFA for strong security.

---

## 📚 References
- [AWS IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)  
- [Best Practices for IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
