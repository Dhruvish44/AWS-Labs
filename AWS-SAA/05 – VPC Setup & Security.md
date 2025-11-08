# AWS Lab 05 – VPC Setup & Security

## 📘 Overview
This lab covers the creation of a custom **Virtual Private Cloud (VPC)**, subnets, route tables, Internet and NAT gateways, and endpoint configuration.  
You’ll learn how to control public and private connectivity in AWS.

**Goal →** Build a secure, isolated network with both public and private instances.

---

## 🏗️ Architecture Diagram
```text
VPC (10.0.0.0/16)
│
├── Public Subnet (10.0.1.0/24)
│     ├── EC2 Bastion Host (Public IP)
│     └── Internet Gateway (IGW)
│
└── Private Subnet (10.0.2.0/24)
      ├── EC2 App Server (No Public IP)
      ├── NAT Gateway (for outbound access)
      └── S3 VPC Endpoint (private AWS access)
```

---

## 🚀 Steps Performed
```text
1️⃣ Create a VPC

- Go to VPC → Create VPC
- Name: dhruvish-vpc-lab
- CIDR: 10.0.0.0/16
✅ Custom VPC created.
```

```text
2️⃣ Create Subnets

- Public Subnet: 10.0.1.0/24 (AZ1)
- Private Subnet: 10.0.2.0/24 (AZ1)
✅ Two logical network zones defined.
```

```text
3️⃣ Attach an Internet Gateway

- Create IGW → Attach to dhruvish-vpc-lab
- Edit Route Table → Add 0.0.0.0/0 → IGW
✅ Public subnet now has internet access.
```

```text
4️⃣ Launch EC2 in Public Subnet

- AMI: Amazon Linux 2, Type: t2.micro
- Enable Auto-assign Public IP
- Security Group: Allow SSH (22)
✅ Instance accessible via internet (acts as Bastion Host).
```

```text
5️⃣ Launch EC2 in Private Subnet

- Disable public IP
- Connect via Bastion Host:
  ssh -i dhruvish-key.pem ec2-user@<private-ip> -J ec2-user@<bastion-public-ip>
✅ Private instance accessible only internally.
```

```text
6️⃣ Add NAT Gateway (Private Subnet Internet Access)

- Create Elastic IP
- NAT Gateway → Public Subnet
- Update Private Subnet Route Table → 0.0.0.0/0 → NAT Gateway
✅ Private instances can now reach the internet securely.
```

```text
7️⃣ Create a VPC Endpoint (Private S3 Access)

- Service: com.amazonaws.<region>.s3
- Type: Gateway Endpoint
- Attach to Private Subnet route table
✅ Private EC2 can access S3 without using internet.
```

---

## 🔐 Security Layers
| Layer | Control | Purpose |
|:--|:--|:--|
| Network | NACLs | Subnet-level stateless rules |
| Instance | Security Groups | Stateful firewalls for EC2 |
| Internet | IGW / NAT Gateway | Controlled external access |
| Private Connectivity | VPC Endpoints | Secure AWS service access |

---

## 🧠 Key Takeaways
```text
- VPC is an isolated network in AWS.
- Public Subnets use IGW for internet access.
- Private Subnets use NAT Gateway for outbound-only access.
- Security Groups are stateful, NACLs are stateless.
- VPC Endpoints enable private AWS connectivity.
```

---

## 🧩 Verification Commands (CLI)
```bash
aws ec2 describe-vpcs
aws ec2 describe-subnets
aws ec2 describe-route-tables
aws ec2 describe-nat-gateways
aws ec2 describe-vpc-endpoints
```

---

## ✅ Results
- Custom VPC with public/private subnets deployed.
- Internet and NAT gateways functioning correctly.
- Bastion host enables secure private access.
- Private EC2 communicates with S3 via VPC Endpoint.
