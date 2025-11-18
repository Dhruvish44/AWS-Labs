# AWS Lab 34 – EventBridge Event Bus + Routing Rules + Lambda

## 📘 Overview
This lab demonstrates **event-driven microservice routing** using EventBridge.  
An event is sent → EventBridge filters it → routes to specific Lambda functions.

---

## 🏗️ Architecture Diagram
```text
Producer → EventBridge Bus → Rule (Filter) → Lambda → Logs / DB
```

---

## 🚀 Steps Performed
```text
1️⃣ Create Custom Event Bus
Name: dhruvish-bus
```

```text
2️⃣ Create Lambda Consumer
Runtime: Python 3.9
Code:
def lambda_handler(event, context):
    print("Event Received:", event)
```

```text
3️⃣ Create EventBridge Rule
Event Pattern Example:
{
  "source": ["app.orders"],
  "detail-type": ["orderCreated"],
  "detail": {
    "status": ["PAID"]
  }
}

Target: Lambda function
```

```text
4️⃣ Send Event to Custom Bus
aws events put-events --entries '[
{
  "Source": "app.orders",
  "DetailType": "orderCreated",
  "Detail": "{\"status\": \"PAID\", \"orderId\": 987}",
  "EventBusName": "dhruvish-bus"
}
]'
```

---

## 🧩 Verification
Check Lambda logs:
```bash
aws logs tail /aws/lambda/<lambda-name> --follow
```

Expected:
```
Event Received: {"detail": {"status": "PAID", "orderId": 987}}
```

---

## 🧠 Key Takeaways
- EventBridge = intelligent event router.  
- Advanced filtering allows targeting specific microservices.  
- Ideal for microservice architectures.  
