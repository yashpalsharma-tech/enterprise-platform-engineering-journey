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



