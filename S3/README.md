# 🪣 AWS S3 – Interview Questions & Answers

A complete collection of **frequently asked**, **intermediate**, and **scenario-based** interview questions for **Amazon S3 (Simple Storage Service)** — tailored for **DevOps Engineer** and **AWS Practitioner** interviews.

---

## 🟢 Basic S3 Interview Questions

### 1. What is Amazon S3?
Amazon S3 (Simple Storage Service) is an **object storage service** that allows you to store and retrieve data at any scale from anywhere. It’s designed for **durability (99.999999999%)** and **high availability**.

---

### 2. What are objects in S3?
An object is the fundamental entity stored in S3. Each object consists of:
- **Key (name)**
- **Value (data)**
- **Metadata**
- **Version ID (if versioning is enabled)**

---

### 3. What is an S3 bucket?
A bucket is a **container for storing objects**. Each bucket must have a **globally unique name** and is created in a specific AWS region.

---

### 4. What is the maximum object size you can store in S3?
Maximum size: **5 TB**  
For files larger than 100 MB, AWS recommends using **multipart upload**.

---

### 5. What are the storage classes in S3?
| Storage Class | Use Case |
|----------------|-----------|
| **S3 Standard** | Frequently accessed data |
| **S3 Intelligent-Tiering** | Automatically moves data between access tiers |
| **S3 Standard-IA** | Infrequent access |
| **S3 One Zone-IA** | Infrequent access in a single AZ |
| **S3 Glacier** | Archival storage (retrieval in minutes to hours) |
| **S3 Glacier Deep Archive** | Long-term archival (retrieval in hours) |

---

### 6. What is the difference between S3 and EBS?
| Feature | S3 | EBS |
|----------|----|-----|
| Storage Type | Object Storage | Block Storage |
| Access | HTTP-based (via API/console) | Attached to EC2 instance |
| Use Case | Backup, static assets | Boot volumes, databases |

---

### 7. What is S3 Versioning?
Versioning allows multiple versions of an object to be stored in a bucket. It helps **recover deleted or overwritten** files.

```bash
aws s3api put-bucket-versioning   --bucket my-bucket-name   --versioning-configuration Status=Enabled
```

---

### 8. What is S3 Lifecycle Management?
Lifecycle policies automatically **transition** or **expire** objects based on rules.  
Example: Move objects to **Glacier** after 30 days, delete after 365 days.

---

### 9. What is S3 Cross-Region Replication (CRR)?
CRR automatically replicates objects from a source bucket to a destination bucket in another AWS region for **disaster recovery** or **compliance**.

---

### 10. What is S3 Transfer Acceleration?
It speeds up uploads and downloads by routing traffic through **Amazon CloudFront’s edge locations**.

```bash
aws s3 cp myfile.zip s3://mybucket/ --region us-east-1 --endpoint-url https://<bucketname>.s3-accelerate.amazonaws.com
```

---

## 🟠 Intermediate-Level Questions

### 11. What are S3 Event Notifications?
S3 can trigger **events** (Lambda, SNS, or SQS) when certain actions occur, like object upload or deletion.

Example use cases:
- Trigger Lambda to resize an image after upload.  
- Send notification when a new object is added.

---

### 12. What is the difference between S3 and Glacier?
| Feature | S3 | Glacier |
|----------|----|----------|
| Purpose | Active storage | Archival storage |
| Retrieval time | Milliseconds | Minutes to hours |
| Cost | Higher | Very low |

---

### 13. How do you secure data in S3?
- Enable **Bucket Policies** and **IAM permissions**
- Use **S3 Block Public Access**
- Encrypt data (SSE-S3, SSE-KMS, SSE-C)
- Enable **MFA Delete**

---

### 14. What is S3 Object Lock?
S3 Object Lock prevents objects from being deleted or overwritten for a fixed amount of time — used for **compliance and WORM (Write Once, Read Many)** scenarios.

---

### 15. What is S3 Select?
S3 Select allows you to **query specific data** from an object using SQL, without downloading the entire file.

```bash
aws s3api select-object-content   --bucket my-bucket   --key data.csv   --expression "SELECT * FROM S3Object s WHERE s.age > 30"   --expression-type SQL   --input-serialization '{"CSV": {}}'   --output-serialization '{"CSV": {}}'
```

---

### 16. How to host a static website using S3?
1. Create an S3 bucket with **public access**.  
2. Enable **static website hosting**.  
3. Upload HTML files.  
4. Access via S3 endpoint or Route 53 domain.

---

### 17. How to enforce HTTPS for S3 bucket access?
Use **CloudFront** in front of S3 and redirect all HTTP requests to HTTPS.

---

## 🔵 Scenario-Based Questions

### 18. Scenario: You need to back up EC2 logs daily to S3.
Use **AWS CLI or Lambda** to automate upload:
```bash
aws s3 sync /var/log/ s3://my-logs-bucket/daily/
```

---

### 19. Scenario: You accidentally deleted a file. How to recover?
- Enable **Versioning** → Retrieve previous version of the object.  
- If not versioned, recovery may not be possible unless backed up elsewhere.

---

### 20. Scenario: You want to move old data to Glacier automatically.
Create a **Lifecycle Policy**:  
Move objects to **Glacier** after 30 days.

```bash
aws s3api put-bucket-lifecycle-configuration   --bucket my-bucket   --lifecycle-configuration file://lifecycle.json
```

`lifecycle.json` example:
```json
{
  "Rules": [
    {
      "ID": "MoveToGlacier",
      "Prefix": "",
      "Status": "Enabled",
      "Transitions": [
        {
          "Days": 30,
          "StorageClass": "GLACIER"
        }
      ]
    }
  ]
}
```

---

### 21. Scenario: You need to restrict S3 bucket access to VPC.
Use **VPC Endpoint Policy** and bucket policy to only allow access from your VPC.

---

### 22. Scenario: Detect and prevent accidental public exposure.
Enable:
- **Block Public Access** (account level)  
- **AWS Config rules** to detect public buckets

---

### 23. Scenario: Transfer data from one account to another securely.
Use **Bucket Policy** granting permissions to another AWS account and enable **Cross-Account IAM roles**.

---

## 🟣 Advanced Questions

### 24. What is S3 Inventory?
S3 Inventory provides a daily or weekly **CSV or ORC report** of all objects, metadata, and encryption status for auditing and management.

---

### 25. How does S3 handle consistency?
- **Read-after-write consistency** for PUTs of new objects.  
- **Eventual consistency** for overwrite PUTs and DELETEs.

---

### 26. What are pre-signed URLs in S3?
Pre-signed URLs grant **temporary access** to objects without making them public.

```bash
aws s3 presign s3://mybucket/myfile.txt --expires-in 3600
```

---

### 27. What is S3 Access Analyzer?
Analyzes bucket policies and IAM permissions to identify **unintended public or cross-account access**.

---

### 28. How do you optimize S3 cost?
- Use **Lifecycle policies** to transition data.  
- Use **Intelligent-Tiering** for automatic optimization.  
- Enable **S3 Storage Lens** for cost analysis.

---

## ✅ Summary Table

| Feature | Description |
|----------|--------------|
| Object Storage | Store any amount of data |
| Versioning | Recover deleted/overwritten objects |
| Lifecycle Rules | Automate transitions and deletions |
| Replication | Cross-region or same-region copies |
| Encryption | Protect data at rest and in transit |
| Events | Trigger automation via Lambda/SNS/SQS |

---

**💡 Tip for DevOps Engineers:**  
Combine S3 with:
- **CloudFront** → for content delivery  
- **Lambda** → for event automation  
- **Athena** → for queryable data lakes  

---



