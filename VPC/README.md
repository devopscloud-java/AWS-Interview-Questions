# 🌐 AWS VPC – Interview Questions & Answers

A comprehensive set of **frequently asked**, **intermediate**, and **scenario-based** interview questions for **Amazon Virtual Private Cloud (VPC)** — designed for **DevOps Engineers** and **Cloud Practitioners**.

---

## 🟢 Basic VPC Interview Questions

### 1. What is Amazon VPC?
Amazon Virtual Private Cloud (VPC) allows you to **create a private network** within AWS where you can launch and manage AWS resources securely. It gives you full control over **IP addressing, routing, and security**.

---

### 2. What are the main components of a VPC?
- **VPC** – The virtual network itself.  
- **Subnets** – Divide your VPC into public and private sections.  
- **Route Tables** – Define routing rules for network traffic.  
- **Internet Gateway (IGW)** – Allows access to the internet.  
- **NAT Gateway / NAT Instance** – Enables private instances to access the internet.  
- **Security Groups** – Control inbound/outbound traffic at instance level.  
- **Network ACLs (NACLs)** – Control traffic at subnet level.  
- **VPC Peering / Transit Gateway** – Connect multiple VPCs.  

---

### 3. What is the CIDR block in VPC?
A **CIDR block (Classless Inter-Domain Routing)** defines the IP address range of your VPC.  
Example: `10.0.0.0/16` gives 65,536 IP addresses.

---

### 4. How many VPCs can you create per AWS region?
By default, **5 VPCs per region** (can be increased with AWS support).

---

### 5. What is the difference between a public and private subnet?
| Subnet Type | Internet Access | Typical Use Case |
|--------------|------------------|------------------|
| Public Subnet | Yes (via IGW) | Web servers |
| Private Subnet | No direct access | Databases, internal apps |

---

### 6. What is an Internet Gateway (IGW)?
An IGW allows **instances in a VPC to connect to the internet** and vice versa.

```bash
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --internet-gateway-id igw-123abc --vpc-id vpc-456xyz
```

---

### 7. What is a NAT Gateway?
A **NAT Gateway** enables instances in private subnets to connect to the internet (e.g., for software updates) without exposing them to inbound connections.

---

### 8. What are route tables?
Route tables determine **where network traffic is directed**.  
Each subnet must be associated with a route table.

Example:
| Destination | Target |
|--------------|---------|
| 10.0.0.0/16 | local |
| 0.0.0.0/0 | igw-123456 |

---

### 9. What are security groups?
Security groups act as **virtual firewalls** for instances, controlling inbound and outbound traffic.  
They are **stateful**, meaning return traffic is automatically allowed.

---

### 10. What is a Network ACL (NACL)?
Network ACLs are **stateless firewalls** for controlling traffic at the subnet level.  
You must explicitly allow both inbound and outbound rules.

---

## 🟠 Intermediate-Level Questions

### 11. Difference between Security Group and NACL
| Feature | Security Group | Network ACL |
|----------|----------------|-------------|
| Level | Instance | Subnet |
| Stateful/Stateless | Stateful | Stateless |
| Default Behavior | Deny all inbound, allow outbound | Allow all inbound/outbound |
| Rules Evaluation | All rules are evaluated | Evaluated in order |

---

### 12. What is VPC Peering?
VPC Peering connects **two VPCs** privately within or across AWS accounts.  
Traffic flows as if they are within the same network.

```bash
aws ec2 create-vpc-peering-connection --vpc-id vpc-111aaa --peer-vpc-id vpc-222bbb
```

---

### 13. What is AWS Transit Gateway?
AWS Transit Gateway connects **multiple VPCs and on-prem networks** using a central hub. It simplifies large-scale network architectures.

---

### 14. What is a VPC Endpoint?
VPC Endpoints allow **private access to AWS services** (like S3, DynamoDB) without using the public internet.  
Two types:
- **Interface Endpoint (ENI-based)**  
- **Gateway Endpoint (S3/DynamoDB)**

---

### 15. What is the default VPC?
Every region has a **default VPC** with:
- CIDR block (172.31.0.0/16)
- One default subnet per AZ
- Internet access enabled

---

### 16. What are Elastic Network Interfaces (ENIs)?
ENIs are **virtual network cards** attached to EC2 instances. They allow:
- Multiple IPs per instance  
- Network failover support  
- Separation of management and data traffic

---

### 17. What is DHCP Options Set in VPC?
It defines **custom domain name servers (DNS)**, domain names, and NTP servers for instances in a VPC.

---

### 18. How do you connect your on-premises data center to AWS VPC?
1. **VPN Connection** (Site-to-Site VPN)  
2. **AWS Direct Connect** (dedicated line)  
3. **Transit Gateway** (for multiple VPNs)

---

### 19. What is VPC Flow Logs?
Flow Logs capture **IP traffic information** going to and from network interfaces in a VPC.  
They help in security analysis and troubleshooting.

```bash
aws ec2 create-flow-logs   --resource-type VPC   --resource-id vpc-12345   --traffic-type ALL   --log-group-name my-flow-logs
```

---

### 20. What is PrivateLink?
AWS PrivateLink provides **secure, private connectivity** between VPCs, services, and AWS accounts **without using public IPs**.

---

## 🔵 Scenario-Based Questions

### 21. Scenario: EC2 in private subnet needs internet access.
Use a **NAT Gateway** in a public subnet. Update route table:
```
Destination: 0.0.0.0/0 → Target: nat-xxxxxx
```

---

### 22. Scenario: Web servers in public subnet and DB in private subnet — how to secure communication?
- Allow DB port (e.g., 3306) only from web server security group.  
- Deny public internet access to DB subnet.

---

### 23. Scenario: You need to connect multiple VPCs across accounts.
Use **VPC Peering** for small-scale, or **Transit Gateway** for large-scale connections.

---

### 24. Scenario: Restrict S3 access from VPC only.
Use an **S3 Gateway Endpoint** and update bucket policy:
```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:*",
  "Resource": "arn:aws:s3:::mybucket/*",
  "Condition": {
    "StringEquals": {
      "aws:SourceVpce": "vpce-123456789"
    }
  }
}
```

---

### 25. Scenario: You need to troubleshoot network issues in VPC.
Use:
- **VPC Flow Logs**  
- **Reachability Analyzer**  
- **Network Manager** (for Transit Gateway)

---

## 🟣 Advanced Questions

### 26. What is AWS Direct Connect?
A **dedicated private network connection** between on-premises data center and AWS.  
It provides **lower latency** and **consistent performance** compared to VPN.

---

### 27. What are Transit Gateway route tables?
They control how traffic flows between connected VPCs, VPNs, and Direct Connect gateways.

---

### 28. Can two VPCs have overlapping CIDR blocks?
No, **overlapping CIDR ranges** cannot be peered. You must use non-overlapping CIDRs or Transit Gateway with route filtering.

---

### 29. What is Elastic IP and how does it work in VPC?
Elastic IPs are **static public IP addresses**. They can be remapped to different instances in case of failure for high availability.

---

### 30. How do you secure a VPC?
- Restrict inbound/outbound using **Security Groups** and **NACLs**  
- Enable **Flow Logs**  
- Use **Private Subnets** for sensitive resources  
- Use **IAM roles and VPC Endpoints** instead of public access

---

## ✅ Summary Table

| Component | Description |
|------------|-------------|
| VPC | Virtual network environment |
| Subnet | Logical division (public/private) |
| IGW | Enables internet access |
| NAT Gateway | Allows outbound-only internet access |
| Security Group | Instance-level firewall |
| NACL | Subnet-level firewall |
| Peering / TGW | Connect VPCs privately |
| Flow Logs | Network traffic logging |

---

**💡 Tip for DevOps Engineers:**  
Combine VPC with:
- **CloudWatch Logs** → for Flow Log analysis  
- **Lambda** → for automated network remediation  
- **GuardDuty** → for threat detection  

---

