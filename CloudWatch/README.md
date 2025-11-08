# ☁️ AWS CloudWatch – Interview Questions & Answers

A complete collection of **frequently asked**, **intermediate**, and **scenario-based** interview questions for **AWS CloudWatch** — tailored for **DevOps Engineer** and **AWS Practitioner** roles.

---

## 🟢 Basic CloudWatch Interview Questions

### 1. What is Amazon CloudWatch?
Amazon CloudWatch is a **monitoring and observability service** that provides data and actionable insights for AWS resources, hybrid, and on-premises applications.  
It helps you collect metrics, monitor logs, set alarms, and automatically react to changes in your AWS environment.

---

### 2. What are CloudWatch metrics?
Metrics are the **fundamental data points** in CloudWatch.  
Examples:
- EC2: CPU utilization  
- ELB: Latency  
- RDS: Free storage space  

---

### 3. What are CloudWatch Alarms?
Alarms **monitor metrics** and **trigger actions** when a threshold is reached.  
Actions include sending SNS notifications or performing auto-scaling.

---

### 4. Difference between CloudWatch and CloudTrail?

| Feature | CloudWatch | CloudTrail |
|----------|-------------|-------------|
| Purpose | Monitors metrics & logs | Records API calls |
| Data Type | Performance data | Activity/audit data |
| Example | CPU utilization, latency | Who started/stopped EC2 instance |

---

### 5. How does CloudWatch collect data?
- Automatically collects metrics from AWS services like EC2, RDS, Lambda.  
- You can also **publish custom metrics** using the AWS CLI, SDKs, or CloudWatch Agent.

---

### 6. What are custom metrics?
Custom metrics are **user-defined metrics** published from applications or on-prem servers.  
Example: `NumberOfActiveUsers`, `QueueDepth`, `MemoryUsage`.

---

### 7. What is the default metric collection period?
- **Basic monitoring:** 5 minutes (default)  
- **Detailed monitoring:** 1 minute

---

### 8. What are CloudWatch Logs?
CloudWatch Logs collect, monitor, and store logs from AWS resources (EC2, Lambda, ECS, etc.).  
Logs are grouped into:
- **Log groups** → collections of log streams  
- **Log streams** → sequences of log events from a specific source

---

### 9. What is a CloudWatch Dashboard?
A customizable dashboard to visualize metrics and alarms in real time.

---

### 10. Retention period of CloudWatch metrics

| Resolution | Retention |
|-------------|------------|
| 1 minute | 15 days |
| 5 minutes | 63 days |
| 1 hour | 455 days (15 months) |

---

## 🟠 Intermediate-Level Questions

### 11. How do you monitor EC2 memory and disk metrics?
By default, CloudWatch doesn’t collect these metrics.  
You must:
1. Install the **CloudWatch Agent** on the EC2 instance.  
2. Configure the metrics in the agent configuration file.  
3. Publish them to CloudWatch.

---

### 12. What are CloudWatch Events (EventBridge)?
EventBridge lets you **react to changes** in your AWS environment.  
Examples:
- Trigger Lambda when EC2 stops.
- Notify via SNS when an Auto Scaling event occurs.

---

### 13. How to create an alarm via AWS CLI?

```bash
aws cloudwatch put-metric-alarm   --alarm-name "HighCPU"   --metric-name CPUUtilization   --namespace AWS/EC2   --statistic Average   --period 300   --threshold 80   --comparison-operator GreaterThanThreshold   --dimensions Name=InstanceId,Value=i-1234567890abcdef0   --evaluation-periods 2   --alarm-actions arn:aws:sns:region:account-id:topicname
```

---

### 14. Can CloudWatch trigger automated actions?
✅ Yes.  
CloudWatch can:
- Send SNS notifications  
- Invoke Lambda functions  
- Start/stop EC2 instances  
- Trigger Auto Scaling actions

---

### 15. What are dimensions in CloudWatch?
Dimensions are name/value pairs used to identify a metric uniquely.  
Example:
```
Name: InstanceId  
Value: i-0abcd1234
```

---

### 16. How to view CloudWatch logs for Lambda?
Lambda automatically sends logs to CloudWatch under:
```
/aws/lambda/<function-name>
```

View logs using CLI:
```bash
aws logs get-log-events   --log-group-name /aws/lambda/my-function   --log-stream-name <stream-name>
```

---

## 🔵 Scenario-Based Questions

### 17. Scenario: EC2 instance CPU = 100%. How to get notified?
1. Create an alarm on `CPUUtilization > 90%`.  
2. Attach SNS topic to send an email/SMS notification.  
3. Optionally trigger an Auto Scaling policy.

---

### 18. Scenario: Stop idle EC2 instances at night.
1. Create a metric filter for CPU < 5%.  
2. Trigger a Lambda function via EventBridge to stop the instance.

---

### 19. Scenario: Analyze log errors across EC2 instances.
1. Send logs to **CloudWatch Logs**.  
2. Create a **log group** for your application.  
3. Use **CloudWatch Logs Insights** to query:
   ```sql
   fields @timestamp, @message
   | filter @message like /ERROR/
   | sort @timestamp desc
   | limit 20
   ```

---

### 20. Scenario: Monitor application logs on EC2.
1. Install CloudWatch Logs Agent.  
2. Configure `/etc/awslogs/awslogs.conf` with log file paths.  
3. Start the agent to push logs automatically.

---

### 21. Scenario: AWS billing alert.
1. Enable **Billing Metrics** in CloudWatch.  
2. Create an alarm on `EstimatedCharges`.  
3. Notify via SNS when charges exceed a threshold.

---

## 🟣 Advanced Questions

### 22. What are metric filters in CloudWatch Logs?
Metric filters extract numerical data from logs.  
Example: Count how many times `ERROR` appears in a log file.

---

### 23. How does CloudWatch integrate with Auto Scaling?
CloudWatch alarms trigger Auto Scaling policies based on metrics like CPUUtilization or NetworkIn.

---

### 24. Can CloudWatch monitor non-AWS resources?
✅ Yes.  
You can monitor on-prem servers using **CloudWatch Agent** or **API**.

---

### 25. What is CloudWatch Logs Insights?
A query tool to analyze logs using SQL-like syntax.

```sql
fields @timestamp, @message
| filter @message like /Exception/
| sort @timestamp desc
| limit 10
```

---

## ✅ Summary Table

| Feature | Description |
|----------|--------------|
| Metrics | Numerical data points (CPU, memory, etc.) |
| Logs | Application/system log storage |
| Alarms | Trigger actions when thresholds are breached |
| Dashboards | Visualize metrics and alarms |
| Events | Respond to AWS resource changes |
| Insights | Analyze log data with queries |

---

**💡 Tip for DevOps Engineers:**  
Combine CloudWatch with:
- **SNS** → for alerting  
- **Lambda** → for auto-remediation  
- **Auto Scaling** → for dynamic infrastructure scaling  

---

