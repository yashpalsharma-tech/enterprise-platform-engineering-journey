**IAM service Key tskeway Points**

What is IAM?
IAM (Identity and Access Management) is the AWS service used to securely manage who can access AWS resources and what actions they are allowed to perform.

Authentication vs Authorization
Authentication i.e Identity Check
Question:
Who are you?  example Username, Password, MFA, Access Key

Authorization i.e Permission Check
Question:
What are you allowed to do?

IAM Components:
IAM User: Represents a person or an application. (Example Yashpal, DBA, Developer, Terraform, GitHub Actions)

IAM Group: A collection of users. (Developers, Finance, DBAs, Cloud Team)
Instead of assigning permissions one by one, Assign permissions to the group. Every user in that group automatically inherits them.

IAM Policy
A policy is simply a JSON document that defines permissions. Example
(Allow
Read S3
Start EC2
Stop EC2

Deny
Delete S3
Delete RDS)

IAM Role:
A role is not a user.
Instead, it is an identity that can be assumed temporarily by:
AWS services (for example, an EC2 instance accessing S3)
Applications
Users
Another AWS account

Roles provide temporary credentials instead of long-term passwords or access keys.

Root User:
When you create an AWS account,
AWS creates one Root User.
This account has unrestricted permissions.

Least Privilege Principle: Give users only the permissions they need to perform their job—and nothing more.


