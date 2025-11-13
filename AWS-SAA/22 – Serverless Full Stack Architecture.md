# AWS Lab 22 – Serverless Full Stack Architecture

## 📘 Overview
Combine API Gateway, Lambda, DynamoDB, and EventBridge into a full event-driven pipeline.

---

## 🚀 Steps Performed
```text
1️⃣ User submits form → API Gateway → Lambda
2️⃣ Lambda writes data → DynamoDB
3️⃣ DynamoDB stream triggers another Lambda → sends event to EventBridge
4️⃣ EventBridge rule → sends notification to SNS
✅ Complete event-driven chain operational.
```

```text
Test via API:
curl -X POST https://<api-id>.execute-api.ap-south-1.amazonaws.com/prod/users -d '{"name":"Dhruvish"}'
✅ Record stored in DynamoDB, event propagated.
```

---

## 🧠 Key Takeaways
- Entire app can run serverlessly.  
- EventBridge simplifies decoupled integrations.  
- Zero servers, zero downtime, global scalability.
