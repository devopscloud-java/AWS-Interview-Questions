# ☁️ AWS RDS & DynamoDB — Interview Questions and Answers

Comprehensive guide covering **Amazon RDS** (Relational Database Service) and **DynamoDB** (NoSQL).  
Includes **key concepts, interview Q&A, and real-world DevOps scenarios**.

---

## 🟦 Amazon RDS (Relational Database Service)

### 💡 What is Amazon RDS?
Amazon RDS is a **managed relational database service** that automates database setup, patching, backups, and scaling.  
It supports multiple engines like **MySQL, PostgreSQL, Oracle, SQL Server, MariaDB, and Amazon Aurora**.

---

### ✅ Benefits of RDS
- Automated backups and patching  
- Multi-AZ high availability  
- Read replicas for performance  
- Vertical and horizontal scaling  
- Monitoring via CloudWatch  

---

### ⚙️ Multi-AZ vs Read Replica

| Feature | Multi-AZ | Read Replica |
|----------|-----------|--------------|
| Purpose | High availability & failover | Performance (read scaling) |
| Type | Synchronous replication | Asynchronous replication |
| Read-only | No | Yes |
| Failover | Automatic | Manual promotion required |

**Scenario:**  
Your production DB must stay up even during maintenance → **Use Multi-AZ**.  
Need to handle high read traffic → **Add Read Replicas**.

---

### 💾 Backups in RDS
- **Automated backups** (1–35 days retention)
- **Manual snapshots** (kept indefinitely)
- **Point-in-time recovery** available

**Scenario:**  
Database corrupted due to deployment → Restore from automated backup to a specific time.

---

### ⚡ RDS Storage Types
- General Purpose SSD (gp2/gp3)
- Provisioned IOPS (io1/io2)
- Magnetic (deprecated)

---

### 🔒 Security Best Practices
- Use **VPC security groups**
- Enable **IAM database authentication**
- Enforce **SSL/TLS** for connections
- Use **KMS encryption**
- Disable public accessibility

---

### 📈 Scaling in RDS
- **Vertical scaling:** Change instance type (CPU, RAM)
- **Horizontal scaling:** Add **read replicas**

**Scenario:**  
CPU usage above 80% → scale vertically or add read replicas.

---

### 🔁 Failover in RDS
In Multi-AZ mode, RDS automatically switches to the standby instance during outages or maintenance.  
Downtime is typically under a minute.

---

### 🔍 Monitoring Tools
- **CloudWatch:** CPU, memory, IOPS
- **Enhanced Monitoring:** OS-level metrics
- **Performance Insights:** Query-level analysis

---

### 🧠 RDS Troubleshooting Scenario
**Issue:** High latency during traffic spikes  
**Possible Causes:**
- CPU saturation → Scale instance  
- Slow queries → Analyze with Performance Insights  
- Read-heavy workload → Add read replicas  
- IOPS limit reached → Switch to io1/io2

---

## 🟨 Amazon DynamoDB (NoSQL)

### 💡 What is DynamoDB?
DynamoDB is a **fully managed NoSQL key-value and document database** that provides **single-digit millisecond latency** and **automatic scaling**.

---

### 🧩 Core Components
- **Table:** Container for data  
- **Items:** Rows  
- **Attributes:** Columns  
- **Primary Key:** Partition key or partition + sort key  
- **Indexes:** GSI (Global) & LSI (Local)

---

### ⚖️ GSI vs LSI

| Feature | GSI | LSI |
|----------|-----|-----|
| Key attributes | Can differ from base table | Must share partition key |
| Creation time | Anytime | At table creation |
| Storage | Separate | Same partition |
| Use case | Query flexibility | Sorted queries within partition |

---

### 📚 Consistency Models
- **Eventually Consistent Reads:** May return stale data but faster  
- **Strongly Consistent Reads:** Always up-to-date, slightly slower  

**Scenario:**  
Need real-time accuracy (banking) → Use **Strongly Consistent Reads**.

---

### 📈 Scaling in DynamoDB
- **Auto Scaling:** Adjusts capacity automatically  
- **On-Demand Mode:** Instant scaling per request  
- **Partitioning:** Distributes load using hash keys

---

### 🔄 DynamoDB Streams
Captures **INSERT, MODIFY, DELETE** events from tables for:
- **Lambda triggers**
- **Auditing**
- **Real-time analytics**

**Scenario:**  
Send email when a new order is created → Use **Streams + Lambda**.

---

### ⏰ TTL (Time to Live)
Automatically deletes items after expiry.

**Scenario:**  
Use TTL for **session management** to auto-remove expired sessions.

---

### 💰 Provisioned vs On-Demand Mode

| Mode | Description | Use Case |
|------|--------------|----------|
| Provisioned | Manually set RCU/WCU | Predictable workloads |
| On-Demand | Pay-per-request | Variable workloads |

---

### 🚀 Performance Optimization
- Design **effective partition keys**  
- Use **indexes**  
- Enable **DAX (DynamoDB Accelerator)**  
- Keep items **< 400 KB**

---

### 🧠 DynamoDB Troubleshooting Scenario
**Issue:** Throttling (`ProvisionedThroughputExceededException`)  
**Solutions:**
- Switch to **On-Demand** mode  
- Increase **read/write capacity**  
- Use **batch operations**  
- Add **DAX caching**

---

## 🧩 Real-World Architecture Example: RDS + DynamoDB

**Use Case:** E-commerce application

| Component | Purpose |
|------------|----------|
| **RDS (MySQL/PostgreSQL)** | User profiles & order transactions |
| **DynamoDB** | Product catalog & shopping sessions |
| **Lambda** | Syncs updates between RDS and DynamoDB |
| **CloudWatch** | Monitors performance and error metrics |

### 📊 Simple Architecture Diagram

```text
       ┌────────────┐
       │   Client   │
       └─────┬──────┘
             │
        ┌────▼─────┐
        │  API GW  │
        └────┬─────┘
             │
     ┌───────▼────────┐
     │ AWS Lambda      │
     └──────┬──────────┘
            │
   ┌────────▼─────────┐     ┌───────────────┐
   │ Amazon RDS (SQL) │     │ DynamoDB (NoSQL)│
   └──────────────────┘     └────────────────┘

🧑‍💻 Example Interview Scenario

Question:

Your app experiences high read latency on RDS and some session inconsistencies.

How do you fix it?

Answer:

Move session data to DynamoDB for low-latency access.

Keep transactional data in RDS.

Add Read Replicas to offload read traffic.

Use CloudWatch alarms for proactive monitoring.
