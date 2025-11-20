# AWS Lab 41 – AWS WAF + CloudFront Web Protection

## 📘 Overview
This lab configures AWS WAF to protect a CloudFront distribution against common web attacks (SQLi, XSS, IP blocking).

**Goal →** Attach WAF WebACL to CloudFront and apply managed + custom rules.

---

## 🏗️ Architecture Diagram
```text
User → CloudFront → WAF WebACL → S3 / ALB / API Gateway
```

---

## 🚀 Steps Performed

### 1️⃣ Create CloudFront Distribution
```
Origin: S3 bucket (public website)
Viewer Protocol: Redirect HTTP to HTTPS
```

---

### 2️⃣ Create WebACL
WAF → WebACL → Create

Settings:
```
Name: dhruvish-waf
Region: Global (for CloudFront)
```

---

### 3️⃣ Add Managed Rule Groups
Enable:
- AWSManagedRulesCommonRuleSet  
- SQLi Rule Set  
- BadBot Rule Set  

---

### 4️⃣ Add Custom IP Block Rule
```json
{
  "Name": "BlockBadIP",
  "Priority": 1,
  "Action": { "Block": {} },
  "Statement": {
    "IPSetReferenceStatement": {
      "ARN": "arn:aws:wafv2:...:ipset/BlockedIPs"
    }
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "BlockedIPs"
  }
}
```

---

### 5️⃣ Associate WebACL with CloudFront
WebACL → Associate Resource → CloudFront Distribution

---

## 🧩 Verification
Send test requests:
```bash
curl http://<CloudFrontDomain>?id=' OR 1=1 --
```
Result → Blocked.

Test blocked IP:
```bash
curl --interface <blocked-ip> https://<CloudFrontDomain>
```

---

## 🧠 Key Takeaways
- WAF protects HTTP/HTTPS layer (L7).  
- Attach WAF → CloudFront for global protection.  
- Combine managed + custom rules for best results.
