# AWS Lab 47 – High Availability Web App (ALB + Auto Scaling + RDS Multi-AZ)

## 📘 Overview
Deploy a production-grade HA architecture across multiple AZs:
- ALB  
- Auto Scaling Group  
- Multi-AZ RDS  

**Goal →** Ensure failover at both compute and database layers.

---

## 🏗️ Architecture Diagram
```text
                 Internet
                     │
                    ALB
              ┌──────────────┐
              │              │
           EC2-A          EC2-B
           (AZ-a)         (AZ-b)
              │              │
              └── ASG Auto Replace
                     │
               RDS Multi-AZ
```

---

## 🚀 Steps Performed

### 1️⃣ Create Launch Template
```
AMI: Amazon Linux 2
User Data:
#!/bin/bash
echo "Hi from $(hostname)" > /var/www/html/index.html
yum install -y httpd && systemctl start httpd
```

---

### 2️⃣ Create Auto Scaling Group
```
VPC: default or custom
Subnets: AZ-a + AZ-b
Desired = 2
Min = 2
Max = 4
Health checks: EC2 + ALB
```

---

### 3️⃣ Create Application Load Balancer
```
Listener: HTTP:80
Target Group: dhruvish-tg
Health check path: /
```

Attach ASG → Target Group.

---

### 4️⃣ Create RDS Multi-AZ Instance
```
Engine: MySQL/Postgres
Multi-AZ: ENABLED
Storage: gp3
```

---

### 5️⃣ Connect EC2 → RDS
Install client:
```bash
sudo yum install -y mysql
```

Test connection:
```bash
mysql -h <rds-endpoint> -u admin -p
```

---

## 🧩 Verification

### Check ALB routing:
```
curl http://<alb-dns>
```

You should see alternating:
```
Hi from ip-xxx-xxx-xx
```

### Kill an EC2 instance:
```
aws ec2 terminate-instances --instance-ids <id>
```

ASG automatically replaces it.

### Test RDS failover:
Trigger failover:
```
aws rds reboot-db-instance --db-instance-identifier <id> --force-failover
```

---

## 🧠 Key Takeaways
- ALB ensures traffic distribution.  
- ASG maintains desired capacity.  
- RDS Multi-AZ provides automatic failover.
