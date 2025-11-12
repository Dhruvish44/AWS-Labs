# AWS Lab 16 – ALB + Auto Scaling Integration

## 📘 Overview
Deploy an ALB with an Auto Scaling Group behind it, ensuring high availability and dynamic scaling.

---

## 🚀 Steps Performed
```text
1️⃣ Create Launch Template
- EC2 → Launch Template → Define:
  AMI: Amazon Linux 2
  Instance Type: t2.micro
  Security Group: Allow HTTP (80)
  User Data:
    #!/bin/bash
    yum install -y httpd
    echo "Hello from $(hostname)" > /var/www/html/index.html
    systemctl start httpd
    systemctl enable httpd
✅ Template created.
```

```text
2️⃣ Create Target Group
- Name: dhruvish-tg
- Protocol: HTTP, Port 80
- Health Check Path: /
✅ Ready for load balancer integration.
```

```text
3️⃣ Create Application Load Balancer
- Scheme: Internet-facing
- Listener: HTTP:80 → Target Group: dhruvish-tg
✅ ALB DNS generated.
```

```text
4️⃣ Create Auto Scaling Group
- Launch Template: dhruvish-template
- VPC: default
- Subnets: Multi-AZ
- Target Group: dhruvish-tg
- Desired: 2, Min: 1, Max: 3
- Scaling Policy: CPU > 70% → Add instance
✅ Auto Scaling connected to ALB.
```

---

## 🧩 Verification
```bash
ab -n 1000 -c 50 http://<ALB-DNS>/
aws autoscaling describe-auto-scaling-groups
```

✅ Instances scale up/down automatically under load.

---

## 🧠 Key Takeaways
- ALB + ASG = High availability + fault tolerance.  
- Health checks automatically replace failed instances.  
- User data initializes instances at launch.
