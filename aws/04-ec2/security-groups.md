**Key Takeaway Point**
EC2 Security Groups

A Security Group (SG) acts as a virtual firewall for your EC2 instance.
It controls inbound and outbound network traffic.

Security Groups are stateful.
That means if an inbound connection is allowed, the response traffic is automatically allowed back.
You don't need to create a separate inbound rule for the response traffic.
Security Groups are allow-only, If traffic doesn't match an allowed inbound rule, it is implicitly denied.
Source can be another Security Group, not just an IP address.

DB-SG

  ↓
  
TCP 1521

  ↓
  
Source: App-SG


Why use App-SG as the source instead of the application's private IP address?
Using the Security Group as the source provides dynamic and scalable access control. If an application server is replaced or its private IP changes, the database rule continues to work as long as the new instance belongs to the App-SG. It avoids maintaining individual IP addresses.

Security Group vs Network ACL

Think of your office building.
Security Group = Security Guard at each Office

Imagine every office has its own security guard.
Only people with permission can enter.

Each office has its own guard.

This is exactly how Security Groups work.

They protect individual EC2 instances.

Network ACL = Security Gate at the Building Entrance

Now imagine the building itself has a security gate.

Everyone entering the building must pass through it.
This is how a Network ACL works.

It protects an entire subnet, not individual EC2 instances.

NACL protects the subnet.
Security Group protects the EC2 instance.

Security Group

Protects an EC2 instance
Stateful
Supports Allow rules only

Network ACL
Protects a Subnet
Stateless
Supports Allow and Deny rules



