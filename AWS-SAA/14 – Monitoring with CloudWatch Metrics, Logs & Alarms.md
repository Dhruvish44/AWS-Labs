# AWS Lab 14 – Monitoring with CloudWatch Metrics, Logs & Alarms

## 📘 Overview
This lab sets up CloudWatch metrics and alarms to monitor EC2 instance health, and configures logging and SNS alerts.

**Goal →** Implement proactive monitoring and notifications.

---

## 🚀 Steps Performed
```text
1️⃣ Create SNS Topic for Alerts
aws sns create-topic --name DhruvishAlerts
aws sns subscribe --topic-arn <arn> --protocol email --notification-endpoint <your-email>
✅ Confirm subscription.
```

```text
2️⃣ Create CloudWatch Alarm
aws cloudwatch put-metric-alarm \
--alarm-name CPUHigh \
--metric-name CPUUtilization \
--namespace AWS/EC2 \
--statistic Average \
--period 300 \
--threshold 80 \
--comparison-operator GreaterThanThreshold \
--dimensions Name=InstanceId,Value=<EC2-ID> \
--evaluation-periods 2 \
--alarm-actions <SNS-ARN>

✅ Alarm triggers when CPU > 80% for 10 minutes.
```

```text
3️⃣ Enable EC2 Detailed Monitoring
aws ec2 monitor-instances --instance-ids <EC2-ID>
✅ Granular 1-minute metrics enabled.
```

```text
4️⃣ Stream Application Logs
- Install CloudWatch Agent on EC2.
sudo yum install amazon-cloudwatch-agent -y
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
✅ Logs visible in CloudWatch → Log Groups.
```

---

## 🧩 Verification
```bash
aws cloudwatch describe-alarms
aws logs describe-log-groups
aws sns list-subscriptions
```

---

## 🧠 Key Takeaways
- CloudWatch monitors metrics, logs, and alarms.  
- SNS integrates with alarms for instant alerts.  
- Use detailed monitoring for production instances.  
- Centralize logs using the CloudWatch Agent.
