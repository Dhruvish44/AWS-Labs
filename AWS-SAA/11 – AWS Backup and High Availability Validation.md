# AWS Lab 11 – AWS Backup and High Availability Validation

## 📘 Overview
Centralize backups for EBS, EFS, and RDS and test HA failover.

---

## 🚀 Steps Performed
```text
1️⃣ Open AWS Backup
- Create Backup Vault: dhruvish-vault
- Create Backup Plan: daily-backup-plan
- Frequency: Daily @ 00:00 UTC
```

```text
2️⃣ Assign Resources
- Add EBS, EFS, RDS to backup plan.
✅ Automatic scheduled backups enabled.
```

```text
3️⃣ Test Restoration
- Delete EBS volume → Restore from Backup Vault.
- Simulate EC2 failure → Recover AMI from snapshot.
✅ Data intact and restored successfully.
```

```text
4️⃣ Validate HA
- Stop primary RDS → failover to secondary.
✅ Minimal downtime and automatic recovery.
```

---

## 🧠 Key Takeaways
- AWS Backup unifies backup management.  
- Multi-AZ design prevents single-AZ failure.  
- Snapshots + Replication = Disaster Recovery readiness.
