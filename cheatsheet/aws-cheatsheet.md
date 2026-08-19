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
| Question clue | Answer |
|---|---|
| Managed relational database | RDS |
| Full OS access | DB on EC2 |
| AZ failure | Multi-AZ |
| Automatic failover | Multi-AZ |
| Read-heavy workload | Read Replica |
| Many SELECT queries | Read Replica |
| HA + read scaling | Multi-AZ + Read Replica |
| Too many connections | RDS Proxy |
| Restore to specific time | PITR |
| Automatic backup | Automated Backups |
| Backup until manually deleted | Manual Snapshot |
| DB should not face internet | Private Subnets |
| Only app servers access DB | DB-SG ← APP-SG |
| Encryption at rest | KMS |
| Encryption in transit | SSL/TLS |
```
