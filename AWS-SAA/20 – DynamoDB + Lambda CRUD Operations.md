# AWS Lab 20 – DynamoDB + Lambda CRUD Operations

## 📘 Overview
Use Lambda to perform Create, Read, Update, and Delete operations on a DynamoDB table.

---

## 🚀 Steps Performed
```text
1️⃣ Create DynamoDB Table
Name: Users
Primary Key: userId (String)
✅ Table ready.
```

```text
2️⃣ Create Lambda Function
Runtime: Python 3.9
IAM Role: Allow DynamoDB full access
Code:
import boto3, json, uuid
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Users')

def lambda_handler(event, context):
    method = event['httpMethod']
    if method == 'POST':
        item = json.loads(event['body'])
        item['userId'] = str(uuid.uuid4())
        table.put_item(Item=item)
        return {'statusCode': 200, 'body': json.dumps(item)}
    elif method == 'GET':
        data = table.scan()
        return {'statusCode': 200, 'body': json.dumps(data['Items'])}
✅ Deploy and test.
```

```text
3️⃣ Connect via API Gateway
- Resource: /users
- Methods: GET, POST → Lambda integration
✅ Full CRUD via API.
```

---

## 🧠 Key Takeaways
- DynamoDB is fast, serverless storage.  
- Lambda + API Gateway = backend API with zero servers.  
- IAM roles control DB access securely.
