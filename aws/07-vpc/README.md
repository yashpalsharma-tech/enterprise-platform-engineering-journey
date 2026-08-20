# VPC Advanced Networking

## 1. Internet Gateway

An Internet Gateway (IGW) enables communication between a VPC and the internet.

For an IPv4 EC2 instance to communicate directly with the internet, the architecture normally requires:

- Internet Gateway attached to the VPC
- Route from the subnet to the Internet Gateway
- Public IPv4 address or Elastic IP on the instance
- Security Group rules allowing required traffic
- NACL rules allowing required traffic

```text
Internet
   |
   v
Internet Gateway
   |
   v
Public Subnet
   |
   v
EC2 with Public IPv4
```

Example public route:

```text
Destination        Target
10.0.0.0/16        local
0.0.0.0/0          Internet Gateway
```

Important:

A public IPv4 address alone does not make a subnet public.

A subnet is considered public when its route table has a route to an Internet Gateway.

---

# 2. Route Tables

A route table determines where network traffic from a subnet is directed.

Example:

```text
Destination        Target
10.0.0.0/16        local
0.0.0.0/0          Internet Gateway
```

The `local` route enables routing within the VPC.

```text
10.0.0.0/16 → local
```

The default route:

```text
0.0.0.0/0
```

represents destinations not matched by a more specific route.

---

# 3. Public vs Private Subnet Routing

## Public Subnet

Typical route:

```text
10.0.0.0/16 → local
0.0.0.0/0   → Internet Gateway
```

Architecture:

```text
Public EC2
    |
    v
Internet Gateway
    |
    v
Internet
```

## Private Subnet

A private application subnet requiring outbound IPv4 internet access commonly uses:

```text
10.0.0.0/16 → local
0.0.0.0/0   → NAT Gateway
```

Architecture:

```text
Private EC2
     |
     v
NAT Gateway
     |
     v
Internet Gateway
     |
     v
Internet
```

---

# 4. NAT Gateway

A NAT Gateway allows resources in private subnets to initiate outbound IPv4 connections without allowing unsolicited internet connections to be initiated through the NAT Gateway to those private resources.

Typical uses:

- OS updates
- Software downloads
- Package repositories
- External APIs
- Security patches

Architecture:

```text
Private EC2
     |
     v
Private Route Table
0.0.0.0/0 → NAT Gateway
     |
     v
NAT Gateway
Public Subnet
     |
     v
Internet Gateway
     |
     v
Internet
```

A public NAT Gateway is:

- Deployed in a public subnet
- Associated with an Elastic IP address
- Connected to the internet through an Internet Gateway

Exam rule:

```text
Private EC2 needs outbound IPv4 internet access
                    ↓
                NAT Gateway
```

---

# 5. NAT Gateway vs Internet Gateway

```text
Public Resource
      |
      v
Internet Gateway
      |
      v
Internet
```

versus:

```text
Private Resource
      |
      v
NAT Gateway
      |
      v
Internet Gateway
      |
      v
Internet
```

Remember:

```text
IGW
→ VPC connectivity to/from internet

NAT Gateway
→ Outbound IPv4 internet connectivity for private resources
```

---

# 6. Highly Available NAT Architecture

For workloads across multiple Availability Zones, a resilient architecture commonly deploys a NAT Gateway in each AZ.

```text
AZ-A                         AZ-B

Public Subnet A              Public Subnet B
      |                            |
 NAT Gateway A                NAT Gateway B
      ^                            ^
      |                            |
Private Subnet A             Private Subnet B
      |                            |
    EC2-A                        EC2-B
```

Routes:

```text
Private Subnet A
0.0.0.0/0 → NAT Gateway A

Private Subnet B
0.0.0.0/0 → NAT Gateway B
```

Benefits:

- AZ independence
- Improved resilience
- Avoids unnecessary cross-AZ NAT traffic

For smaller development environments, one NAT Gateway may sometimes be used to reduce cost while accepting reduced resilience.

---

# 7. VPC Endpoints

VPC Endpoints allow private connectivity between resources in a VPC and supported services without requiring an Internet Gateway or NAT Gateway for that service traffic.

```text
Private EC2
     |
     v
VPC Endpoint
     |
     v
AWS Service
```

Two important endpoint types:

- Gateway Endpoint
- Interface Endpoint

---

# 8. Gateway VPC Endpoint

Gateway Endpoints are important for:

```text
Amazon S3
Amazon DynamoDB
```

Example:

```text
Private EC2
     |
     v
S3 Gateway Endpoint
     |
     v
Amazon S3
```

Instead of:

```text
Private EC2
     |
     v
NAT Gateway
     |
     v
Amazon S3
```

Gateway Endpoints work with VPC route tables.

Benefits include:

- Private connectivity
- No NAT Gateway required for S3/DynamoDB endpoint traffic
- Can reduce NAT-related costs
- Gateway endpoints have no hourly endpoint charge

Exam clue:

```text
Private EC2 → S3
      +
Avoid NAT Gateway
      ↓
S3 Gateway VPC Endpoint
```

---

# 9. Interface VPC Endpoint

Interface Endpoints provide private connectivity to many AWS services using AWS PrivateLink.

An Interface Endpoint creates Elastic Network Interfaces with private IP addresses in selected subnets.

Example:

```text
Private EC2
     |
     v
Interface Endpoint
ENI + Private IP
     |
     v
AWS PrivateLink
     |
     v
AWS Secrets Manager
```

Interface Endpoints can use Security Groups.

Exam clue:

```text
Private access to supported AWS service
             +
ENI with private IP
             ↓
Interface VPC Endpoint
             ↓
AWS PrivateLink
```

---

# 10. Gateway vs Interface Endpoint

| Feature | Gateway Endpoint | Interface Endpoint |
|---|---|---|
| Key services | S3, DynamoDB | Many AWS services |
| Technology | Route-table based | AWS PrivateLink |
| Creates ENI | No | Yes |
| Private IP on endpoint ENI | No | Yes |
| Security Group on endpoint | No | Yes |
| Hourly endpoint charge | No | Generally yes |

Exam shortcut:

```text
S3 / DynamoDB
      ↓
Gateway Endpoint

Many other supported AWS services
      ↓
Interface Endpoint
      ↓
PrivateLink
```

---

# 11. VPC Peering

VPC Peering provides private connectivity between two VPCs.

Example:

```text
VPC-A
10.0.0.0/16
     |
     | VPC Peering
     |
VPC-B
10.1.0.0/16
```

Route table in VPC-A:

```text
Destination       Target
10.1.0.0/16       Peering Connection
```

Route table in VPC-B:

```text
Destination       Target
10.0.0.0/16       Peering Connection
```

Security Groups and NACLs must also permit the required traffic.

---

# 12. VPC Peering Is Non-Transitive

Consider:

```text
VPC-A ←→ VPC-B ←→ VPC-C
```

This does NOT automatically mean:

```text
VPC-A ←→ VPC-C
```

VPC Peering does not provide transitive routing.

Remember:

```text
A ↔ B     YES

B ↔ C     YES

A → B → C
     NO
```

---

# 13. AWS Transit Gateway

AWS Transit Gateway acts as a central networking hub.

Instead of building many individual VPC Peering connections:

```text
VPC-A ─── VPC-B
  |\       /|
  | \     / |
  |  \   /  |
VPC-C ─── VPC-D
```

Transit Gateway provides a hub-and-spoke design:

```text
             VPC-A
               |
VPC-B ── Transit Gateway ── VPC-C
               |
             VPC-D
               |
             VPC-E
```

Transit Gateway can centrally connect:

- Multiple VPCs
- On-premises networks
- Other supported network attachments

Exam clue:

```text
Two VPCs
   ↓
VPC Peering

Many VPCs + Central Hub
   ↓
Transit Gateway
```

---

# 14. VPC Peering vs Transit Gateway

| Requirement | Better Fit |
|---|---|
| Simple connectivity between two VPCs | VPC Peering |
| Few point-to-point VPC connections | VPC Peering |
| Many VPCs | Transit Gateway |
| Central networking hub | Transit Gateway |
| Transitive routing architecture | Transit Gateway |
| Central VPC + on-premises connectivity | Transit Gateway |

---

# 15. Security Groups

Security Groups operate at the resource/ENI level.

They are:

```text
STATEFUL
```

If traffic is allowed in one direction, response traffic for that connection is automatically permitted.

Characteristics:

- Stateful
- Allow rules only
- Associated with network interfaces/resources
- Commonly used as resource-level firewall controls

---

# 16. Network ACLs

Network ACLs operate at the subnet level.

They are:

```text
STATELESS
```

Required inbound and outbound traffic must be independently permitted.

Characteristics:

- Stateless
- Subnet-level
- Supports ALLOW rules
- Supports DENY rules
- Rules evaluated according to rule number

---

# 17. Security Group vs NACL

| Feature | Security Group | NACL |
|---|---|---|
| Level | Resource/ENI | Subnet |
| Stateful | Yes | No |
| Allow rules | Yes | Yes |
| Deny rules | No | Yes |
| Return traffic | Automatically permitted for allowed connection | Must be permitted |
| Rule evaluation | All applicable rules | Rule-number order |

Exam shortcut:

```text
Security Group
      ↓
STATEFUL
      ↓
ALLOW ONLY

NACL
      ↓
STATELESS
      ↓
ALLOW + DENY
```

---

# 18. Bastion Host

A Bastion Host is a controlled jump point used to access resources in private subnets.

Traditional architecture:

```text
Administrator
      |
      | SSH
      v
Bastion Host
Public Subnet
      |
      | SSH
      v
Private EC2
Private Subnet
```

The Bastion Host should have tightly restricted administrative access.

Example:

```text
Bastion SG
SSH 22
Source: Approved Admin IP

Private EC2 SG
SSH 22
Source: Bastion SG
```

For modern AWS environments, AWS Systems Manager Session Manager can often provide administrative access without opening inbound SSH or maintaining a Bastion Host.

---

# 19. Longest Prefix Match

AWS routing selects the most specific matching route.

Example:

```text
Destination       Target

10.0.0.0/16       local
10.0.1.0/24       VPC Peering
0.0.0.0/0         NAT Gateway
```

Destination:

```text
10.0.1.50
```

All three routes technically match, but:

```text
/24 > /16 > /0
```

Therefore:

```text
10.0.1.50
     ↓
10.0.1.0/24
     ↓
VPC Peering
```

Remember:

```text
Most specific matching route wins
              ↓
Longest Prefix Match
```

---

# 20. Production Multi-AZ VPC Architecture

Example:

```text
                       Internet
                          |
                  Internet Gateway
                          |
            +-------------+-------------+
            |                           |
           AZ-A                        AZ-B
            |                           |
     Public Subnet A             Public Subnet B
            |                           |
       ALB Node A                   ALB Node B
            |                           |
       NAT GW-A                     NAT GW-B
            |                           |
            v                           v
 Private App Subnet A         Private App Subnet B
            |                           |
         EC2-A                       EC2-B
          APP-SG                     APP-SG
            |                           |
            +-------------+-------------+
                          |
                    RDS Endpoint
                          |
            +-------------+-------------+
            |                           |
 Private DB Subnet A          Private DB Subnet B
            |                           |
      RDS Primary               RDS Standby
         DB-SG                     DB-SG
```

S3 access:

```text
Private EC2
     |
     v
S3 Gateway Endpoint
     |
     v
Amazon S3
```

Database Security Group:

```text
Database Port
Source: APP-SG
```

---

# 21. Production Traffic Paths

## User to Application

```text
User
 ↓
Internet Gateway
 ↓
ALB
 ↓
EC2 Private App Tier
```

## Private EC2 to Internet

```text
EC2-A
 ↓
NAT Gateway A
 ↓
Internet Gateway
 ↓
Internet
```

and:

```text
EC2-B
 ↓
NAT Gateway B
 ↓
Internet Gateway
 ↓
Internet
```

## Private EC2 to S3

```text
Private EC2
 ↓
S3 Gateway Endpoint
 ↓
Amazon S3
```

## Application to Database

```text
EC2
APP-SG
 ↓
Database Port
 ↓
RDS
DB-SG
```

---

# 22. VPC Exam Quick Reference

```text
Public subnet
→ Route to Internet Gateway

Private EC2 needs outbound IPv4 internet
→ NAT Gateway

NAT Gateway
→ Public subnet

Highly available NAT architecture
→ NAT Gateway per AZ

Private EC2 needs S3
→ S3 Gateway Endpoint

S3 / DynamoDB
→ Gateway Endpoint

Many other AWS services
→ Interface Endpoint

Interface Endpoint
→ AWS PrivateLink + ENI

Connect two VPCs
→ VPC Peering

VPC Peering
→ Non-transitive

Connect many VPCs centrally
→ Transit Gateway

Security Group
→ Stateful

NACL
→ Stateless

Security Group
→ Allow only

NACL
→ Allow + Deny

Traditional SSH jump server
→ Bastion Host

Modern administrative access without inbound SSH
→ Systems Manager Session Manager

Multiple matching routes
→ Longest Prefix Match

Most specific prefix
→ Route selected
```
