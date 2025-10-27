# 🧠 AWS EC2 Interview Questions and Answers

### 📘 Basic Level

**1. What is Amazon EC2?**  
Amazon EC2 (Elastic Compute Cloud) is a web service that provides scalable virtual servers in the AWS cloud. It allows users to run applications on virtual machines called *instances*.

**2. What are EC2 instance types?**  
- General Purpose (t3, t4g, m6i)  
- Compute Optimized (c6i, c7g)  
- Memory Optimized (r6i, x2idn)  
- Storage Optimized (i4i, d3)  
- Accelerated Computing (p4d, g5)

**3. What is an AMI (Amazon Machine Image)?**  
An AMI is a template containing the OS, software, and configuration used to launch EC2 instances.

**4. EC2 Pricing Models:**  
- On-Demand  
- Reserved Instances  
- Spot Instances  
- Dedicated Hosts  
- Savings Plans

**5. Default storage in EC2:**  
EBS (Elastic Block Store) for persistent storage. Optional Instance Store for temporary data.

**6. Connecting to EC2:**  
Linux: `ssh -i mykey.pem ec2-user@<public-ip>`  
Windows: Use RDP with decrypted password.

---

### 📗 Intermediate Level

**7. Difference between EBS and Instance Store**  

| Feature | EBS | Instance Store |
|----------|-----|----------------|
| Data Persistence | Yes | No |
| Durability | High | Low |
| Use case | Databases | Temporary cache |

**8. What is an Elastic IP?**  
A static public IPv4 address that can be remapped to another instance.

**9. What is EC2 User Data?**  
A script executed during the first boot.  
Example:  
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
```

**10. How do you scale EC2 automatically?**  
Using Auto Scaling Groups with CloudWatch alarms.

**11. What is a Security Group?**  
A virtual firewall that controls inbound/outbound traffic for instances.

**12. Security Groups vs NACLs**  

| Feature | Security Group | NACL |
|----------|----------------|------|
| Level | Instance | Subnet |
| Stateful | Yes | No |
| Rules | Allow only | Allow/Deny |

**13. What is a Key Pair?**  
Public/private key used for SSH authentication.

---

### 📙 Advanced Level

**14. How do you secure EC2?**  
- Use IAM roles instead of credentials  
- Restrict security groups  
- Enable encryption  
- Use SSM for access  
- Rotate keys regularly

**15. How to make EC2 highly available?**  
- Deploy in multiple AZs  
- Use Load Balancer  
- Use Auto Scaling Groups  
- Store data in EFS or RDS

**16. Backup strategies:**  
- EBS Snapshots  
- AMI Creation  
- AWS Backup

**17. Troubleshooting EC2 launch issues:**  
Check instance status, IAM roles, subnet, key pairs, and CloudWatch logs.

**18. Stop vs Terminate**  

| Action | Data Persistence | Billing | Elastic IP |
|--------|------------------|----------|-------------|
| Stop | Keeps EBS | Stopped | Retained |
| Terminate | Deletes EBS | No | Released |

**19. Migration to EC2:**  
Use AWS Application Migration Service or Server Migration Service.

**20. SSH Issue Scenario:**  
1. Verify port 22 open  
2. Use correct key pair  
3. Check instance state  
4. Validate NACL and public IP  
5. Review SSH logs via EC2 serial console

---

### 💡 DevOps-Specific Questions

| Topic | Question | Key Concept |
|-------|-----------|-------------|
| CI/CD | How does Jenkins deploy to EC2? | SSH or CodeDeploy |
| Terraform | How do you define EC2? | `resource "aws_instance"` |
| Ansible | How do you manage EC2 inventory? | AWS dynamic inventory plugin |
| Monitoring | How do you monitor EC2? | CloudWatch metrics + alarms |
| Scaling | How do you scale EC2 automatically? | Auto Scaling Group |

---
