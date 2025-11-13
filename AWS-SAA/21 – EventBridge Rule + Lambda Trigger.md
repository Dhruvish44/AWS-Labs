# AWS Lab 21 – EventBridge Rule + Lambda Trigger

## 📘 Overview
Automate tasks using EventBridge rules to trigger Lambda functions based on scheduled or service events.

---

## 🚀 Steps Performed
```text
1️⃣ Create Lambda Function
Runtime: Python 3.9
Code:
def lambda_handler(event, context):
    print("Event Received:", event)
    return {"statusCode": 200}
✅ Deploy function.
```

```text
2️⃣ Create EventBridge Rule
- Type: Schedule expression
- cron(0/5 * * * ? *) → every 5 minutes
- Target: Lambda function
✅ Scheduled invocation created.
```

```text
3️⃣ Verify
Check CloudWatch Logs for Lambda output.
✅ Function triggered automatically every 5 minutes.
```

---

## 🧠 Key Takeaways
- EventBridge automates serverless workflows.  
- Rules can target any AWS service.  
- No manual cron jobs — fully managed scheduling.
