# AWS Lab 31 – SQS Queue + Lambda Worker (Decoupling)

## 📘 Overview
This lab demonstrates how to decouple a producer and consumer using **SQS + Lambda**.  
Messages are pushed to SQS → Lambda pulls them → processes them asynchronously.

---

## 🏗️ Architecture Diagram
```text
Producer → SQS Queue → Lambda Worker → DynamoDB / Logs
```

---

## 🚀 Steps Performed
```text
1️⃣ Create SQS Queue
Type: Standard
Name: dhruvish-queue
Visibility Timeout: 30 sec
Message Retention: 4 days
Receive Wait Time: 20 sec (long polling)
```

```text
2️⃣ Create Lambda Function
Runtime: Python 3.9
IAM Role: SQS full access + CloudWatch logs

Code:
import json

def lambda_handler(event, context):
    for record in event['Records']:
        msg = record['body']
        print("Processing message:", msg)
    return {"statusCode": 200}
```

```text
3️⃣ Add SQS Trigger to Lambda
SQS → Lambda integration
Batch size: 1
```

```text
4️⃣ Send Messages to Queue
aws sqs send-message \
--queue-url <QUEUE_URL> \
--message-body "Hello from SQS"
```

---

## 🧩 Verification
Check Lambda logs:
```bash
aws logs tail /aws/lambda/<function-name> --follow
```

You should see:
```
Processing message: Hello from SQS
```

---

## 🧠 Key Takeaways
- SQS protects systems from overload.  
- Lambda pulls messages automatically.  
- Visibility Timeout prevents double-processing.  
