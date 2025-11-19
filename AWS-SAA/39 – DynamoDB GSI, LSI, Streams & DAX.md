# AWS Lab 39 – DynamoDB GSI, LSI, Streams & DAX

## 📘 Overview
This lab covers major DynamoDB performance and scalability features:
- GSI  
- LSI  
- Streams  
- DAX Acceleration  

---

## 🏗️ Architecture Diagram
```text
DynamoDB Table
   ├── GSI (query alternative keys)
   ├── LSI (sort within partitions)
   ├── Stream (change log)
   └── DAX (microsecond caching)
```

---

## 🚀 Steps Performed

### 1️⃣ Create DynamoDB Table
```
Table Name: Users
Partition Key: userId (String)
Sort Key: createdAt (Number)
Billing Mode: On-Demand
```

---

### 2️⃣ Add GSI
```
GSI Name: EmailIndex
Partition Key: email
Projection: ALL
```

---

### 3️⃣ Add LSI
(Must be created at table creation; recreate table if needed)
```
LSI Name: StatusIndex
Sort Key: status
```

---

### 4️⃣ Enable DynamoDB Streams
Mode: NEW_AND_OLD_IMAGES

Create Lambda to process stream events:
```python
def lambda_handler(event, context):
    print("Event:", event)
```

---

### 5️⃣ Deploy DAX Cluster
```
Cluster name: dhruvish-dax
Node count: 3
Node type: dax.t3.small
```

Update app SDK:
```python
from amazondax import AmazonDaxClient
dax = AmazonDaxClient(endpoints=['<dax-endpoint>'])
```

---

## 🧩 Verification

### Query GSI:
```bash
aws dynamodb query \
--table-name Users \
--index-name EmailIndex \
--key-condition-expression "email = :e" \
--expression-attribute-values '{":e":{"S":"test@example.com"}}'
```

### Check Streams Logs:
```bash
aws logs tail /aws/lambda/<stream-processor> --follow
```

---

## 🧠 Key Takeaways
- GSI = query by different partition key.  
- LSI = alternate sort key, same partition.  
- Streams + Lambda = event-driven DB.  
- DAX = microsecond read latency.  
