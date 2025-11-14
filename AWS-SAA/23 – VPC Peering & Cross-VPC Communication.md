# AWS Lab 23 – VPC Peering & Cross-VPC Communication

## 📘 Overview
This lab demonstrates how to create a secure **VPC Peering connection** between two VPCs and enable private communication between EC2 instances across VPCs.

**Goal →** Connect VPC-A and VPC-B in the same region and verify bidirectional access using private IPs.

---

## 🏗️ Architecture Diagram
```text
              VPC Peering Connection (pcx-12345)
    ┌───────────────────────────┐       ┌───────────────────────────┐
    │         VPC-A             │ ←────→│         VPC-B             │
    │  CIDR: 10.0.0.0/16        │       │  CIDR: 10.1.0.0/16        │
    │  EC2-A: 10.0.1.10         │       │  EC2-B: 10.1.1.10         │
    └───────────────────────────┘       └───────────────────────────┘
```

---

## 🚀 Steps Performed
```text
1️⃣ Create VPC-A
CIDR: 10.0.0.0/16
Public Subnet: 10.0.1.0/24
Launch EC2-A in subnet.
```

```text
2️⃣ Create VPC-B
CIDR: 10.1.0.0/16
Public Subnet: 10.1.1.0/24
Launch EC2-B in subnet.
```

```text
3️⃣ Create VPC Peering
VPC-A → VPC-B
Accept request from VPC-B side.
```

```text
4️⃣ Update Route Tables
VPC-A Route Table:
10.1.0.0/16 → pcx-<id>

VPC-B Route Table:
10.0.0.0/16 → pcx-<id>
```

```text
5️⃣ Allow Traffic in Security Groups
Add inbound rule:
Type: ALL ICMP → allow ping testing
Type: SSH → allow from other VPC’s CIDR
```

---

## 🧩 Verification
SSH into EC2-A:
```bash
ping 10.1.1.10
ssh ec2-user@10.1.1.10
```

SSH into EC2-B:
```bash
ping 10.0.1.10
ssh ec2-user@10.0.1.10
```

---

## 🧠 Key Takeaways
- VPC Peering is **non-transitive**.  
- CIDR blocks must **not overlap**.  
- Both route tables must be updated.  
- Great for small multi-VPC architectures.
