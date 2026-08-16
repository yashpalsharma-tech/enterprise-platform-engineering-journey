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

```text
ALB
 |
 +-----------------------+
 |                       |
API Target Group      Auth Target Group
 |                       |
 +----+----+              +----+----+
 |         |              |         |
EC2-1    EC2-2           EC2-3    EC2-4

```

Each Target Group can have its own:

Targets

Health checks

Port

Scaling configuration

**5. Listeners & Listener Rules**

A Listener receives incoming connection requests on a configured protocol and port.

Common examples:

HTTP  → Port 80
HTTPS → Port 443

The listener evaluates the configured rules and determines where the request should be routed.

Request flow:

```text
User
 |
 v
ALB Listener
 |
 v
Listener Rule
 |
 v
Target Group
 |
 v
Healthy Target

```

Listener rules can use conditions such as:

URL path

Hostname

HTTP headers

Query parameters

Source IP

**6. Path-Based Routing**

Path-based routing routes requests based on the URL path.

Example:
/api/*       → API Target Group

/login/*     → Authentication Target Group

/payments/*  → Payment Target Group


**7. Host-Based Routing**

Host-based routing routes requests based on the hostname.

Example:

```text
api.company.com
        ↓
API Target Group

login.company.com
        ↓
Auth Target Group

payments.company.com
        ↓
Payment Target Group

```

**8. Default Listener Rule**

Listener rules are evaluated according to their configured priority.

Example:

Priority 1 → /api/*       → API Target Group

Priority 2 → /login/*     → Auth Target Group

Priority 3 → /payments/*  → Payment Target Group

Default     → Everything else → Web Target Group

If a request does not match any specific listener rule, the ALB uses the default rule.


**9. Blue/Green Deployment**

Blue/Green deployment uses two separate environments:

Blue → Current production version

Green → New application version

Example:

```text
                    ALB
                     |
          +----------+----------+
          |                     |
     Blue Target Group     Green Target Group
          |                     |
      Version 1              Version 2

```

Benefits:

Minimal or zero downtime

Safer deployments

Easy rollback

Ability to test the new version before production traffic is switched


**10. Sticky Sessions**

Sticky Sessions, also called session affinity, allow the ALB to associate a user's requests with the same target for the configured stickiness duration.

```text
User
 |
 +-- Request 1 → ALB → EC2-1
 |
 +-- Request 2 → ALB → EC2-1
 |
 +-- Request 3 → ALB → EC2-1

```

Sticky sessions can be useful when an application stores session information locally on an EC2 instance.

However, relying heavily on sticky sessions can make scaling and failover more difficult.

**11. Stateless Applications**

A stateless application does not depend on session information stored locally on a specific EC2 instance.

Instead, shared session/state information can be stored in an external service such as:

Amazon ElastiCache

Database

Other centralized session stores

Example:

```text

              ALB
               |
        +------+------+
        |             |
      EC2-1         EC2-2
        |             |
        +------+------+
               |
        Shared Session Store

```

Benefits:

Easier horizontal scaling,
Better fault tolerance,
Easier EC2 replacement,
Better Auto Scaling compatibility,
Any healthy EC2 instance can handle the request.

Production preference: Prefer stateless application architecture where practical instead of depending on sticky sessions.

**12. Production Scenarios**

**Scenario 1: Sudden Traffic Increase**

Problem:

A single EC2 instance cannot handle a sudden increase in traffic.

Solution:

Application Load Balancer

Auto Scaling Group

Multiple EC2 instances

CloudWatch monitoring

**Scenario 2: EC2 Instance Failure**

If an EC2 instance becomes unhealthy:

ALB detects the unhealthy target through health checks.
ALB stops routing user traffic to the unhealthy target.
ASG can replace the unhealthy EC2 instance.
New instance starts using the Launch Template/AMI.
New instance passes the ALB health check.
ALB starts routing traffic to the new healthy instance.

**Scenario 3: Availability Zone Failure**

Deploy EC2 instances across multiple Availability Zones.

Example:

```text

          ALB
           |
      +----+----+
      |         |
     AZ-A      AZ-B
      |         |
    EC2-1     EC2-2

```
If AZ-A fails, ALB can route traffic to healthy targets in AZ-B.

The ASG can launch replacement instances according to the configured capacity and Availability Zone distribution.

**Scenario 4: Entire AWS Region Failure**

An ALB cannot protect against an entire AWS Region failure because the ALB is deployed within an AWS Region.

For regional disaster recovery:

```text

Users
  |
  v
Route 53
  |
  +-------------------+
  |                   |
Singapore           Sydney
  |                   |
ALB                 ALB
  |                   |
EC2                 DR EC2

```

Route 53 can be configured with appropriate routing and health checks to direct new DNS queries toward the DR Region when the primary Region is unavailable.


**Scenario 5: Blue/Green Deployment Failure**

If the Green environment is deployed but starts producing errors:

The ALB listener can be changed to route traffic back to the Blue Target Group.


**13. ALB vs CloudWatch**
**ALB**

Responsible for:

Traffic routing
Listener rules
Target groups
Health checks
Sending traffic to healthy targets

**CloudWatch**

Responsible for:

Monitoring
Metrics
Alarms
Scaling triggers

**Auto Scaling Group**

Responsible for:

Maintaining desired capacity
Launching instances
Replacing unhealthy instances
Scaling based on configured policies
