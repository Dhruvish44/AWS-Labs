# AWS Lab 19 – Lambda + API Gateway REST API

## 📘 Overview
Deploy a REST API using API Gateway that triggers a Lambda function to return dynamic responses.

---

## 🚀 Steps Performed
```text
1️⃣ Create Lambda Function
Runtime: Python 3.9
Handler: lambda_function.lambda_handler
Code:
def lambda_handler(event, context):
    name = event.get("queryStringParameters", {}).get("name", "Dhruvish")
    return {
        "statusCode": 200,
        "body": f"Hello, {name}! from AWS Lambda"
    }
✅ Deploy function.
```

```text
2️⃣ Create API Gateway
- Type: HTTP API
- Integration: Lambda Function
- Routes: GET /hello
- Stage: prod
✅ Endpoint URL generated.
```

```text
3️⃣ Test API
curl https://<api-id>.execute-api.ap-south-1.amazonaws.com/prod/hello?name=Dhruvish
✅ Lambda executed successfully.
```

---

## 🧠 Key Takeaways
- API Gateway exposes Lambda as a REST API.  
- Fully serverless — no EC2 required.  
- Ideal for microservice APIs or backend integrations.
