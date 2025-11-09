# AWS Lab 06 – S3 Static Website Hosting + Transfer Acceleration

## 📘 Overview
This lab sets up an S3 bucket for **static website hosting**, enables **versioning**, and configures **Transfer Acceleration** for faster global access.

---

## 🚀 Steps Performed
```text
1️⃣ Create S3 Bucket
- Name: dhruvish-static-site
- Region: ap-south-1
- Block Public Access: OFF
- Enable Versioning
```

```text
2️⃣ Upload Website Files
- index.html
- error.html
```

```text
3️⃣ Enable Static Website Hosting
- Properties → Static website hosting → Enable
- Index document: index.html
- Error document: error.html
✅ Public endpoint generated (e.g. http://dhruvish-static-site.s3-website-ap-south-1.amazonaws.com)
```

```text
4️⃣ Enable Transfer Acceleration
- Go to “Properties” → Enable “Transfer Acceleration”
✅ Test upload speed improvement via:
  bucketname.s3-accelerate.amazonaws.com
```

```text
5️⃣ Enable Logging and Lifecycle
- Enable Access Logs (store in separate log bucket)
- Add Lifecycle Rule: Move objects to S3-IA after 30 days
```

---

## 🧠 Key Takeaways
```text
- S3 can host static websites directly.
- Versioning protects from accidental overwrite/deletion.
- Transfer Acceleration uses AWS edge network for speed.
- Lifecycle rules optimize storage cost.
```
