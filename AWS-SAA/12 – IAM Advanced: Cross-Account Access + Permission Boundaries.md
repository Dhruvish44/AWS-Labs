# AWS Lab 12 – IAM Advanced: Cross-Account Access + Permission Boundaries

## 📘 Overview
This lab demonstrates **secure cross-account access** using IAM Roles and **permission boundaries** to restrict maximum allowed privileges.

**Goal →** Allow Account B to access Account A’s S3 bucket without creating IAM users in Account A.

---

## 🏗️ Architecture Diagram
```text
Account A (Resource Owner)        Account B (Requester)
┌────────────────────────────┐    ┌────────────────────────────┐
│ S3 Bucket: dhruvish-data   │ ←─ │ IAM Role: CrossAccountRole │
│ IAM Role + Trust Policy    │    │ IAM User: analyst          │
└────────────────────────────┘    └────────────────────────────┘
```

---

## 🚀 Steps Performed
```text
1️⃣ In Account A – Create IAM Role
- IAM → Roles → Create role → Another AWS Account
- Account ID: <Account B ID>
- Permissions: AmazonS3ReadOnlyAccess
- Role Name: CrossAccountRole

✅ Role created with trust to Account B.
```

```text
2️⃣ Edit Trust Policy
{
  "Version": "2012-10-17",
  "Statement": [{
      "Effect": "Allow",
      "Principal": {"AWS": "arn:aws:iam::<AccountB-ID>:root"},
      "Action": "sts:AssumeRole"
  }]
}
✅ Allows Account B to assume this role.
```

```text
3️⃣ In Account B – Assume the Role
aws sts assume-role \
--role-arn arn:aws:iam::<AccountA-ID>:role/CrossAccountRole \
--role-session-name crossaccountsession

✅ Temporary credentials issued by STS.
```

```text
4️⃣ Apply Permission Boundary (Account B)
{
  "Version": "2012-10-17",
  "Statement": [{
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::dhruvish-data/*"
  }]
}
✅ Limits access to only S3 read actions.
```

---

## 🧩 Verification Commands
```bash
aws s3 ls s3://dhruvish-data --profile crossaccountsession
aws sts get-caller-identity
```

---

## 🧠 Key Takeaways
- **Roles** are better than sharing access keys.  
- **Trust policies** define who can assume roles.  
- **Permission boundaries** prevent privilege escalation.  
- Cross-account access = secure + auditable with CloudTrail.
