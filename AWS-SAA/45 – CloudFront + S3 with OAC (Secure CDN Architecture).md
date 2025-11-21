# AWS Lab 45 – CloudFront + S3 with OAC (Secure CDN Architecture)

## 📘 Overview
This lab configures CloudFront with an S3 origin **secured using Origin Access Control (OAC)** so S3 cannot be accessed publicly — only through CloudFront.

**Goal →** Build a secure, global CDN distribution with restricted origin access.

---

## 🏗️ Architecture Diagram
```text
Users → CloudFront (OAC Signed) → S3 (Private)
```

---

## 🚀 Steps Performed

### 1️⃣ Create S3 Bucket (Private)
```
Name: dhruvish-cloudfront-origin
Block Public Access: ENABLED
Versioning: Optional
```

Upload file:
```text
index.html
```

---

### 2️⃣ Create CloudFront Distribution
```
Origin: S3 bucket (private)
Viewer Protocol Policy: Redirect HTTP to HTTPS
Allowed Methods: GET, HEAD
Cache Policy: CachingOptimized
```

---

### 3️⃣ Configure Origin Access Control (OAC)
CloudFront → Origins → Create OAC

```
Signing Behavior: Sign requests
OAC Name: dhruvish-oac
```

Attach to CloudFront distribution.

---

### 4️⃣ Update S3 Bucket Policy (Auto-generated)
S3 gets a policy:
```json
{
  "Effect": "Allow",
  "Principal": {
    "Service": "cloudfront.amazonaws.com"
  },
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::dhruvish-cloudfront-origin/*",
  "Condition": {
    "StringEquals": {
      "AWS:SourceArn": "arn:aws:cloudfront::<account>:distribution/<id>"
    }
  }
}
```

---

### 5️⃣ Test Distribution
Open:
```
https://<cloudfront-domain>/
```

Try accessing S3 directly:
```
https://s3.amazonaws.com/dhruvish-cloudfront-origin/index.html
```
Should be **blocked**.

---

## 🧩 Verification
Check CloudFront access logs (if enabled):
```
GET /index.html 200
```

---

## 🧠 Key Takeaways
- OAC replaces OAI (newer, more secure).  
- S3 can only be accessed through CloudFront.  
- Best for secure global content delivery.
