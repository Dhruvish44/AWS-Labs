# 🚀 Introduction to Amazon API Gateway  

**Lab Source:** AWS SkillBuilder  
**Format:** Hands-on Simulation with Console Walkthrough  
**Category:** Serverless & API Management  

---

## 📌 Overview  
In this lab, I created a **simple FAQ microservice** using **Amazon API Gateway** and **AWS Lambda**. The setup allowed me to:  

- Create a **Lambda function** running Node.js to return random FAQ responses.  
- Configure an **API Gateway REST endpoint** to invoke the Lambda function.  
- Debug and monitor using **Amazon CloudWatch**.  

This exercise demonstrated how **API Gateway transforms HTTP requests into JSON**, routes them securely via VPC, and integrates with Lambda for serverless microservice delivery.  

---

## 🎯 Objectives  
By the end of the lab, I was able to:  

- ✅ Create an AWS Lambda function with pre-written code.  
- ✅ Attach Lambda to a VPC, subnets, and security group.  
- ✅ Create and configure an API Gateway REST endpoint.  
- ✅ Test the integration using browser & console test events.  
- ✅ Debug API Gateway and Lambda with CloudWatch logs.  

---

## 🛠 Services Used  
- **Amazon API Gateway** – to define and deploy REST APIs.  
- **AWS Lambda** – to execute backend logic serverlessly.  
- **Amazon CloudWatch** – to capture logs and debug events.  
- **VPC, Subnets & Security Groups** – to secure the Lambda function.  

---

## 🔍 Key Learnings  

### 🔹 Amazon API Gateway  
- Converts HTTP requests into JSON for backend services.  
- Supports request/response transformation.  
- Allows **access control with IAM** and **API Keys**.  
- Integrates with **CloudWatch** for monitoring.  
- Can use **CloudFront caching** for faster responses.  

### 🔹 AWS Lambda  
- Serverless compute that runs code without managing servers.  
- Supports event-driven triggers (S3, DynamoDB, API Gateway, etc.).  
- Provides automatic scaling, built-in fault tolerance, and observability.  
- Must be stateless — any persistent data is stored in external services (S3, DynamoDB).  

---

## 🧪 Lab Tasks  

### **Task 1: Create Lambda Function**  
- Created a Lambda function named **FAQ**.  
- Runtime: **Node.js 18.x**.  
- Execution role: `lambda-basic-execution`.  
- Attached to VPC (CIDR: `10.0.0.0/16`) with subnets & security group.  
- Added pre-written JavaScript code to randomly return an FAQ.  

### **Task 2: Create API Gateway Endpoint**  
- Added **API Gateway Trigger** → REST API.  
- Configured deployment stage: `myDeployment`.  
- Created API endpoint: **FAQ-API**.  
- Set security: *Open* (no auth for lab).  

### **Task 3: Test & Debug**  
- Tested via browser using API Gateway endpoint → Random FAQ returned.  
- Created a console test event (`{}` as empty JSON).  
- Verified success in Lambda console logs.  
- Used **CloudWatch Logs** for debugging execution details.  

---

## ✅ Final Outcome  
Successfully built and tested a **serverless microservice** powered by **API Gateway + Lambda**.  
- API responded with dynamic JSON FAQs.  
- Debugged with CloudWatch logs.  
- Learned fundamentals of **REST API design**, Lambda integration, and secure VPC configuration.  

---

## 📂 Repository Mapping  

- `Introduction_to_Amazon_API_Gateway.md` → This writeup  
- `Introduction to Amazon API Gateway.pdf` → Official exported lab PDF
- 📄 **Lab PDF:** [View here](https://github.com/Dhruvish44/AWS-Labs/blob/main/Introduction%20to%20Amazon%20API%20Gateway.pdf)  

---

## 🚀 Next Steps  
- Add IAM-based authentication to API.  
- Move FAQs to **DynamoDB** for persistent storage.  
- Add methods for `GET /questions`, `POST /questions`, etc.  
- Deploy APIs with versioning (dev/test/prod stages).  

---

✍️ *Hands-on Proof-of-Work: Built, tested, and documented as part of my AWS security & serverless journey.*  
