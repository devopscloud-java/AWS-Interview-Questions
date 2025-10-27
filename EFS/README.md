# 🧩 Amazon EFS (Elastic File System) Interview Questions and Answers

## 1. **Basic EFS Interview Questions**

### **Q1. What is Amazon EFS?**
Amazon Elastic File System (EFS) is a fully managed, scalable, shared file storage service for use with AWS Cloud and on-premises resources. It provides NFS (Network File System) protocol–based storage that can be accessed concurrently by multiple EC2 instances.

### **Q2. What type of storage does EFS provide?**
EFS provides **file storage** (not block or object). It supports the **NFSv4 protocol** and behaves like a shared filesystem.

### **Q3. How does EFS differ from EBS and S3?**
| Feature | **EFS** | **EBS** | **S3** |
|----------|----------|----------|--------|
| Type | File Storage | Block Storage | Object Storage |
| Shared Access | Multiple EC2 instances | Single EC2 instance | Unlimited clients |
| Protocol | NFSv4 | Attached volume | REST API |
| Scaling | Automatically scalable | Fixed size | Automatically scalable |
| Use Case | Shared storage | Database, OS | Backup, data lake |

### **Q4. What are the performance modes in EFS?**
1. **General Purpose (default)** — low latency, ideal for web servers and CMS.  
2. **Max I/O** — supports highly parallelized applications (e.g., big data).

### **Q5. What are the throughput modes in EFS?**
1. **Bursting Throughput** — scales automatically based on file system size.  
2. **Provisioned Throughput** — specify desired throughput (MB/s) independent of storage size.

---

## 2. **Architecture & Configuration Questions**

### **Q6. How do you mount an EFS file system to an EC2 instance?**
1. Install the **amazon-efs-utils** package.  
2. Mount command:
   ```bash
   sudo mount -t efs fs-12345678:/ /mnt/efs
   ```
3. Ensure EC2 and EFS are in the **same VPC**, and **security groups** allow NFS (port 2049).

### **Q7. What is an EFS Mount Target?**
A mount target is a network endpoint (ENI) in a subnet that EC2 instances use to access the EFS file system. One mount target per **Availability Zone (AZ)** is required for multi-AZ access.

### **Q8. How is data stored in EFS?**
Data is stored redundantly **across multiple Availability Zones** within a region, ensuring durability and availability.

### **Q9. How does EFS handle scaling?**
EFS automatically **scales up or down** based on the amount of data stored — no manual provisioning needed.

### **Q10. How do you access EFS from on-premises?**
Use **AWS Direct Connect** or **VPN** to extend your on-premises network into your VPC and mount EFS via NFS.

---

## 3. **Advanced and Scenario-Based Questions**

### **Q11. You notice slow performance on EFS — how do you troubleshoot?**
- Check throughput mode (switch to **provisioned** if required).  
- Use **General Purpose** for low-latency workloads.  
- Monitor with **CloudWatch** metrics.  
- Verify **security group** for NFS (2049).  
- Use **Max I/O** for high concurrency.

### **Q12. How do you back up data from EFS?**
- Use **AWS Backup** or **EFS-to-EFS** Backup.  
- Use **AWS DataSync** to replicate to another EFS or S3.

### **Q13. How do you secure data in EFS?**
- **Encryption in-transit** (TLS).  
- **Encryption at-rest** (KMS).  
- **IAM policies** and **security groups**.  
- **Access Points** for fine-grained permissions.

### **Q14. What is EFS Access Point?**
An EFS Access Point defines **user permissions and root directories** for specific applications to simplify access management.

### **Q15. How do you monitor and log EFS usage?**
- **CloudWatch** for metrics.  
- **CloudTrail** for API logs.  
- **AWS Config** for compliance.

---

## 4. **Pricing and Management Questions**

### **Q16. How is Amazon EFS billed?**
- Pay for **storage used (GB/month)**.  
- Optional: **Provisioned throughput**, **EFS IA**, and **data transfer** costs.

### **Q17. What is EFS Lifecycle Management?**
Automatically moves files that haven’t been accessed for a configured period (e.g., 30 days) to **Infrequent Access (IA)**.

### **Q18. Difference between EFS Standard and EFS Infrequent Access (IA)?**
| Feature | **EFS Standard** | **EFS IA** |
|----------|------------------|------------|
| Access Frequency | Frequent | Infrequent |
| Cost | Higher | Lower |
| Performance | High | Slightly lower |
| Best For | Active files | Backup/archive data |

---

## 5. **Real-World & DevOps Scenario Questions**

### **Q19. Scenario: Shared Jenkins Workspace**
**Use Case:** Jenkins master-slave setup requires shared workspace storage.  
**Solution:** Mount EFS on both nodes and point Jenkins workspace to `/mnt/jenkins` for consistent build artifacts.

### **Q20. Scenario: ECS Fargate Shared Storage**
**Use Case:** Containers need shared persistent storage.  
**Solution:** Create EFS, add Access Point, attach to ECS task definition, and mount inside containers.

### **Q21. Can EFS be used with Lambda?**
Yes. AWS Lambda can **mount EFS** for shared datasets exceeding the `/tmp` 512 MB limit.

### **Q22. Scenario: Cross-Region EFS Replication**
**Solution:** Use **AWS DataSync** to replicate EFS between regions periodically.

---

## **Bonus Tips**
- Combine **EFS + ALB + EC2** for WordPress or PHP apps.  
- Use **EFS + Auto Scaling** for shared web content.  
- Share CI/CD build artifacts via EFS instead of SSH copying.

---

**✅ This EFS Interview Guide is ideal for:**
- AWS/DevOps Engineer interviews
- Jenkins, EC2, ECS, or Lambda architecture scenarios
- Real-world troubleshooting and architecture design practice.

