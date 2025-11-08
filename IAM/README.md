AWS IAM Interview Questions & Answers
1. Basic Questions

Q1. What is AWS IAM and why is it used?
A: IAM (Identity and Access Management) is a service that allows you to securely control access to AWS resources. It manages users, groups, roles, and permissions. IAM is used to enforce security, apply least privilege, and manage authentication and authorization for AWS services.

Q2. What are IAM Users, Groups, Roles, and Policies?
A:

User: Individual identity with credentials (username/password, access keys).

Group: Collection of users, used to assign permissions collectively.

Role: Assignable identity for AWS services or users; provides temporary credentials.

Policy: JSON document defining permissions (allow/deny actions on resources).

Q3. Difference between IAM User and IAM Role

Feature	IAM User	IAM Role
Identity	Permanent	Temporary
Credentials	Long-term	Temporary (via STS)
Use-case	Human users	AWS services, cross-account access

Q4. What is an IAM Policy? Name types.
A: Policies are JSON documents defining permissions.
Types:

Managed Policies: AWS-managed or customer-managed reusable policies.

Inline Policies: Embedded directly into a user, group, or role.

Resource-based Policies: Attached directly to resources like S3 bucket policies.

Q5. Difference between Inline and Managed Policies

Inline: Specific to a user/group/role; deleted if entity is deleted.

Managed: Standalone and reusable; can attach to multiple entities.

Q6. How can you enforce MFA for users?

Enable MFA via AWS Console or CLI.

Users must provide MFA token along with password.

Use IAM Policy condition "aws:MultiFactorAuthPresent": "true" to enforce MFA on critical actions.

2. Intermediate Questions

Q7. Difference between Resource-based and Identity-based policies

Resource-based: Attached to resources; specify which IAM users/roles can access. (Example: S3 bucket policy)

Identity-based: Attached to user, group, or role; specifies which resources they can access.

Q8. Difference between Roles and Groups

Role: Temporary identity, assumed by users, services, or external accounts.

Group: Permanent collection of users; no temporary credentials.

Q9. Can IAM policies allow explicit deny and explicit allow?

Yes:

Explicit deny > explicit allow

If no statement matches, default is deny.

Q10. How can you rotate IAM access keys?

Create a new access key for the user.

Update the application/CLI with new key.

Deactivate and delete old key.

AWS recommends rotation every 90 days.

Q11. What is the principle of least privilege?

Grant only necessary permissions.

Avoid using root account for daily tasks.

Use IAM roles with minimal required privileges.

Q12. IAM Policy Simulator

AWS tool to test the effect of policies before applying.

Helps ensure policies do not unintentionally grant/deny access.

Q13. Difference between Access Key and Secret Key

Access Key ID: Public identifier.

Secret Key: Private secret used to sign requests.

Together, they allow programmatic access to AWS resources.

3. Scenario-based Questions

Q14. User can only read objects from an S3 bucket

<pre>{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::my-bucket/*"]
    }
  ]
}
</pre>

Q15. EC2 accessing S3 without storing credentials

Use IAM Role attached to the EC2 instance.

EC2 automatically gets temporary credentials via Instance Profile.

Avoids hardcoding keys.

Q16. Cross-account access

Create IAM Role in target account.

Use trust policy to allow user from source account to assume the role.

Use sts:AssumeRole API to get temporary credentials.

Q17. Recover deleted policy

AWS does not allow recovery of deleted policies.

Use version control or backup scripts to restore JSON of deleted policies.

Q18. Prevent root account usage

Enable MFA on root.

Use IAM users/roles for all daily operations.

Delete root access keys if possible.

Q19. Enforce password policies

Use IAM password policy to require:

Minimum length

Uppercase, lowercase, number, symbol

Expiration and reuse prevention

4. Advanced / Security-focused Questions

Q20. IAM roles and temporary credentials

Roles provide temporary credentials (access key, secret key, session token) via STS.

Credentials expire after a defined period (default 1 hour, configurable).

Q21. Security Token Service (STS)

Provides temporary credentials for IAM roles.

Useful for cross-account access, federated users, EC2, Lambda.

Q22. IAM Access Advisor

Shows services accessed by a user or role.

Helps remove unused permissions and implement least privilege.

Q23. Audit IAM permissions

Use IAM Access Analyzer and CloudTrail.

Identify unused roles, excessive permissions, and access anomalies.

Q24. Restrict login from specific IPs

<pre>{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "NotIpAddress": {"aws:SourceIp": "203.0.113.0/24"}
      }
    }
  ]
}
</pre>

Q25. Service Control Policies (SCPs) vs IAM Policies

SCP: Enforced at AWS Organization level; cannot grant more permissions than IAM policy allows.

IAM Policy: Enforced per user, role, or group; cannot override SCP deny.

5. Trick / Brain-Teasers

Q26. Can an IAM user have inline and managed policies?

Yes, both can coexist.

Q27. Can a role be assumed by multiple AWS services?

Yes, using trust policy. Example: EC2 instance role can also be assumed by Lambda.

Q28. Can a policy be attached to another policy?

No, policies cannot attach to policies. Only to users, groups, or roles.
