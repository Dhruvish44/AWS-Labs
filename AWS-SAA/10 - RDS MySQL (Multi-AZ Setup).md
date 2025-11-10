# AWS Lab 10 – RDS MySQL (Multi-AZ Deployment)

## 📘 Overview
Launch a managed RDS database with Multi-AZ failover enabled.

---

## 🚀 Steps Performed
```text
1️⃣ Create RDS Instance
- Engine: MySQL
- DB Instance Class: db.t3.micro
- Storage: 20 GB gp3
- Multi-AZ: Enabled
- Public Access: No
```

```text
2️⃣ Set Credentials
- Master username: admin
- Password: ********
- VPC Security Group: Allow 3306 (MySQL)
✅ Instance launches and creates a standby in another AZ.
```

```text
3️⃣ Connect to RDS
mysql -h <endpoint> -u admin -p
SHOW DATABASES;
✅ Database accessible and auto-failover ready.
```

```text
4️⃣ Create Read Replica (optional)
- RDS → Create Read Replica → Target Region: same or different.
✅ Used for read scaling.
```

---

## 🧠 Key Takeaways
- RDS is fully managed relational database.  
- Multi-AZ = HA failover.  
- Read replicas scale reads horizontally.  
- Encryption and backups are automated.
