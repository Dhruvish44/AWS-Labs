# AWS Lab 43 – Amazon Inspector (EC2 & Container Scanning)

## 📘 Overview
Inspector scans EC2 instances, Lambda layers, and ECR container images for vulnerabilities (CVE-based).

**Goal →** Enable Inspector → Scan EC2 → Scan container images.

---

## 🏗️ Architecture Diagram
```text
EC2 / ECR Images → Inspector → Findings → Security Hub (optional)
```

---

## 🚀 Steps Performed

### 1️⃣ Enable Amazon Inspector
Console → Inspector → Enable

---

### 2️⃣ Scan EC2 Instances
Inspector automatically scans:
- Software versions  
- Network exposure  
- Known vulnerabilities  

Generate test finding:
```
Install outdated Apache/nginx
```

Inspector detects CVE vulnerability.

---

### 3️⃣ Scan ECR Images
Push a Docker image with known vulnerabilities:
```bash
docker pull nginx:1.14
docker tag nginx:1.14 <ECR_URI>/nginx:old
docker push <ECR_URI>/nginx:old
```

Inspector → Findings → Container Vulnerabilities

---

## 🧩 Verification
```bash
aws inspector2 list-findings
```

---

## 🧠 Key Takeaways
- Inspector = vulnerability scanning (EC2 + ECR).  
- Does NOT fix, only detects.  
- Auto-integrates with Security Hub.
