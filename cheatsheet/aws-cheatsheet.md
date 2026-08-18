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
