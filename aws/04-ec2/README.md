**EC2 service Key tskeway Points**

Amazon EC2 (Elastic Compute Cloud) is AWS's service for creating and managing virtual servers in the cloud.
Why is it called "Elastic"? You can scale resources up or down as demand changes.

What is Amazon EC2?
Amazon EC2 (Elastic Compute Cloud) is an AWS service that allows users to provision, launch, and manage 
scalable virtual servers in the cloud. It provides on-demand compute capacity, allowing businesses to deploy 
applications quickly without purchasing or maintaining physical hardware. 
EC2 supports multiple operating systems, different instance types, networking, storage options, 
and integrates with other AWS services.

Why do companies use EC2 instead of buying physical servers?
It eliminates the need to purchase and maintain physical hardware.
Servers can be provisioned within minutes.
Compute resources can scale up or down based on demand.
Companies pay only for the resources they use.
It integrates seamlessly with AWS services such as IAM, EBS, CloudWatch, Load Balancers, and Auto Scaling.

What is a Hypervisor?
A Hypervisor is software that allows multiple virtual machines to run on the same physical server.

AWS uses its own high-performance hypervisor technology (based on the Nitro System) to securely isolate EC2 instances.

What is an AMI?
AMI = Amazon Machine Image
Think of an AMI as a template for launching an EC2 instance.

It contains:
Operating System
Installed software (optional)
Configuration (optional)
Boot volume

Common AMIs
Amazon Linux
Ubuntu
Red Hat Enterprise Linux (RHEL)
Windows Server

You can also create custom AMIs.

Instance Families
Family	Optimized For	Example
T	General purpose, burstable	Small web servers, development
M	Balanced CPU and memory	Enterprise applications
C	Compute optimized	Batch jobs, compute-intensive apps
R	Memory optimized	Databases, SAP, caching
X	High-memory workloads	Large in-memory databases
I – Storage Optimized High local storage/I/O Data-intensive workloads

Consider the following factors while deciding the EC2 instance type.

CPU utilization
Memory utilization
Network throughput
Storage I/O
Application workload
Performance testing
Cost

Important Concept: Immutable Infrastructure

Instead of modifying existing servers in place, create a new version of the server and replace the old one.
