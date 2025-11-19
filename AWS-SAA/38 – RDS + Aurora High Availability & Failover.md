# AWS Lab 38 – RDS + Aurora High Availability & Failover

## 📘 Overview
This lab creates:
- RDS MySQL Multi-AZ instance  
- Aurora MySQL cluster (1 writer + 1 reader)  

Then performs **failover tests**.

---

## 🏗️ Architecture Diagram
```text
RDS Multi-AZ
  │
  ├── Primary Instance (AZ-a)
  └── Standby Instance (AZ-b)

Aurora Cluster
  ├── Writer Endpoint
  ├── Reader Endpoint (LB)
  └── Replicas
```

---

## 🚀 Steps Performed

### 1️⃣ RDS Multi-AZ Setup
```
Engine: MySQL
Instance Class: db.t3.micro
Storage: gp3
Multi-AZ: Enabled
Backup: 7 days
```

RDS automatically provisions:
- Primary (AZ a)
- Standby (AZ b)

---

### 2️⃣ Aurora Cluster Setup
```
Engine: Aurora MySQL
Cluster: dhruvish-aurora
Writer: 1 instance
Reader: 1 instance
Backtrack: Enabled
```

---

### 3️⃣ Test Read Scaling
Connect:
```bash
mysql -h <reader-endpoint>
SELECT COUNT(*) FROM information_schema.tables;
```

---

### 4️⃣ Perform Failover (Aurora)
Console → Failover  
Or CLI:
```bash
aws rds failover-db-cluster --db-cluster-identifier dhruvish-aurora
```

Writer → Reader swap.

---

### 5️⃣ Perform Failover (RDS Multi-AZ)
Reboot with failover:
```bash
aws rds reboot-db-instance \
--db-instance-identifier dhruvish-rds \
--force-failover
```

---

## 🧩 Verification
Check new writer:
```bash
aws rds describe-db-clusters --db-cluster-identifier dhruvish-aurora
```

Check RDS instance:
```bash
aws rds describe-db-instances
```

---

## 🧠 Key Takeaways
- Multi-AZ = HA, not scaling.  
- Read Replicas = scaling, not HA.  
- Aurora separates compute + storage → instant failover.  
