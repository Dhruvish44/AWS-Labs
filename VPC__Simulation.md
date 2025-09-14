# Amazon VPC Security & Networking Simulation  
**Author:** Dhruvish Rathod  
**Role:** SOC Analyst | Cloud Security Enthusiast  
**Date:** September 2025  

---

## 📌 Objective  
Design a **Virtual Private Cloud (VPC)** with public and private subnets, attach an internet gateway, configure route tables, and secure access with network ACLs.  

---

## 🛠 Tools & Services Used  
- **Amazon VPC** — Networking environment  
- **Internet Gateway** — Public access  
- **NAT Gateway** — Outbound internet access from private subnet  
- **Network ACLs & Security Groups** — Firewall rules  

---

## 🌐 Scenario Overview  
- Created a VPC with **1 public subnet + 1 private subnet**.  
- Configured **CIDR blocks**:  
  - Public: `10.0.25.0/24`  
  - Private: `10.0.50.0/24`  
- Added **Internet Gateway** for public subnet access.  
- Configured **NAT Gateway** for private subnet outbound access.  

---

## 🔍 Findings  
- Public subnet had a route to Internet Gateway → accessible from internet.  
- Private subnet only had route via NAT Gateway → no direct inbound from internet.  
- Default Security Group allowed full self-referencing traffic, but denied external by default.  

---

## 🛠 Remediation Steps  
1. Created VPC with isolated subnets.  
2. Configured **route tables** for internet vs private routing.  
3. Verified ACLs to enforce default deny for unlisted traffic.  
4. Documented resource IDs and VPC diagram.  

---

## ✅ Outcome  
- Established secure VPC baseline with least-exposure principles.  
- Demonstrated understanding of **subnet isolation** and **controlled routing**.  
- Added multi-tier architecture foundation for future cloud deployments.  

---

## 📄 Lab PDF  
[View here](./AWS_VPC_Lab.pdf)
