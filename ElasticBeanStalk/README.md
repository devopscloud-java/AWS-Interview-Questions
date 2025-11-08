Basic Questions

1. What is AWS Elastic Beanstalk?
   
Answer:

AWS Elastic Beanstalk (EB) is a Platform as a Service (PaaS) that allows you to deploy and manage applications in the AWS Cloud without worrying about the infrastructure. It automatically handles capacity provisioning, load balancing, scaling, and application health monitoring.

Key Points:

Supports multiple languages: Java, .NET, Node.js, Python, PHP, Ruby, Go, Docker.

Automatically provisions AWS resources like EC2, S3, RDS, and ELB.

Provides application versions and rolling updates.

2. How does Elastic Beanstalk work?
   
Answer:

You upload your application code (WAR, ZIP, Docker image).

EB selects the right platform (e.g., Tomcat, Node.js).

EB provisions resources: EC2 instances, Load Balancer, Auto Scaling, Security Groups.

EB deploys the app, monitors health, and performs scaling automatically.

3. What are the components of Elastic Beanstalk?
   
Answer:

Application: Logical container for your environments.

Application Version: Specific deployable code (ZIP/WAR).

Environment: Running version of the application (Dev, Test, Prod).

Environment Tier: Web Server Tier or Worker Tier.

Platform: Technology stack used (e.g., Python, Node.js, Docker).

4. What are the environment tiers in Elastic Beanstalk?
   
Answer:

Web Server Environment: Handles HTTP requests (uses load balancer).

Worker Environment: Handles background processing tasks (uses SQS to process jobs).

Intermediate Questions

5. How does Elastic Beanstalk handle scaling?
Answer:

Supports Auto Scaling of EC2 instances based on metrics like CPU utilization, network traffic, or custom CloudWatch metrics.

Can perform rolling deployments, rolling with additional batch, or immutable deployments to avoid downtime.

6. How do you deploy an application in Elastic Beanstalk?
Answer:

Using AWS Management Console: Upload code → Select platform → Deploy.

Using AWS CLI:
<pre>
eb init           # Initialize application
eb create         # Create environment
eb deploy         # Deploy new version
eb status         # Check environment status
</pre>

Using CI/CD tools: Integrate with CodePipeline, Jenkins, or GitHub Actions.

7. What is the difference between Elastic Beanstalk and EC2?

Feature	Elastic Beanstalk	EC2

Management	Managed PaaS	User manages everything

Scaling	Automatic	Manual unless configured

Deployment	Application-level	Server-level

Complexity	Low	High

Health Monitoring	Built-in	Custom setup

8. How do you configure environment variables in Elastic Beanstalk?
9. 
Answer:

Via the EB Console → Configuration → Software.

Using .ebextensions config files:

<pre>option_settings:
  aws:elasticbeanstalk:application:environment:
    ENV_NAME: "production"
    DB_HOST: "mydb.example.com"
</pre>

9. How do you perform updates in Elastic Beanstalk without downtime?
    
Answer:

Rolling Updates: Deploy updates in batches; some instances remain live.

Rolling with Additional Batch: Adds temporary instances for deployment.

Immutable Updates: Deploys new instances with updated code, then swaps them.

10. What monitoring and logging options does Elastic Beanstalk provide?
    
Answer:

Monitoring: Integrated with CloudWatch, health dashboards.

Logs: Can be accessed via the EB console or downloaded from EC2 instances.

Enhanced Health: Tracks request latency, error rates, and instance health.

Scenario-Based Questions

11. Scenario: Your EB application crashes frequently during peak traffic. How do you troubleshoot?
    
Answer:

Check Elastic Beanstalk environment health and logs.

Inspect CloudWatch metrics for CPU, memory, and network spikes.

Review application logs (/var/log/web.stdout.log).

Consider increasing instance size or enabling Auto Scaling.

Ensure database connections are optimized if using RDS.

12. Scenario: You need to deploy a new version of your app but cannot afford downtime.
    
Answer:

Use Rolling with Additional Batch or Immutable Deployments.

EB creates new instances with the updated version and swaps traffic gradually.

13. How can you use a custom domain with Elastic Beanstalk?
    
Answer:

Create a CNAME in Route 53 pointing to the EB environment URL.

Ensure SSL certificates are attached using AWS Certificate Manager (ACM).

14. Can you use Elastic Beanstalk with Docker?
    
Answer:

Yes, EB supports:

Single-container Docker: Simple Dockerfile.

Multi-container Docker: Using ECS and Dockerrun.aws.json file.

15. How do you back up data in Elastic Beanstalk environments?
    
Answer:

EB itself does not manage persistent storage; use RDS snapshots, S3 backups, or EFS for file storage.

Tips for Interview:

Always mention AWS best practices like environment separation (Dev/Test/Prod).

Emphasize scaling, monitoring, and zero-downtime deployments.

Be ready for scenario-based questions where you optimize costs or troubleshoot.
