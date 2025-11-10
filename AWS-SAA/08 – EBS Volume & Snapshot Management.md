# AWS Lab 08 – EBS Volume & Snapshot Management

## 📘 Overview
Create, attach, back up, and restore EBS volumes.

---

## 🚀 Steps Performed
```text
1️⃣ Launch an EC2 instance (t2.micro)
2️⃣ Create EBS Volume (8 GB gp3) in same AZ
3️⃣ Attach Volume to Instance
sudo lsblk
sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data
✅ Volume mounted and usable.
```

```text
4️⃣ Create Snapshot
aws ec2 create-snapshot --volume-id <vol-id> --description "EBS backup"
✅ Snapshot stored in S3.
```

```text
5️⃣ Restore Volume from Snapshot
aws ec2 create-volume --snapshot-id <snap-id> --availability-zone ap-south-1a
✅ New volume restored and attached to new instance.
```

---

## 🧠 Key Takeaways
- EBS provides persistent block storage.  
- Snapshots enable backup and cross-region recovery.  
- Volumes are AZ-scoped.
