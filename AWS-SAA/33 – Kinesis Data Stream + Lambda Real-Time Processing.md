# AWS Lab 33 – Kinesis Data Stream + Lambda Real-Time Processing

## 📘 Overview
This lab demonstrates a real-time data ingestion pipeline using **Kinesis Data Streams → Lambda**.

**Goal →** Process streaming events with sub-second latency.

---

## 🏗️ Architecture Diagram
```text
Producers → Kinesis Stream → Lambda Processor → S3 / Logs / DynamoDB
```

---

## 🚀 Steps Performed
```text
1️⃣ Create Kinesis Data Stream
Name: dhruvish-stream
Shards: 1 (1MB/s write, 2MB/s read)
Retention: 24 hours
```

```text
2️⃣ Create Lambda Function
Runtime: Python 3.9
IAM: Kinesis read + CloudWatch logs

Code:
def lambda_handler(event, context):
    for record in event['Records']:
        payload = record["kinesis"]["data"]
        print("Decoded Data:", payload)
    return {"statusCode": 200}
```

```text
3️⃣ Add Kinesis Trigger to Lambda
Batch size: 100 records
Max batching window: 1 sec
```

```text
4️⃣ Put Sample Events into Kinesis
aws kinesis put-record \
--stream-name dhruvish-stream \
--data "Hello Stream" \
--partition-key 1
```

---

## 🧩 Verification
Tail Lambda logs:
```bash
aws logs tail /aws/lambda/<function-name> --follow
```

Output:
```
Decoded Data: Hello Stream
```

---

## 🧠 Key Takeaways
- Kinesis handles real-time streaming ingestion.  
- Lambda processes records instantly.  
- Shards control scalability and throughput.  
