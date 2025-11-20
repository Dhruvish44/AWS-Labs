# AWS Lab 42 – GuardDuty + Security Hub Integration

## 📘 Overview
Enable GuardDuty for threat detection and integrate it with Security Hub for centralized security visibility.

**Goal →** Detect anomalies and aggregate findings in Security Hub.

---

## 🏗️ Architecture Diagram
```text
CloudTrail / VPC Flow Logs / DNS Logs
         │
     GuardDuty
         │
   Security Hub
         │
   Insights / Compliance
```

---

## 🚀 Steps Performed

### 1️⃣ Enable GuardDuty
Console → GuardDuty → Enable

Sources automatically included:
- CloudTrail  
- VPC Flow Logs  
- DNS logs  

---

### 2️⃣ Generate Sample Finding (built-in)
GuardDuty → Settings → Generate Sample Findings

---

### 3️⃣ Enable Security Hub
Console → Security Hub → Enable

Enable standards:
- AWS Foundational Security Best Practices  
- CIS AWS Foundations  
- PCI DSS (optional)

---

### 4️⃣ Integrate GuardDuty with Security Hub
Security Hub → Integrations → GuardDuty → Enable

---

## 🧩 Verification

### Check GuardDuty findings:
```bash
aws guardduty list-findings --detector-id <detector>
```

### Check Security Hub findings:
```bash
aws securityhub get-findings
```

---

## 🧠 Key Takeaways
- GuardDuty = threat detection (no blocking).  
- Security Hub = central security dashboard.  
- Sample findings help validate detection pipeline.
