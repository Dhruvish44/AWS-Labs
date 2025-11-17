# AWS Lab 29 – ECS EC2 Cluster Deployment (Self-Managed Nodes)

## 📘 Overview
This lab deploys ECS using EC2 instances as worker nodes instead of Fargate.

**Goal →** Understand EC2-backed ECS clusters and agent behavior.

---

## 🏗️ Architecture Diagram
```text
                    ALB
                    │
               ECS Service
                    │
             ECS Tasks (Containers)
                    │
         ECS Agent on EC2 Instances
                    │
          Auto Scaling Group (EC2)
```

---

## 🚀 Steps Performed
```text
1️⃣ Create ECS Cluster
Cluster type: EC2 Linux + Networking
Instance type: t3.micro
Desired instances: 2
AMI: ECS-Optimized Amazon Linux 2
```

```text
2️⃣ Launch EC2 Instances
Instances automatically register with ECS via ecs-agent:
sudo systemctl status ecs
```

```text
3️⃣ Create Task Definition
Same as Fargate but launch type = EC2.
```

```text
4️⃣ Create ECS Service
Cluster: dhruvish-ec2-cluster
Service: dhruvish-ec2-service
Desired tasks: 2
Load Balancer: ALB
```

```text
5️⃣ Attached Target Group
Target type: instance
Port mapping: 80 → 80
```

---

## 🧩 Verification
Check if containers are running:
```bash
aws ecs list-tasks --cluster dhruvish-ec2-cluster
```

SSH into EC2 & check Docker containers:
```bash
docker ps
```

Check application:
```
http://<ALB-DNS>
```

---

## 🧠 Key Takeaways
- EC2 mode gives more control, but requires maintenance.  
- ECS Agent registers tasks on EC2 automatically.  
- ALB integrates smoothly with ECS EC2 target groups.  
