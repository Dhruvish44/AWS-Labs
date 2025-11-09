# AWS Lab 07 – CloudFront Distribution + Route 53 Domain Setup

## 📘 Overview
This lab creates a **CloudFront Distribution** to cache content from an S3 origin and configures a **custom domain** using Route 53.

---

## 🚀 Steps Performed
```text
1️⃣ Create an S3 Bucket (Origin)
- Bucket: dhruvish-cf-origin
- Upload index.html
- Disable public access
```

```text
2️⃣ Create CloudFront Distribution
- Origin: dhruvish-cf-origin.s3.amazonaws.com
- Viewer Protocol Policy: Redirect HTTP → HTTPS
- Cache TTL: 24 hours
- Restrict Bucket Access: Yes (Create OAI)
✅ Distribution Domain: dxxxx.cloudfront.net
```

```text
3️⃣ Test CloudFront
- Open CloudFront URL → Cached content delivered globally.
```

```text
4️⃣ Configure Route 53 (Custom Domain)
- Domain: dhruvishlab.com (or use any hosted zone)
- Create Record: A (Alias) → CloudFront Distribution
✅ Domain now resolves to CloudFront cached site.
```

```text
5️⃣ Optional: Add SSL Certificate
- Use AWS Certificate Manager (ACM)
- Attach certificate to CloudFront distribution
✅ HTTPS enabled for secure access.
```

---

## 🔐 Security Best Practices
| Control | Purpose |
|:--|:--|
| OAI | Restrict direct S3 bucket access |
| HTTPS | Secure data in transit |
| Route 53 Health Checks | Enable failover |
| TTL Optimization | Improve cache performance |
| Logging | Enable CloudFront access logs |

---

## 🧠 Key Takeaways
```text
- CloudFront speeds up global content delivery.
- OAI secures private S3 origins.
- Route 53 integrates seamlessly with CloudFront.
- HTTPS with ACM provides end-to-end encryption.
```
