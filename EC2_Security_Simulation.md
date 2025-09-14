# EC2 Security & Termination Protection – AWS Compute Simulation

**Author:** Dhruvish Rathod  
**Role:** SOC Analyst (Aspiring Cloud Security)  
**Date:** August 2025  

---

## 📌 Objective
Deploy and secure an EC2 instance in a simulated AWS environment. Key goals:  
- Launch with termination protection enabled  
- Configure security groups for least privilege  
- Monitor instance health using CloudWatch  
- Validate protection against accidental deletion  

---

## 🛠 Tools & Services Used
- **Amazon EC2 Console** – Instance management  
- **Amazon VPC + Security Groups** – Network isolation & firewall rules  
- **Amazon CloudWatch** – Instance monitoring  
- **AWS Systems Manager** – Secure management without SSH  

---

## 🌐 Scenario Overview
In a compute simulation, I launched a **Windows Server 2019 EC2 instance** (t2.micro).  
- **Tags:** Applied `Name=Web-Server` for identification.  
- **Termination Protection:** Enabled to prevent accidental deletion.  
- **Networking:** Deployed into `Lab VPC` with a public subnet.  
- **Security Group:** Configured HTTP (80) access only, blocked all others.  

---

## 🔍 Findings
1. Default security groups were overly permissive (`All traffic, all ports`).  
2. Termination protection was not enabled by default.  
3. Instance lacked fine-grained monitoring (CloudWatch not customized).  

---

## 🛠 Remediation Steps
### 1. Harden Security Group
```json
{
  "IpProtocol": "tcp",
  "FromPort": 80,
  "ToPort": 80,
  "CidrIp": "0.0.0.0/0"
}
```
Restricted inbound traffic to HTTP only.

Denied unrestricted SSH (port 22) access.

2. Enable Termination Protection

Prevented accidental deletion by enabling termination protection flag at launch.

3. Configure CloudWatch Monitoring

Activated detailed monitoring (1-min granularity).

Set alarms for CPU > 70% and failed status checks.

✅ Outcome

Reduced attack surface with tightened security groups.

Protected uptime by enabling termination protection.

Improved visibility with CloudWatch alarms.

📊 Lessons Learned

Default security groups are too broad — always customize.

Termination protection should be a standard safeguard.

Monitoring must be enabled early for production resilience.
