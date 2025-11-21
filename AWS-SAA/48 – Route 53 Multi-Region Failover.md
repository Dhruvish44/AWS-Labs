# AWS Lab 48 – Route 53 Multi-Region Failover

## 📘 Overview
Implement a **multi-region DR architecture** using Route 53 health checks and failover routing.

**Goal →** Automatically route traffic from Region A → Region B if Region A fails.

---

## 🏗️ Architecture Diagram
```text
           Route53 Hosted Zone
               /         \
Primary (Active)     Secondary (Passive)
Region A             Region B
ALB + ASG            ALB + ASG
```

---

## 🚀 Steps Performed

### 1️⃣ Deploy Application in Two Regions
Deploy your:
- ALB  
- ASG  
- EC2 web app  

in:
- **ap-south-1** (primary)  
- **us-east-1** (secondary)  

---

### 2️⃣ Create Health Check
Route53 → Health Checks

```
Type: HTTP
Endpoint: http://<Primary-ALB-DNS>/
Failure threshold: 3
```

---

### 3️⃣ Create DNS Records
Hosted Zone → Create:

### Primary (Active)
```
Type: A record (Alias)
Name: www.example.com
Alias target: Primary ALB
Routing Policy: Failover (PRIMARY)
Associate health check: YES
```

### Secondary (Passive)
```
Type: A record (Alias)
Name: www.example.com
Alias target: Secondary ALB
Routing Policy: Failover (SECONDARY)
```

---

### 4️⃣ Simulate Failure
Stop EC2 instances in primary region:
```
aws autoscaling update-auto-scaling-group \
--auto-scaling-group-name <ASG> \
--desired-capacity 0
```

Route53 will:
- Notice failure (via health check)
- Shift traffic to secondary region

---

## 🧩 Verification
Run:
```bash
curl http://www.example.com
```

It should now return content from:
```
Secondary Region
```

---

## 🧠 Key Takeaways
- Failover requires **health checks**.  
- Route53 supports multi-region DR natively.  
- Active–Passive is cheaper than Active–Active.
