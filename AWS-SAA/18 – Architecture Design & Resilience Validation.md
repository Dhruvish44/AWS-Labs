# AWS Lab 18 – Architecture Design & Resilience Validation

## 📘 Overview
This lab tests the fault tolerance and recovery behavior of your ALB + ASG architecture.

---

## 🚀 Steps Performed
```text
1️⃣ Load Test
ab -n 2000 -c 100 http://<ALB-DNS>/
✅ Auto Scaling adds instances dynamically.
```

```text
2️⃣ Simulate Instance Failure
aws ec2 terminate-instances --instance-ids <InstanceID>
✅ ASG detects failure and replaces instance automatically.
```

```text
3️⃣ AZ Failure Simulation
- Disable one subnet → observe continued traffic flow.
✅ Multi-AZ ensures uptime.
```

```text
4️⃣ Review CloudWatch Metrics
CPUUtilization, RequestCount, HealthyHostCount
✅ Confirm scaling worked correctly.
```

---

## 🧠 Key Takeaways
- Multi-AZ + ASG = self-healing architecture.  
- Load balancer DNS never changes, even during scaling.  
- Real production apps follow this “stateless + scalable” pattern.
