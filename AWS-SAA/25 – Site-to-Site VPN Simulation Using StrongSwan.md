# AWS Lab 25 – Site-to-Site VPN Simulation Using StrongSwan

## 📘 Overview
This lab simulates a **hybrid on-prem → AWS VPN connection** using an EC2 instance running StrongSwan as the **Customer Gateway (CGW)**.

**Goal →** Build an IPsec-encrypted tunnel between AWS and a simulated “on-prem” EC2 VM.

---

## 🏗️ Architecture Diagram
```text
             (Simulated On-Premises)
                   EC2-CGW
               StrongSwan VPN
                    │
                    │  (IPsec Tunnel)
                    ▼
     AWS Virtual Private Gateway (VGW)
                    │
                    ▼
                AWS VPC
```

---

## 🚀 Steps Performed
```text
1️⃣ Launch EC2 VM to simulate on-prem
AMI: Ubuntu
Install StrongSwan:
sudo apt update
sudo apt install -y strongswan
```

```text
2️⃣ Create Virtual Private Gateway
VPC → Create VGW
Attach VGW to your VPC.
```

```text
3️⃣ Create Customer Gateway
- IP address = EC2 public IP
- Routing: Static
```

```text
4️⃣ Create VPN Connection
VGW ↔ Customer Gateway
Download configuration file (StrongSwan).
```

```text
5️⃣ Configure StrongSwan
Edit:
 /etc/ipsec.conf  
 /etc/ipsec.secrets  

Use settings from AWS config file.
Restart service:
sudo systemctl restart strongswan
```

```text
6️⃣ Update VPC Route Table
Destination: CGW private network  
Target: VGW
```

---

## 🧩 Verification
```bash
ping <VPC-private-EC2-IP>   # from StrongSwan EC2
```

AWS side:
```bash
ping <onprem-private-IP>
```

---

## 🧠 Key Takeaways
- IPsec VPN encrypts traffic over public internet.  
- 2 tunnels provide redundancy.  
- Useful for hybrid cloud & data center extensions.  
- DX + VPN = enterprise-grade hybrid reliability.
