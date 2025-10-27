# 🌩️ AWS Interview Questions & Answers

This repository contains a **comprehensive collection of AWS interview questions and answers** — ideal for **DevOps Engineers, Cloud Architects, and Developers** preparing for technical interviews.  
Each topic includes **conceptual**, **scenario-based**, and **hands-on** questions to help you master AWS services.

---

## 📚 Topics Covered

| No. | AWS Service / Concept | Description |
|-----|------------------------|--------------|
| 1 | **EC2 (Elastic Compute Cloud)** | Compute service for running virtual machines |
| 2 | **S3 (Simple Storage Service)** | Object storage for backup, archive, and data lakes |
| 3 | **VPC (Virtual Private Cloud)** | Networking layer for isolation and security |
| 4 | **IAM (Identity & Access Management)** | Securely manage users, roles, and permissions |
| 5 | **EBS & EFS** | Block and file storage options for EC2 |
| 6 | **RDS & DynamoDB** | Managed relational and NoSQL databases |
| 7 | **CloudFormation & Terraform** | Infrastructure as Code (IaC) |
| 8 | **Lambda & Serverless** | Event-driven compute without managing servers |
| 9 | **CloudWatch & CloudTrail** | Monitoring and auditing tools |
| 10 | **CI/CD with Jenkins & CodePipeline** | Continuous Integration & Deployment on AWS |

---

## 💬 Sample Questions & Answers

### **1️⃣ EC2 (Elastic Compute Cloud)**

**Q:** What is EC2 and how does it work?  
**A:** EC2 provides resizable compute capacity in the cloud. You can launch instances, choose AMIs, define instance types, and manage networking using VPC.

**Q:** What’s the difference between Spot, Reserved, and On-Demand instances?  
**A:**  
- **On-Demand:** Pay per use, flexible.  
- **Reserved:** Commit for 1–3 years, cheaper.  
- **Spot:** Bid for unused capacity, cost-effective but can be interrupted.

---

### **2️⃣ S3 (Simple Storage Service)**

**Q:** How do you make an S3 bucket public?  
**A:** Disable block public access, set a bucket policy allowing `s3:GetObject` permission for `Principal: *`.

**Q:** What are S3 storage classes?  
**A:** Standard, Intelligent-Tiering, Standard-IA, One Zone-IA, Glacier, and Deep Archive — each with different pricing and retrieval times.

---

### **3️⃣ VPC (Virtual Private Cloud)**

**Q:** What is a VPC and its components?  
**A:** A logically isolated section of the AWS cloud where you define your own IP range, subnets, route tables, internet gateways, and security groups.

**Q:** Difference between Security Group and NACL?  
**A:**  
- **Security Group:** Stateful, applied to EC2 instances.  
- **NACL:** Stateless, applied at subnet level.

---

### **4️⃣ EFS (Elastic File System)**

**Q:** How is EFS different from EBS?  
**A:**  
- **EFS:** Network file system (shared storage, auto-scalable).  
- **EBS:** Block storage attached to a single EC2 instance.

---

### **5️⃣ CI/CD on AWS**

**Q:** How do you implement a CI/CD pipeline using Jenkins and AWS?  
**A:**  
- Jenkins triggers a build on Git push.  
- Artifacts are deployed to S3 or EC2 using AWS CLI.  
- Optionally integrate with CodeDeploy or Terraform for automation.

---

## 🚀 How to Use This Repository

1. Clone this repo  
   ```bash
   git clone https://github.com/<your-username>/aws-interview-questions.git
