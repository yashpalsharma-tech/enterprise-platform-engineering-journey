# Amazon Elastic Load Balancer (ELB)

## What is Elastic Load Balancer?

Amazon Elastic Load Balancer (ELB) is a managed AWS service that automatically distributes incoming application traffic across 
multiple healthy targets such as EC2 instances, containers and IP addresses.

---

## Why do we need a Load Balancer?

Without a Load Balancer:

- Single EC2 instance can become overloaded
- Poor response time
- Single Point of Failure
- Application downtime
- No automatic traffic distribution

Benefits:

- High Availability
- Fault Tolerance
- Scalability
- Improved Performance
- Automatic Health Checks

---

## Types of Load Balancers

### Application Load Balancer (ALB)
- Layer 7 (HTTP/HTTPS)
- URL-based Routing
- Host-based Routing
- Supports Microservices

### Network Load Balancer (NLB)
- Layer 4 (TCP/UDP)
- Ultra-low latency
- Millions of requests/sec

### Gateway Load Balancer (GWLB)
- Used with virtual firewalls
- Network appliances

### Classic Load Balancer (Legacy)
- Older generation
- Rarely used for new deployments

---

## Application Load Balancer

Responsibilities:

- Distributes requests
- Performs Health Checks
- Sends traffic only to healthy targets
- Works with Auto Scaling Groups
- Supports Path-based Routing
- Supports Host-based Routing

---

## Health Checks

ALB performs periodic HTTP/HTTPS health checks.

Example:

GET /health

Healthy Response:

HTTP 200 OK

If health checks fail:

- Instance marked unhealthy
- Traffic stopped
- Auto Scaling replaces failed instance (if configured)

---

## ALB and CloudWatch

ALB does NOT use CloudWatch to determine instance health.

ALB Health Checks
- HTTP/HTTPS requests

CloudWatch
- CPU Utilization
- Network
- Metrics
- Alarms
- Auto Scaling

---

## ALB + Auto Scaling

1. ALB performs Health Check.
2. EC2 becomes unhealthy.
3. ALB stops sending traffic.
4. ASG launches replacement EC2.
5. New EC2 passes Health Check.
6. ALB starts routing traffic.

---

## High Availability

Deploy:

- Multiple Availability Zones
- Auto Scaling Group
- Application Load Balancer

Benefits:

- No Single Point of Failure
- Automatic Failover
- Fault Tolerance

---

## Regional Disaster

ALB protects against:

- EC2 failures
- AZ failures

ALB cannot protect against:

- Complete AWS Region failure

Use:

Amazon Route53

↓

Another ALB

↓

DR Region


# Real Production Scenarios

## Scenario 1

Single EC2 server becomes overloaded during traffic spike.

Solution:

- Application Load Balancer
- Auto Scaling Group
- CloudWatch
- Launch Template

---

## Scenario 2

One EC2 instance becomes unhealthy.

Solution:

ALB stops routing traffic.

ASG launches replacement EC2.

---

## Scenario 3

One Availability Zone fails.

Solution:

ALB routes traffic to healthy EC2 instances in another AZ.

ASG maintains desired capacity.

---

## Scenario 4

Entire AWS Region fails.

Solution:

Use Route53 Failover Routing.

Deploy another ALB in DR Region.

Fail over traffic to DR site.


# AWS Load Balancer

## 1. What is Elastic Load Balancer?

Amazon Elastic Load Balancing (ELB) is a managed AWS service that distributes incoming application traffic across multiple healthy targets such as EC2 instances.

Benefits:

- High Availability
- Fault Tolerance
- Scalability
- Improved application performance
- Automatic health checks

---

## 2. Why Do We Need a Load Balancer?

A single EC2 instance can become overloaded when traffic increases.

A Load Balancer distributes incoming requests across multiple healthy EC2 instances.

```text
Users
   |
   v
Application Load Balancer
   |
   +--------+--------+
   |        |        |
 EC2-1    EC2-2    EC2-3

```

**3. Types of AWS Load Balancers**

Application Load Balancer (ALB)
Layer 7
HTTP/HTTPS
Path-based routing
Host-based routing
Suitable for web applications and microservices

Network Load Balancer (NLB)
Layer 4
TCP/UDP/TLS
High performance
Very low latency

Gateway Load Balancer (GWLB)
Used for virtual network appliances
Firewalls
Intrusion detection/prevention systems
Security appliances

Classic Load Balancer (CLB)
Older generation load balancer
Legacy service
Not recommended for new architectures
