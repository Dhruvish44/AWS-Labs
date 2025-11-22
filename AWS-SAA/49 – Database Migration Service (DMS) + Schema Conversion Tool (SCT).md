# AWS Lab 49 – Database Migration Service (DMS) + Schema Conversion Tool (SCT)

## 📘 Overview
This lab demonstrates a migration using:
- **AWS SCT** → Convert schema from source DB to target  
- **AWS DMS** → Perform continuous data replication (CDC)

**Goal →** Migrate a MySQL source database to **Amazon Aurora MySQL** with minimal downtime.

---

## 🏗️ Architecture Diagram
```text
On-Prem / EC2 MySQL DB
           │
         (SCT)
           │
        Schema Migrated
           │
          DMS
           │ (CDC + Full Load)
        Aurora MySQL
```

---

## 🚀 Steps Performed

### 1️⃣ Create Source Database (MySQL)
Launch EC2 → Install MySQL:

```bash
sudo yum install -y mariadb-server
sudo systemctl start mariadb
mysql -u root -e "CREATE DATABASE orders;"
```

Insert sample table:

```sql
CREATE TABLE orders.customers (
 id INT PRIMARY KEY AUTO_INCREMENT,
 name VARCHAR(50),
 country VARCHAR(50)
);
INSERT INTO orders.customers (name, country) VALUES ("Alice", "USA"), ("Karan", "India");
```

---

### 2️⃣ Deploy Aurora MySQL Cluster
```
Engine: Aurora MySQL
Cluster identifier: dhruvish-aurora
Instance Class: db.t3.medium
```

---

### 3️⃣ Use AWS SCT (Schema Conversion Tool)

- Source: MySQL
- Target: Aurora MySQL
- Convert schema → Apply to Aurora

---

### 4️⃣ Configure AWS DMS

Replication Instance:
```
Class: dms.t3.medium
Allocated Storage: 50GB
```

Endpoints:
- Source: MySQL host (EC2)
- Target: Aurora cluster endpoint

Migration Task:
```
Task Type: Full load + Change Data Capture (CDC)
Table mapping: Include all tables
```

Start task.

---

## 🧩 Verification

Check row count in Aurora:

```sql
SELECT COUNT(*) FROM orders.customers;
```

Add new record on source:

```sql
INSERT INTO orders.customers (name, country) VALUES ("Zara", "UK");
```

Check in Aurora → CDC should sync it.

---

## 🧠 Key Takeaways
- SCT migrates schema; DMS migrates data.  
- CDC enables near-zero-downtime cutover.  
- Ideal for heterogeneous migrations.
