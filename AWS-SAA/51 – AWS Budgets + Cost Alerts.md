# AWS Lab 51 – AWS Budgets + Cost Alerts

## 📘 Overview
Create spending controls using AWS Budgets and alert via email when thresholds exceed.

---

## 🏗️ Architecture Diagram
```text
Cost Monitoring → Budget Rule → SNS Email Alert
```

---

## 🚀 Steps Performed

### 1️⃣ Create SNS Topic for Alerts
```
Topic: billing-alerts
Subscription: Email
```

---

### 2️⃣ Create Cost Budget
AWS Budget → Create

```
Type: Cost Budget
Limit: ₹1000/month
Alert: When forecast > 80%
Notify: SNS Topic billing-alerts
```

---

### 3️⃣ Enable Cost Explorer
```
AWS Cost Explorer → Enable
```

---

## 🧩 Verification

Trigger test budget email:
```
Budgets → Send Test Notification
```

Expected email:
```
AWS Billing Alert: Cost threshold exceeded.
```

---

## 🧠 Key Takeaways
- Budgets = alerts  
- Cost Explorer = trend analysis  
- SNS enables automation (ticket, Lambda, Slack).
