# AWS Lab 44 – IAM Identity Center (SSO) + Permission Sets

## 📘 Overview
This lab configures AWS IAM Identity Center (SSO) to manage multi-account access using permission sets.

**Goal →** Centralize user login and access to multiple accounts via SSO.

---

## 🏗️ Architecture Diagram
```text
Identity Provider (IAM Identity Center)
          │
   Permission Sets
          │
AWS Accounts (via Organizations)
```

---

## 🚀 Steps Performed

### 1️⃣ Enable IAM Identity Center
Console → IAM Identity Center → Enable

---

### 2️⃣ Add Users (Internal Directory)
```
User: dhruvish
Email: your-email@example.com
```

---

### 3️⃣ Create Permission Set
Example: **AdministratorAccess**

Or create custom:
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "*",
    "Resource": "*"
  }]
}
```

---

### 4️⃣ Assign User to AWS Account
IAM Identity Center → Assign Users  
Select:
- User  
- Account  
- Permission Set  

---

### 5️⃣ Login via SSO Portal
Open:
```
https://<your-company>.awsapps.com/start
```

Sign in → Access assigned AWS accounts.

---

## 🧩 Verification
Check via CLI:
```bash
aws sso login --profile dev
aws sts get-caller-identity --profile dev
```

---

## 🧠 Key Takeaways
- IAM Identity Center = centralized access across accounts.  
- Permission Sets = policy bundles.  
- Integrates with Organizations for enterprise-level setup.
