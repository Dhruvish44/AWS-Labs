# AWS Lab 46 – ElastiCache Redis for Session Storage

## 📘 Overview
This lab deploys an ElastiCache Redis cluster and connects it to an EC2 instance as a session store.

**Goal →** Demonstrate low-latency caching for high performance.

---

## 🏗️ Architecture Diagram
```text
EC2 App → Redis Cluster → (Optional) RDS / API
```

---

## 🚀 Steps Performed

### 1️⃣ Create Redis Cluster
```
Cluster engine: Redis
Node type: cache.t3.micro
Single node (dev/test)
Multi-AZ: Enabled (production)
Encryption in transit: Enabled
```

---

### 2️⃣ Launch EC2 Instance
```
AMI: Amazon Linux 2
SG: Allow outbound to Redis SG
```

---

### 3️⃣ Install Redis CLI
SSH into EC2:
```bash
sudo yum install -y redis
```

---

### 4️⃣ Connect to Redis Cluster
```bash
redis-cli -h <redis-primary-endpoint>
```

Test:
```bash
set session:user123 "Dhruvish logged in"
get session:user123
```

---

### 5️⃣ Set TTL for Session Expiry
```bash
expire session:user123 3600
```

---

## 🧩 Verification
Check keys:
```bash
redis-cli -h <endpoint> keys '*'
```

---

## 🧠 Key Takeaways
- Redis supports persistence + multi-AZ failover.  
- Perfect for login sessions, caching, and real-time data.
