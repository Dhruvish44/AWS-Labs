# AWS Lab 26 – Hybrid Architecture: DX + VPN Backup + Transit Gateway

## 📘 Overview
This lab designs a full hybrid architecture using **Direct Connect (primary)**, **Site-to-Site VPN (backup)**, and **Transit Gateway** as the central routing hub.

**Goal →** Understand enterprise-level resiliency and high availability for hybrid workloads.

---

## 🏗️ Architecture Diagram
```text
                         On-Prem Data Center
                   ┌──────────────┬──────────────┐
                   │              │              │
           Direct Connect       VPN (IPsec)    OSPF/BGP Routing
                   │              │
                   ▼              ▼
            Direct Connect   Virtual Private Gateway
               Gateway           (VGW)
                   │              │
                   └──────┬──────┘
                          ▼
                AWS Transit Gateway (Hub)
           ┌──────────────┼──────────────┬──────────────┐
           ▼              ▼              ▼              ▼
       VPC-A          VPC-B          VPC-C        (More VPCs...)
```

---

## 🚀 Steps Performed
```text
1️⃣ Provision Direct Connect (Simulated)
Use DX Gateway + private VIF (console option).
```

```text
2️⃣ Create VPN Backup
Create Customer Gateway → Create VPN → Attach to TGW.
```

```text
3️⃣ Create Transit Gateway
Attach:
- DX Gateway
- VPN Attachment
- VPC Attachments (A/B/C)
```

```text
4️⃣ Configure Routing
TGW Route Table:
On-Prem Routes → DX Gateway (Primary)
Failover Route → VPN (Backup)

VPC Routes:
On-Prem CIDR → TGW
```

---

## 🧩 Verification
Failover Testing:
1. Disable DX (simulate outage).  
2. Verify traffic routes through VPN.

Commands:
```bash
traceroute <onprem-IP>
```

---

## 🧠 Key Takeaways
- DX provides **private, high-bandwidth** connectivity.  
- VPN provides **encrypted failover path**.  
- TGW provides **massive-scale routing hub**.  
- This is the **#1 enterprise hybrid pattern** in AWS.
