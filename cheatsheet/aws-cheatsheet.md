# Amazon aws Cheat Sheet

## Definition

## Key Components

## Important Interview Points

## AWS Exam Tips

## Best Practices

## Common Mistakes

## One-Line Revision


# Elastic Load Balancer

Layer 7 → ALB

Layer 4 → NLB

Health Check:
GET /health

Healthy Response:
HTTP 200 OK

ALB:
✔ HTTP
✔ HTTPS
✔ Path Routing
✔ Host Routing

Benefits

✔ High Availability
✔ Fault Tolerance
✔ Health Checks
✔ Auto Scaling Integration

ALB ≠ CloudWatch

ALB
→ Health Checks

CloudWatch
→ Monitoring & Auto Scaling



# AWS Load Balancer Quick Reference

## Elastic Load Balancer

ELB = Managed AWS service that distributes incoming traffic across healthy targets.

Benefits:

- High Availability
- Fault Tolerance
- Scalability
- Improved Performance
- Health Checks

---

## Load Balancer Types

ALB → Layer 7 → HTTP/HTTPS

NLB → Layer 4 → TCP/UDP/TLS

GWLB → Network Security Appliances

CLB → Legacy

---

## ALB Components

```text
User
 ↓
ALB
 ↓
Listener
 ↓
Listener Rule
 ↓
Target Group
 ↓
Healthy Target


**# AWS Route 53 Quick Reference**

**## Route 53**

AWS managed DNS service.

DNS:

Domain Name
    ↓
Route 53
    ↓
Destination

---

## DNS Records

### A

Domain → IPv4

Example:

www.company.com → 13.229.123.45

### AAAA

Domain → IPv6

### CNAME

Domain → Another Domain

Example:

app.company.com → application.example.com

### Alias

Domain → Supported AWS Resource

Common examples:

- ALB
- CloudFront
- S3 website endpoint
- API Gateway

---

## Hosted Zones

Public Hosted Zone:

Used for publicly resolvable domains.

Private Hosted Zone:

Used for DNS names inside associated VPCs.

---

# Route 53 Routing Policies

## Simple

Use for simple/straightforward routing.

```text
User
 ↓
Route 53
 ↓
ALB



# Amazon RDS Quick Reference

## RDS

```text
Managed Relational Database
          ↓
      Amazon RDS
```

AWS manages much of the underlying database infrastructure.

---

## RDS vs EC2

```text
Want managed DB
      ↓
RDS

Need full OS/root access
      ↓
Database on EC2
```

---

## Multi-AZ

```text
Primary RDS - AZ-A
       |
       | Synchronous Replication
       v
Standby RDS - AZ-B
```

Purpose:

```text
HIGH AVAILABILITY
       +
AUTOMATIC FAILOVER
```

---

## Read Replica

```text
Primary
   |
   | Asynchronous Replication
   v
Read Replica
```

Purpose:

```text
READ SCALING
```

---

## Multi-AZ vs Read Replica

```text
DB/AZ Failure
     ↓
Multi-AZ

High SELECT Load
     ↓
Read Replica

Both
     ↓
Multi-AZ + Read Replica
```

---

## Automated Backups

```text
RDS
 ↓
Automated Backup
 ↓
PITR
```

Use for:

```text
Restore to specific point in time
```

---

## Manual Snapshot

```text
RDS
 ↓
Manual Snapshot
 ↓
Keep until manually deleted
```

Use before:

- Major upgrade
- Risky database change
- Major application deployment

---

## PITR

```text
10:36 Healthy
   ↓
10:37 Accidental Delete
   ↓
Restore to ~10:36
   ↓
New RDS Instance
```

---

## RDS Security

```text
Internet
   ↓
ALB
Public Subnet
   ↓
EC2
Private Subnet
APP-SG
   ↓
RDS
Private DB Subnet
DB-SG
```

DB-SG:

```text
DB Port
Source: APP-SG
```

---

## Encryption

```text
At Rest
   ↓
AWS KMS

In Transit
   ↓
SSL/TLS
```

---

## RDS Endpoint

```text
Application
     ↓
RDS DNS Endpoint
     ↓
Current Primary DB
```

Do not hard-code database IP addresses.

---

## RDS Proxy

```text
Application / Lambda
        ↓
    RDS Proxy
        ↓
Connection Pool
        ↓
       RDS
```

Use when:

```text
Too many DB connections
       ↓
RDS Proxy
```

---

## RDS Exam Triggers
```text
|        Question clue           |        Answer           |
|--------------------------------|---------------------    |
| Managed relational database    | RDS                     |
| Full OS access                 | DB on EC2               |
| AZ failure                     | Multi-AZ                |
| Automatic failover             | Multi-AZ                |
| Read-heavy workload            | Read Replica            |
| Many SELECT queries            | Read Replica            |
| HA + read scaling              | Multi-AZ + Read Replica |
| Too many connections           | RDS Proxy               |
| Restore to specific time       | PITR                    |
| Automatic backup               | Automated Backups       |
| Backup until manually deleted  | Manual Snapshot         |
| DB should not face internet    | Private Subnets         |
| Only app servers access DB     | DB-SG ← APP-SG          |
| Encryption at rest             | KMS                     |
| Encryption in transit          | SSL/TLS                 |
```



# AWS VPC Advanced Networking Quick Reference

## Internet Gateway

```text
Public Resource
      ↓
Internet Gateway
      ↓
Internet
```

Public subnet route:

```text
0.0.0.0/0 → IGW
```

---

## NAT Gateway

```text
Private EC2
     ↓
NAT Gateway
     ↓
Internet Gateway
     ↓
Internet
```

Private subnet:

```text
0.0.0.0/0 → NAT Gateway
```

NAT Gateway:

```text
Public Subnet
+ Elastic IP
```

---

## Highly Available NAT

```text
AZ-A
Private Subnet → NAT GW-A

AZ-B
Private Subnet → NAT GW-B
```

Production:

```text
One NAT Gateway per AZ
```

---

## Route Tables

```text
VPC CIDR → local

Public subnet:
0.0.0.0/0 → IGW

Private subnet:
0.0.0.0/0 → NAT Gateway
```

---

## VPC Endpoint

```text
Private AWS Service Access
         ↓
    VPC Endpoint
```

---

## Gateway Endpoint

```text
S3
DynamoDB
    ↓
Gateway Endpoint
```

No NAT Gateway required for endpoint traffic.

---

## Interface Endpoint

```text
Many AWS Services
       ↓
Interface Endpoint
       ↓
AWS PrivateLink
       ↓
ENI + Private IP
```

---

## VPC Peering

```text
VPC-A ←→ VPC-B
```

Private VPC-to-VPC connectivity.

Important:

```text
NON-TRANSITIVE
```

---

## Transit Gateway

```text
         VPC-A
           |
VPC-B ── TGW ── VPC-C
           |
         VPC-D
```

Use for:

```text
Many VPCs
+
Central Networking Hub
```

---

## Security Group

```text
Resource / ENI Level
STATEFUL
ALLOW only
```

---

## NACL

```text
Subnet Level
STATELESS
ALLOW + DENY
```

---

## Bastion Host

```text
Admin
 ↓ SSH
Bastion
 ↓ SSH
Private EC2
```

Modern alternative:

```text
AWS Systems Manager
Session Manager
```

---

## Longest Prefix Match

```text
/32
 ↓
/24
 ↓
/16
 ↓
/0
```

Most specific matching route wins.

Example:

```text
10.0.0.0/16 → local
10.0.1.0/24 → Peering
0.0.0.0/0   → NAT

Destination = 10.0.1.50

Winner:
10.0.1.0/24 → Peering
```

---

## Exam Triggers

|           Requirement                 |       Answer       |
|---------------------------------------|--------------------|
| Public subnet internet route          | Internet Gateway   |
| Private EC2 outbound IPv4 internet    | NAT Gateway        |
| Highly available NAT                  | NAT Gateway per AZ |
| Private access to S3                  | Gateway Endpoint   |
| Private access to DynamoDB            | Gateway Endpoint   |
| Private access to many AWS services   | Interface Endpoint |
| ENI + private endpoint IP             | Interface Endpoint |
| PrivateLink                           | Interface Endpoint |
| Connect two VPCs                      | VPC Peering        |
| Many VPCs centrally                   | Transit Gateway    |
| Stateful firewall                     | Security Group     |
| Stateless subnet control              | NACL               |
| Explicit network Deny                 | NACL               |
| Traditional private EC2 SSH access    | Bastion Host       |
| No inbound SSH administration         | SSM Session Manager|
| Multiple matching routes              | Longest Prefix Match|
| Most specific route                   | Highest matching prefix length |

---

## Production VPC

```text
                    Internet
                       ↓
                Internet Gateway
                       ↓
             Internet-Facing ALB
                 Public Subnets
                  /           \
               AZ-A           AZ-B
                ↓              ↓
          Private EC2     Private EC2
              ASG             ASG
                ↓              ↓
             APP-SG          APP-SG
                  \           /
                   \         /
                    ↓       ↓
                  RDS Multi-AZ
                  Private DB
                     DB-SG
```

Outbound internet:

```text
Private EC2-A → NAT GW-A → IGW

Private EC2-B → NAT GW-B → IGW
```

S3:

```text
Private EC2
     ↓
S3 Gateway Endpoint
     ↓
Amazon S3
```

Database:

```text
APP-SG
   ↓
DB Port
   ↓
DB-SG
```



# CloudWatch + CloudTrail + SNS Quick Reference

## CloudWatch

```text
AWS Resource
     ↓
CloudWatch
     ↓
Metrics / Logs / Alarms / Dashboards
```

Think:

```text
CloudWatch
    ↓
WHAT is happening?
```

---

## CloudTrail

```text
AWS API Activity
      ↓
CloudTrail
      ↓
Who + What + When
```

Think:

```text
CloudTrail
    ↓
WHO did WHAT?
```

---

## SNS

```text
CloudWatch Alarm
       ↓
SNS Topic
       ↓
Operations Team
```

Think:

```text
SNS
 ↓
Notify
```

---

## EC2 Monitoring

```text
CPU
 ↓
Standard CloudWatch Metric

Memory
 ↓
CloudWatch Agent
 ↓
CloudWatch Metric

Disk Space
 ↓
CloudWatch Agent
 ↓
CloudWatch Metric

Application Logs
 ↓
CloudWatch Agent
 ↓
CloudWatch Logs
```

---

## Alarm Flow

```text
Resource
   ↓
Metric
   ↓
CloudWatch
   ↓
Alarm
   ↓
SNS
   ↓
Operations
```

---

## Application ERROR Alert

```text
Application
     ↓
CloudWatch Logs
     ↓
Metric Filter
"ERROR"
     ↓
CloudWatch Metric
     ↓
CloudWatch Alarm
     ↓
SNS
     ↓
Email
```

---

## ALB 5xx

```text
HTTPCode_ELB_5XX_Count
        ↓
ALB generated error

HTTPCode_Target_5XX_Count
        ↓
Backend target generated error
```

---

## RDS

```text
CPUUtilization
DatabaseConnections
FreeStorageSpace
ReadIOPS
WriteIOPS
Latency
      ↓
CloudWatch Metrics
```

---

## Exam Triggers

| Requirement | Answer |
|---|---|
| EC2 CPU | CloudWatch Metric |
| EC2 memory | CloudWatch Agent |
| EC2 disk-space utilization | CloudWatch Agent |
| EC2 application logs | Agent + CloudWatch Logs |
| Search ERROR logs | CloudWatch Logs |
| Count ERROR logs | Metric Filter |
| Threshold monitoring | CloudWatch Alarm |
| Email operations | SNS |
| Central monitoring screen | CloudWatch Dashboard |
| ALB 5xx monitoring | CloudWatch Metrics |
| RDS connections | CloudWatch Metrics |
| Who terminated EC2? | CloudTrail |
| Who changed Security Group? | CloudTrail |
| AWS API audit | CloudTrail |
| Memory-based Auto Scaling | Agent → Metric → Auto Scaling |
```

### Memory shortcut

```text
Metrics = NUMBERS

Logs = EVENTS / TEXT

Alarm = THRESHOLD

SNS = NOTIFY

Dashboard = VISUALIZE

CloudTrail = AUDIT
```
