# AWS Lambda & S3 Event-Driven Simulation  
**Author:** Dhruvish Rathod  
**Role:** SOC Analyst | Cloud Security Enthusiast  
**Date:** September 2025  

---

## 📌 Objective  
Create an **AWS Lambda function** to automatically resize images uploaded to an S3 bucket. Configure triggers, test the function, and monitor logs in CloudWatch.  

---

## 🛠 Tools & Services Used  
- **AWS Lambda** — Serverless compute  
- **Amazon S3** — Object storage + event trigger  
- **AWS IAM** — Execution role for Lambda  
- **Amazon CloudWatch** — Monitoring and logging  

---

## 🌐 Scenario Overview  
- Two buckets created:  
  - `images-<randomID>` for input  
  - `images-<randomID>-resized` for output  
- Lambda function `Create-Thumbnail` (Python 3.9) deployed with `lambda-execution-role`.  
- Function triggered on **S3 object-created event**.  
- Used Pillow library to resize images into **128x128 thumbnails**.  
- Logs and metrics monitored via CloudWatch.  

---

## 🔍 Findings  
- S3 bucket names must be globally unique.  
- IAM execution role required **S3 read/write permissions**.  
- Event JSON needed correct bucket and object key.  
- CloudWatch logs helped verify execution, memory usage, and errors.  

---

## 🛠 Remediation Steps  
1. Created input + output S3 buckets.  
2. Configured Lambda function with proper IAM role and VPC security group.  
3. Attached S3 trigger for object-created events.  
4. Validated execution with `HappyFace.jpg`.  
5. Monitored logs in CloudWatch for debugging and metrics.  

---

## ✅ Outcome  
- Successfully resized and stored images securely.  
- Demonstrated **event-driven compute model** in AWS.  
- Improved familiarity with **Lambda triggers + CloudWatch monitoring**.  

---

📄 **Lab PDF:** [View here](https://github.com/Dhruvish44/AWS-Labs/blob/main/Introduction%20to%20AWS%20Lambda.pdf)  
