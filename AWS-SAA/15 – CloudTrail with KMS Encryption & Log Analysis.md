# AWS Lab 15 – CloudTrail with KMS Encryption & Log Analysis

## 📘 Overview
This lab configures CloudTrail for **organization-wide API auditing**, integrates **KMS encryption**, and demonstrates log analysis using Athena.

**Goal →** Track who did what in AWS and secure logs at rest.

---

## 🚀 Steps Performed
```text
1️⃣ Enable CloudTrail
aws cloudtrail create-trail \
--name dhruvish-org-trail \
--s3-bucket-name dhruvish-trail-logs \
--is-multi-region-trail

✅ Trail applies to all regions and delivers logs to S3.
```

```text
2️⃣ Enable Log File Validation
aws cloudtrail update-trail --name dhruvish-org-trail --enable-log-file-validation
✅ Ensures logs aren’t tampered with.
```

```text
3️⃣ Enable KMS Encryption
aws cloudtrail update-trail \
--name dhruvish-org-trail \
--kms-key-id alias/dhruvish-key
✅ Logs now encrypted using CMK.
```

```text
4️⃣ Send Events to CloudWatch Logs
aws cloudtrail update-trail \
--name dhruvish-org-trail \
--cloud-watch-logs-log-group-arn <LOG-GROUP-ARN> \
--cloud-watch-logs-role-arn <ROLE-ARN>
✅ Real-time event monitoring enabled.
```

```text
5️⃣ Query CloudTrail Logs via Athena
- Go to Athena → Create Table from S3 Logs.
- Run:
SELECT eventname, useridentity.username, eventtime
FROM cloudtrail_logs
WHERE eventname LIKE '%Delete%'
ORDER BY eventtime DESC;
✅ Lists recent delete operations.
```

---

## 🧩 Verification
```bash
aws cloudtrail describe-trails
aws cloudtrail get-event-selectors --trail-name dhruvish-org-trail
aws cloudtrail lookup-events --lookup-attributes AttributeKey=EventName,AttributeValue=DeleteBucket
```

---

## 🧠 Key Takeaways
- CloudTrail records all API actions across AWS.  
- Logs should always be encrypted with KMS.  
- Integration with CloudWatch + Athena gives real-time and query-based insights.  
- Essential for audits, incident response, and compliance.
