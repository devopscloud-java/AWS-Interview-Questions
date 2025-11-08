Basic Questions

1. What is AWS CloudFormation?
   
Answer:
AWS CloudFormation is a service that allows you to model, provision, and manage AWS resources using templates (written in JSON or YAML). It automates infrastructure as code (IaC), ensuring resources are deployed consistently.

3. What are the main components of CloudFormation?
   
Answer:

Template: Defines resources and their properties.

Stack: A collection of resources created/managed as a single unit.

Change Set: Preview of changes before updating a stack.

Stack Set: Deploys stacks across multiple accounts or regions.

3. What is the difference between a Stack and a Stack Set?
   
Answer:

Stack: Single deployment in one AWS account and region.

Stack Set: Allows you to create, update, or delete stacks across multiple accounts and regions simultaneously.

4. Which languages can be used to write CloudFormation templates?
   
Answer:

JSON

YAML (more readable and widely used now)

5. What is a Change Set in CloudFormation?
   
Answer:

A Change Set lets you preview proposed changes to your stack without actually applying them. It helps to avoid unintentional disruptions.

Intermediate Questions

6. How do you handle dependencies between resources in CloudFormation?
   
Answer:

CloudFormation automatically detects dependencies between resources.

You can explicitly define dependencies using the DependsOn attribute.

7. How can you pass parameters to a CloudFormation template?
   
Answer:

Use the Parameters section in the template to accept inputs at stack creation. Example:

<pre>Parameters:
  InstanceType:
    Type: String
    Default: t2.micro
    AllowedValues:
      - t2.micro
      - t2.small
</pre>


8. How do you use outputs in CloudFormation?
   
Answer:

Outputs allow you to export values from one stack to use in another stack or for reference. Example:

<pre>Outputs:
  InstanceId:
    Value: !Ref MyEC2Instance
    Export:
      Name: MyInstanceID
</pre>

9. What is a nested stack?
    
Answer:

A nested stack is a stack created as part of another stack, allowing modular and reusable templates. Useful for breaking large templates into smaller, manageable pieces.

11. What are intrinsic functions in CloudFormation?
    
Answer:

Functions that help manipulate values within templates:

!Ref – References a resource or parameter.

!GetAtt – Gets an attribute of a resource.

!Sub – Substitutes variables in strings.

!Join – Joins values into a string.

!If / !Equals / !Not / !And / !Or – Conditional logic.

Advanced / Scenario-Based Questions

11. Scenario: You need to create an EC2 instance and an S3 bucket, but the EC2 instance depends on the S3 bucket. How do you ensure the correct order of creation?
    
Answer:

CloudFormation automatically detects resource dependencies.

To explicitly enforce order, use DependsOn:

<pre>Resources:
  MyBucket:
    Type: AWS::S3::Bucket

  MyInstance:
    Type: AWS::EC2::Instance
    DependsOn: MyBucket
</pre>

12. Scenario: You want to update a stack without downtime. How do you do it?
    
Answer:

Use Change Sets to preview updates.

Use Rolling updates or Stack update policies for resources like Auto Scaling groups to prevent downtime.

Use UpdateReplacePolicy and DeletionPolicy to protect critical resources.

13. How do you manage secrets (passwords, API keys) in CloudFormation?
    
Answer:

Use AWS Secrets Manager or SSM Parameter Store and reference them in your template:

<pre>DBPassword:
  Type: AWS::SSM::Parameter::Value<String>
  Default: /prod/db/password
  </pre>

14. What are common errors in CloudFormation templates?
    
Answer:

Invalid syntax in JSON/YAML.

Missing dependencies.

Using unavailable or unsupported resource properties.

Parameter mismatch.

Circular dependencies.

15. Scenario: You need to deploy the same infrastructure across multiple regions. What is the approach?
    
Answer:

Use Stack Sets to deploy stacks across multiple accounts/regions efficiently.

Use parameters and mappings to customize per region.

16. How do you roll back a failed stack creation or update?
    
Answer:

CloudFormation automatically rolls back if Rollback on failure is enabled.

For manual control, you can disable automatic rollback, fix issues, and retry.

17. What is the difference between CloudFormation and Terraform?
    
Answer:

Feature	CloudFormation	Terraform
Provider	AWS only	Multi-cloud
Language	JSON/YAML	HCL
State Management	Managed by AWS	Local or remote state file
Modularity	Nested stacks	Modules
