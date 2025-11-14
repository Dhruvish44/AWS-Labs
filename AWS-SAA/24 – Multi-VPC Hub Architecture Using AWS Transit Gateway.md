# AWS Lab 24 – Multi-VPC Hub Architecture Using AWS Transit Gateway

## 📘 Overview
This lab connects **three VPCs** to a **Transit Gateway**, enabling **transitive routing** and simplified multi-VPC communication.

**Goal →** Use TGW as a central router to connect VPC-A, VPC-B, and VPC-C automatically.

---

## 🏗️ Architecture Diagram
```text
                      ┌──────────────────────────┐
                      │      Transit Gateway      │
                      │        (tgw-12345)        │
                      └─────────┬─────────┬───────┘
                                │         │
              ┌─────────────────┘         └──────────────────┐
              ▼                                               ▼
      ┌───────────────┐                               ┌───────────────┐
      │    VPC-A       │                               │    VPC-B       │
      │ 10.0.0.0/16    │                               │ 10.1.0.0/16    │
      └───────────────┘                               └───────────────┘
                        ▼
               ┌───────────────┐
               │    VPC-C       │
               │ 10.2.0.0/16    │
               └───────────────┘
```

---

## 🚀 Steps Performed
```text
1️⃣ Create 3 VPCs
VPC-A: 10.0.0.0/16
VPC-B: 10.1.0.0/16
VPC-C: 10.2.0.0/16
Launch EC2s in each.
```

```text
2️⃣ Create Transit Gateway
Name: dhruvish-tgw
ASN: default
```

```text
3️⃣ Attach Each VPC to TGW
TGW → Create VPC Attachment → Choose VPC-A
Repeat for B and C.
```

```text
4️⃣ Edit TGW Route Table
Add routes:
10.0.0.0/16 → tgw-attach-A
10.1.0.0/16 → tgw-attach-B
10.2.0.0/16 → tgw-attach-C
```

```text
5️⃣ Update VPC Route Tables
For each VPC:
Other VPC CIDR → tgw-<id>
```

---

## 🧩 Verification
From EC2-A:
```bash
ping 10.1.1.10
ping 10.2.1.10
```

From EC2-B:
```bash
ping 10.0.1.10
```

All cross-VPC pings should work.

---

## 🧠 Key Takeaways
- TGW allows **transitive routing**.  
- Supports **hundreds of VPCs**.  
- Best for multi-account, multi-VPC architectures.  
- Unlike VPC peering, TGW **scales massively**.
