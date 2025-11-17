# AWS Lab 28 – ECS Fargate Deployment (Serverless Containers)

## 📘 Overview
Deploy a containerized web app on **ECS Fargate**, using an Application Load Balancer (ALB) for public access.

**Goal →** Run containers without provisioning EC2 instances.

---

## 🏗️ Architecture Diagram
```text
                 Internet
                     │
               Application Load Balancer
                     │
           ┌─────────┴───────────┐
           ▼                     ▼
      Fargate Task 1       Fargate Task 2
           │                     │
          ECR ←──── stored Docker image ────→ ECR Repo
```

---

## 🚀 Steps Performed
```text
1️⃣ Create ECS Cluster
Cluster type: Networking only (Fargate)
Name: dhruvish-fargate
```

```text
2️⃣ Create Task Definition
Launch Type: Fargate
CPU: 256
Memory: 512
Network Mode: awsvpc
Container:
  - Image: <ECR_URI>/dhruvish-web:latest
  - Port: 80
Execution Role:
  - AmazonECSTaskExecutionRole
```

```text
3️⃣ Create Application Load Balancer
Type: Internet-facing
Listeners: HTTP:80
Target Group: fargate-tg (IP mode)
```

```text
4️⃣ Create ECS Service
Service: dhruvish-service
Tasks Desired: 2
Load Balancer: ALB + target group
Subnets: Public subnets
Assign public IP: ENABLED
```

---

## 🧩 Verification
Get ALB DNS:
```bash
aws elbv2 describe-load-balancers
```

Test in browser:
```
http://<ALB-DNS>
```

You should see:
```
Hello from ECR Deployment
```

---

## 🧠 Key Takeaways
- Fargate = serverless container compute.  
- No EC2, no patching, no scaling groups.  
- Best for microservices and APIs.  
