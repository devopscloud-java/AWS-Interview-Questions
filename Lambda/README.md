**AWS Lambda** is a **serverless compute service** from Amazon Web Services that lets you **run code without provisioning or managing servers**.

You just upload your code, and AWS Lambda automatically handles everything needed to run and scale it — from capacity provisioning to monitoring and logging.

---

### 🧩 **Key Concept**

> **“Serverless”** means you don’t have to manage servers — but servers still exist. AWS takes care of them for you.

---

### ⚙️ **How AWS Lambda Works**

1. You **write code** (in Python, Java, Node.js, Go, etc.).
2. You **upload** it to Lambda.
3. You **configure a trigger** — something that causes your function to run (like an S3 upload, API Gateway request, or DynamoDB update).
4. Lambda **executes** the function automatically when triggered.
5. You **pay only for the compute time** used — in milliseconds.

---

### 🧠 **Example Use Case**

* A file is uploaded to an **S3 bucket** → triggers a **Lambda function** → resizes the image and stores it back in S3.

---

### 💻 **Example Code (Python)**

```python
def lambda_handler(event, context):
    name = event.get("name", "World")
    return {
        "statusCode": 200,
        "body": f"Hello, {name}!"
    }
```

---

### 🔥 **Common Triggers**

* **Amazon S3** – run code when a file is uploaded
* **Amazon API Gateway** – run code when an HTTP request comes in
* **Amazon DynamoDB Streams** – process database changes
* **Amazon EventBridge / CloudWatch Events** – scheduled jobs (cron)
* **AWS SNS / SQS** – respond to messages

---

### 🪄 **Key Features**

| Feature                     | Description                         |
| --------------------------- | ----------------------------------- |
| **Event-driven**            | Automatically runs on triggers      |
| **Scalable**                | Scales automatically with demand    |
| **Pay-per-use**             | Pay only for runtime and requests   |
| **Integrated monitoring**   | CloudWatch for logs and metrics     |
| **Supports many languages** | Python, Node.js, Java, Go, C#, etc. |

---

### 💰 **Pricing**

* **Free tier:** 1 million requests and 400,000 GB-seconds of compute per month.
* **After that:** Pay per 1ms of execution and number of requests.

---

### 🧩 **Real-World Use Cases**

* Image/video processing
* Serverless APIs
* Chatbots or Alexa skills
* Real-time file validation
* Scheduled database cleanup

---

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/2fd13ed7-9d17-4c4e-b5cb-c82534b28558" />
