# VPC & Network Security Audit – AWS Networking Simulation

**Author:** Dhruvish Rathod  
**Role:** SOC Analyst (Aspiring Cloud Security)  
**Date:** August 2025  

---

## 📌 Objective
Design and audit a Virtual Private Cloud (VPC) to ensure secure network segmentation, internet access control, and least privilege routing.

---

## 🛠 Tools & Services Used
- **Amazon VPC Console** – VPC, subnets, route tables  
- **Internet Gateway (IGW)** – External connectivity  
- **Route Tables** – Traffic flow control  
- **Security Groups** – Instance-level firewalls  

---

## 🌐 Scenario Overview
In the VPC simulation, I deployed:  
- **VPC:** `172.31.0.0/16` range  
- **Public Subnet:** `172.31.0.0/20` with auto-assign public IP  
- **Internet Gateway:** Attached for internet access  
- **Route Table:** Configured for `0.0.0.0/0 → IGW`  

---

## 🔍 Findings
1. **Default Security Group** allowed **all traffic (0.0.0.0/0)** inbound/outbound.  
2. No separation of **public vs private** subnets.  
3. Route table allowed **open internet access** without restrictions.  

---

## 🛠 Remediation Steps

### 1. Create Segmented Subnets
- Public Subnet: For web servers, assigned public IP.  
- Private Subnet: For databases, no direct internet exposure.  

---

### 2. Configure Route Tables
```json
{
  "DestinationCidrBlock": "0.0.0.0/0",
  "GatewayId": "igw-1234567890"
}
```
Public subnet routes internet traffic via IGW.

Private subnet routes only to NAT Gateway for outbound.

3. Harden Security Groups

Public subnet: Allowed inbound HTTP/HTTPS only.

Private subnet: Denied inbound internet, restricted to internal VPC CIDR.

✅ Outcome

Implemented segmented architecture (public vs private).

Reduced exposure risk by isolating sensitive workloads.

Achieved principle of least privilege for network traffic.

📊 Lessons Learned

Default VPCs are convenient but insecure for production.

Security groups must be service-specific, not blanket “allow all.”

Route tables + IGWs must be carefully scoped to prevent data leaks.
