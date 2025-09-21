# Amazon DynamoDB Simulation  
**Author:** Dhruvish Rathod  
**Role:** SOC Analyst | Cloud Security Enthusiast  
**Date:** September 2025  

---

## 📌 Objective  
Practice NoSQL operations by creating a DynamoDB table, inserting data, querying items, updating entries, and finally deleting the table.  

---

## 🛠 Tools & Services Used  
- **Amazon DynamoDB** — NoSQL database  
- **AWS Management Console** — Table creation & queries  

---

## 🌐 Scenario Overview  
- Created table **Music** with `Artist` (Partition Key) and `Song` (Sort Key).  
- Inserted multiple records: *Pink Floyd – Money (1973)*, *John Lennon – Imagine (1971)*, *Psy – Gangnam Style (2011)*.  
- Modified `Psy` entry (updated year).  
- Queried by **Partition Key + Sort Key** for efficiency.  
- Performed a **scan** using filters (Year=1971).  
- Deleted the table at end of lab.  

---

## 🔍 Findings  
- DynamoDB’s schema-less nature allows each item to have unique attributes.  
- Queries are fast when using **primary + sort key**, scans are slower.  
- Easy to add attributes like `Album`, `Year`, or `LengthSeconds` dynamically.  

---

## 🛠 Remediation Steps  
1. Created table with defined keys.  
2. Added items with different attribute sets.  
3. Updated existing item values.  
4. Queried with partition + sort key and tested scan with filters.  
5. Deleted the table to clean up resources.  

---

## ✅ Outcome  
- Gained hands-on exposure to **DynamoDB CRUD operations**.  
- Understood differences between **query vs scan**.  
- Demonstrated DynamoDB’s flexibility for **unstructured data**.  

---

📄 **Lab PDF:** [View here](https://github.com/Dhruvish44/AWS-Labs/blob/main/Lab%20-%20Introduction%20to%20Amazon%20DynamoDB.pdf)  
