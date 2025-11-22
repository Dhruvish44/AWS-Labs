# AWS Lab 52 – Compute Optimization Analysis

## 📘 Overview
Analyze resource usage using AWS Compute Optimizer + Trusted Advisor and simulate Savings Plans scenario.

---

## 🏗️ Architecture Diagram
```text
Compute Optimizer → Trusted Advisor → Savings Plans recommendations
```

---

## 🚀 Steps Performed

### 1️⃣ Enable Compute Optimizer
```
Console → Compute Optimizer → Enable
```

---

### 2️⃣ Review Optimization Insights
Check:
- Over-provisioned EC2  
- Underutilized EBS volumes  
- Lambda memory recommendations  
- EKS compute efficiency  

---

### 3️⃣ Use Trusted Advisor
Check:
- Cost optimization  
- Security  
- Fault tolerance  
- Best practices  

---

### 4️⃣ Simulate Savings Plans Purchase
Cost Explorer → Savings Plans Recommendations

Choose:
```
Type: Compute Savings Plans
Term: 1 year
Payment: Partial Upfront
```

---

## 🧩 Verification

Download cost forecast:
```bash
aws ce get-cost-and-usage --time-period Start=2025-01-01,End=2025-01-31 --granularity MONTHLY --metrics "UnblendedCost"
```

---

## 🧠 Key Takeaways
- Savings Plans reduce compute cost up to 72%.  
- Compute Optimizer predicts right-sizing.  
- Trusted Advisor surfaces hidden cost waste.
