# AWS Lab 03 – AWS Security Basics (CloudTrail, Config, KMS & Monitoring)

## 📘 Overview
This lab demonstrates how to implement **core AWS security and monitoring services** — CloudTrail, AWS Config, and KMS — to ensure visibility, auditability, and data protection.  
**Goal →** Set up a foundational security baseline that logs activity, tracks resource changes, and encrypts data at rest.

---

## 🧱 Architecture Diagram
```text
+-------------------------------------------------------------+
|                     AWS Security Stack                      |
|-------------------------------------------------------------|
| CloudTrail → Logs every API call (saved to S3)              |
| Config     → Tracks configuration changes and compliance    |
| CloudWatch → Monitors metrics and creates alarms            |
| KMS        → Encrypts data across AWS services              |
| IAM        → Manages access (with MFA)                      |
+-------------------------------------------------------------+
```

---

## 🚀 Steps Performed
```text
1️⃣ Enable CloudTrail (Audit All API Calls)

- Navigate to AWS CloudTrail → Trails → Create trail.
- Name it `dhruvish-trail`.
- Choose “Apply to all regions.”
- Create a new S3 bucket → `dhruvish-cloudtrail-logs`.
- Enable Log file validation for integrity checks.
- Perform a few AWS actions (e.g., create S3 bucket, IAM user).
- Open the S3 bucket → verify CloudTrail logs have been delivered.

✅ Result: Every API action (who, when, where, what) is now recorded.
```

```text
2️⃣ Enable AWS Config (Track Configuration Changes)

- Open AWS Config → Get Started.
- Choose “Record all resources supported in this region.”
- Create S3 bucket → `dhruvish-config-logs`.
- Enable delivery channel → same bucket.
- Wait for initial scan → view Timeline to confirm tracking.

✅ Result: Any resource change (e.g., disabling encryption) will be detected.
```

```text
3️⃣ Create and Use a KMS Key (Encrypt Data at Rest)

- Navigate to AWS KMS → Customer Managed Keys → Create key.
- Select Symmetric Key, alias it `dhruvish-kms-key`.
- Assign key usage permission to your IAM admin user.
- Go to your S3 bucket → Enable Default Encryption → KMS → Select `dhruvish-kms-key`.
- Upload a new file to confirm encryption.

✅ Result: All new S3 uploads are automatically encrypted with your custom KMS key.
```

```text
4️⃣ Configure CloudWatch Alarms for Security Monitoring

- Go to CloudWatch → Alarms → Create alarm.
- Choose a metric: `S3 → 4xxErrors`.
- Set threshold: “Greater than 10 for 5 minutes.”
- Create an SNS topic → `SecurityAlerts`.
- Subscribe your email to the topic.

✅ Result: If excessive access errors occur, you’ll get an alert email.
```

```text
5️⃣ Run IAM Access Analyzer (Public Resource Detection)

- Go to IAM → Access Analyzer → Create Analyzer.
- Choose your region and name it `DhruvishAnalyzer`.
- Wait for scan results.
- If any S3 bucket or role is public → review and restrict access.

✅ Result: IAM Access Analyzer confirms that no resources are publicly exposed.
```

---

## 🔐 Security Controls Implemented
| Control | Service | Purpose |
|:--|:--|:--|
| Activity Logging | CloudTrail | Record all API actions |
| Configuration Recording | AWS Config | Detect configuration drift |
| Data Encryption | KMS | Encrypt S3, EBS, and other resources |
| Monitoring & Alerts | CloudWatch + SNS | Notify on abnormal activity |
| Public Access Detection | IAM Access Analyzer | Identify exposed resources |
| Least Privilege | IAM | Enforce minimal permissions |

---

## 🧠 Key Concepts Reinforced
```text
CloudTrail = “Who did what”
Config = “What changed and when”
KMS = “Encrypt everything”
CloudWatch = “Detect and alert”
IAM Analyzer = “Prevent exposure”

✅ Together they form your AWS Security Foundation Layer.
```

---

## ✅ Results
```text
- CloudTrail logs centralized in S3 bucket.
- Config monitors real-time resource changes.
- Custom KMS key protects stored data.
- CloudWatch alarms alert on anomalies.
- Access Analyzer confirms privacy compliance.
```

---

## 🧩 Verification Commands (CLI)
```bash
# Verify CloudTrail
aws cloudtrail describe-trails

# Check Config status
aws configservice describe-configuration-recorders

# List KMS keys
aws kms list-keys

# Get CloudWatch alarms
aws cloudwatch describe-alarms

# Check Access Analyzer findings
aws accessanalyzer list-findings
```

---

## 🧠 Key Takeaways
```text
- Always enable CloudTrail + Config in all regions.
- Use KMS for all encryption needs (S3, EBS, RDS, EFS, etc.).
- Automate alerts with CloudWatch Alarms.
- Regularly run Access Analyzer for exposure checks.
- Security = Visibility + Control + Continuous Monitoring.
```

---

## 📚 References
- AWS CloudTrail Documentation: https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html
- AWS Config Documentation: https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html
- AWS KMS User Guide: https://docs.aws.amazon.com/kms/latest/developerguide/overview.html
- AWS CloudWatch Overview: https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html

