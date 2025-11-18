# AWS Lab 32 – SNS Fan-Out: SNS → Multiple SQS → Lambda

## 📘 Overview
This lab implements the classic **fan-out architecture**:  
SNS publishes a message → multiple SQS queues receive → Lambdas process each independently.

---

## 🏗️ Architecture Diagram
```text
             SNS Topic
                │
     ┌──────────┴──────────┐
     ▼                     ▼
  SQS-A                 SQS-B
   │                     │
 Lambda-A             Lambda-B
```

---

## 🚀 Steps Performed
```text
1️⃣ Create SNS Topic
Name: dhruvish-topic
```

```text
2️⃣ Create Two SQS Queues
Queue A: analytics-queue
Queue B: email-queue
```

```text
3️⃣ Subscribe SQS Queues to SNS
SNS → Subscriptions → SQS
Confirm subscriptions.
```

```text
4️⃣ Create Two Lambda Functions
Lambda A → processes analytics queue  
Lambda B → sends email logs from queue  

Both functions:
- Runtime: Python 3.9
- IAM: Full SQS access
```

```text
5️⃣ Add Each SQS as Trigger for Each Lambda
SQS-A → Lambda-A  
SQS-B → Lambda-B  
```

```text
6️⃣ Publish Message to SNS Topic
aws sns publish \
--topic-arn <SNS_ARN> \
--message "Order Placed: #12345"
```

---

## 🧩 Verification
Check SQS queues:
```bash
aws sqs receive-message --queue-url <analytics-queue-url>
```

Tail Lambda logs:
```bash
aws logs tail /aws/lambda/LambdaA --follow
aws logs tail /aws/lambda/LambdaB --follow
```

---

## 🧠 Key Takeaways
- SNS delivers messages to *multiple consumers*.  
- SQS ensures messages aren’t lost.  
- Perfect for microservices & event broadcasting.  
