# AWS Monitoring & Observability

This module covers:

- Amazon CloudWatch
- CloudWatch Metrics
- CloudWatch Agent
- CloudWatch Logs
- CloudWatch Alarms
- CloudWatch Logs Metric Filters
- CloudWatch Dashboards
- Amazon SNS
- AWS CloudTrail
- Monitoring EC2, ALB and RDS

---

# 1. Amazon CloudWatch

Amazon CloudWatch is an AWS monitoring and observability service.

It can be used to:

- Monitor AWS resources
- Collect metrics
- Collect logs
- Create alarms
- Build dashboards
- Detect operational problems
- Trigger actions and notifications

Basic architecture:

```text
AWS Resources
    |
    +--> EC2
    +--> ALB
    +--> RDS
    |
    v
Amazon CloudWatch
    |
    +--> Metrics
    +--> Logs
    +--> Alarms
    +--> Dashboards
```

---

# 2. CloudWatch Metrics

A metric represents numerical data measured over time.

Examples:

```text
EC2
├── CPUUtilization
├── NetworkIn
└── NetworkOut

ALB
├── RequestCount
├── TargetResponseTime
├── HTTPCode_ELB_5XX_Count
└── HTTPCode_Target_5XX_Count

RDS
├── CPUUtilization
├── DatabaseConnections
├── FreeStorageSpace
├── ReadIOPS
├── WriteIOPS
├── ReadLatency
└── WriteLatency
```

Think:

```text
CloudWatch Metrics
        ↓
"Numbers over time"
```

---

# 3. EC2 Standard Metrics

EC2 automatically provides several infrastructure metrics to CloudWatch.

Examples include:

```text
CPUUtilization
NetworkIn
NetworkOut
DiskReadOps / DiskWriteOps
(for applicable instance-store metrics)
```

However, operating-system metrics such as memory utilization are not standard EC2 metrics.

Important exam clue:

```text
EC2 CPU
   ↓
Standard CloudWatch Metric

EC2 Memory
   ↓
CloudWatch Agent
```

---

# 4. CloudWatch Agent

The CloudWatch Agent can be installed and configured inside EC2 instances to collect additional operating-system metrics and logs.

Examples:

```text
EC2
 |
 +--> Memory Utilization
 |
 +--> Disk Space Utilization
 |
 +--> OS Logs
 |
 +--> Application Logs
          |
          v
   CloudWatch Agent
```

Metrics:

```text
CloudWatch Agent
      ↓
CloudWatch Metrics
```

Logs:

```text
CloudWatch Agent
      ↓
CloudWatch Logs
```

Exam shortcut:

```text
Memory utilization
Disk-space utilization
Application log files
        ↓
CloudWatch Agent
```

---

# 5. CloudWatch Logs

CloudWatch Logs provides centralized storage and monitoring of log data.

Example:

```text
EC2 Application
      |
      | application.log
      v
CloudWatch Agent
      |
      v
CloudWatch Logs
```

Instead of administrators connecting individually to every EC2 instance:

```text
EC2-1 ──┐
EC2-2 ──┼──→ CloudWatch Logs
EC2-3 ──┘
```

Logs can contain:

```text
INFO User login successful

ERROR Database connection failed

ERROR Payment service timeout
```

---

# 6. Log Groups and Log Streams

CloudWatch Logs organizes logs using Log Groups and Log Streams.

Example:

```text
Log Group:
/production/webapp

    |
    +--> Log Stream: EC2-instance-01
    |
    +--> Log Stream: EC2-instance-02
    |
    +--> Log Stream: EC2-instance-03
```

A Log Group groups related logs.

A Log Stream is a sequence of log events from a particular source.

---

# 7. CloudWatch Alarms

A CloudWatch Alarm monitors a metric and evaluates it against a configured threshold.

Example:

```text
EC2
 |
 | CPUUtilization
 v
CloudWatch Metric
 |
 v
CloudWatch Alarm

CPU > 80%
for 5 minutes
 |
 v
ALARM
```

CloudWatch Alarm states include:

```text
OK
ALARM
INSUFFICIENT_DATA
```

### OK

The metric is within the defined condition.

### ALARM

The configured threshold has been breached according to the alarm configuration.

### INSUFFICIENT_DATA

There is not enough data available to determine the alarm state.

---

# 8. CloudWatch Alarm + SNS

CloudWatch Alarms can integrate with Amazon SNS to notify operations teams.

Example:

```text
EC2 CPU
   |
   v
CloudWatch Metric
   |
   v
CloudWatch Alarm
CPU > 80%
   |
   v
Amazon SNS
   |
   v
Operations Team
```

Memory shortcut:

```text
Metric
  ↓
Alarm
  ↓
SNS
  ↓
People
```

---

# 9. Amazon SNS

Amazon Simple Notification Service (SNS) is a publish/subscribe messaging service.

Basic architecture:

```text
Publisher
    |
    v
SNS Topic
    |
    +--> Email
    |
    +--> SMS
    |
    +--> Lambda
    |
    +--> SQS
    |
    +--> HTTP/S Endpoint
```

Monitoring example:

```text
CloudWatch Alarm
       |
       v
    SNS Topic
       |
       v
Operations Team
```

---

# 10. CloudWatch Logs Metric Filters

Metric Filters can convert patterns found in CloudWatch Logs into CloudWatch metrics.

Example application log:

```text
INFO User login
ERROR Payment failed
INFO Order created
ERROR Database timeout
ERROR Payment failed
```

Metric Filter:

```text
Pattern:
ERROR
```

Architecture:

```text
Application
     |
     v
CloudWatch Logs
     |
     v
Metric Filter
Pattern = ERROR
     |
     v
CloudWatch Metric
ErrorCount
     |
     v
CloudWatch Alarm
     |
     v
Amazon SNS
     |
     v
Operations Team
```

Exam clue:

```text
Count occurrences of ERROR
inside application logs
        ↓
CloudWatch Logs Metric Filter
```

---

# 11. CloudWatch Dashboards

CloudWatch Dashboards provide a centralized visual view of operational metrics.

Example:

```text
             CloudWatch Dashboard
                     |
       +-------------+-------------+
       |             |             |
       v             v             v
      EC2           ALB           RDS
       |             |             |
      CPU        RequestCount     CPU
    Network        5xx Errors   Connections
                              FreeStorageSpace
```

Use when:

```text
"Show important metrics
in one centralized screen"
        ↓
CloudWatch Dashboard
```

---

# 12. ALB Monitoring

Application Load Balancers publish operational metrics to CloudWatch.

Important examples:

```text
RequestCount
TargetResponseTime
HTTPCode_ELB_5XX_Count
HTTPCode_Target_5XX_Count
```

Important distinction:

```text
HTTPCode_ELB_5XX_Count
        ↓
5xx generated by ALB
```

versus:

```text
HTTPCode_Target_5XX_Count
        ↓
5xx responses from targets
such as EC2 applications
```

Example:

```text
HTTPCode_ELB_5XX_Count    = 0

HTTPCode_Target_5XX_Count = 1250
```

Likely investigation area:

```text
Backend Targets / Application
```

---

# 13. RDS Monitoring

RDS publishes many operational metrics to CloudWatch.

Examples:

```text
Amazon RDS
    |
    +--> CPUUtilization
    +--> DatabaseConnections
    +--> FreeStorageSpace
    +--> ReadIOPS
    +--> WriteIOPS
    +--> ReadLatency
    +--> WriteLatency
            |
            v
     Amazon CloudWatch
```

Example monitoring flow:

```text
RDS
 ↓
CloudWatch Metric
 ↓
CloudWatch Alarm
 ↓
SNS
 ↓
DBA / Operations
```

Important:

```text
RDS DatabaseConnections
        ↓
CloudWatch Metric
```

A CloudWatch Agent on RDS is not required to obtain this standard RDS metric.

---

# 14. AWS CloudTrail

AWS CloudTrail records AWS API and account activity for auditing and investigation.

CloudTrail can help answer:

```text
WHO performed the action?

WHAT action was performed?

WHEN was it performed?

Which API action was called?

What resource was affected?
```

Example:

```text
IAM User / Role
      |
      | TerminateInstances
      v
AWS API
      |
      v
AWS CloudTrail
      |
      v
Audit Event
```

Typical questions:

```text
Who terminated EC2?

Who modified a Security Group?

Who deleted an AWS resource?

Which IAM identity made an API call?

When did the change occur?
```

Answer:

```text
AWS CloudTrail
```

---

# 15. CloudWatch vs CloudTrail

This is an important certification distinction.

## CloudWatch

Answers:

```text
"What is happening
to my resources/applications?"
```

Examples:

- CPU utilization
- Network activity
- RDS connections
- ALB 5xx errors
- Application logs
- Alarms

## CloudTrail

Answers:

```text
"Who did what
in my AWS environment?"
```

Examples:

- Who terminated EC2?
- Who changed a Security Group?
- Who made an API call?
- When was a resource changed?

Memory trick:

```text
CloudWATCH
    ↓
WATCH resources/applications

CloudTRAIL
    ↓
TRAIL of AWS activity
```

---

# 16. EC2 Memory-Based Auto Scaling

Memory utilization is not a standard EC2 CloudWatch metric.

To scale based on memory:

```text
EC2
 |
 v
CloudWatch Agent
 |
 v
Memory Utilization Metric
 |
 v
CloudWatch
 |
 v
Auto Scaling Policy / Alarm
 |
 v
Auto Scaling Group
 |
 v
Scale Out / Scale In
```

Exam clue:

```text
Auto Scale EC2
based on memory
       ↓
CloudWatch Agent
       ↓
Memory Metric
       ↓
Auto Scaling
```

---

# 17. Production Monitoring Architecture

Example production application:

```text
Users
  |
  v
ALB
  |
  v
EC2 Auto Scaling Group
  |
  v
RDS
```

Monitoring architecture:

```text
EC2
 |
 +--> CPU --------------------→ CloudWatch Metrics
 |
 +--> Memory
 |       |
 |       v
 |  CloudWatch Agent
 |       |
 |       v
 |  CloudWatch Metrics
 |
 +--> Application Logs
         |
         v
    CloudWatch Agent
         |
         v
    CloudWatch Logs


ALB
 |
 +--> RequestCount
 +--> TargetResponseTime
 +--> 5xx Errors
         |
         v
    CloudWatch Metrics


RDS
 |
 +--> CPU
 +--> Connections
 +--> Storage
 +--> IOPS
 +--> Latency
         |
         v
    CloudWatch Metrics
```

Alerting:

```text
CloudWatch Metric
       |
       v
CloudWatch Alarm
       |
       v
Amazon SNS
       |
       v
Operations Team
```

Auditing:

```text
AWS API Activity
       |
       v
AWS CloudTrail
       |
       v
Who + What + When
```

Visualization:

```text
EC2 Metrics ---+
               |
ALB Metrics ---+--> CloudWatch Dashboard
               |
RDS Metrics ---+
```

---

# 18. Monitoring Problem-to-Solution Mapping

| Requirement                   | AWS Solution                       |
| ----------------------------- | ---------------------------------- |
| Monitor EC2 CPU               | CloudWatch Metrics                 |
| Monitor EC2 network           | CloudWatch Metrics                 |
| Monitor EC2 memory            | CloudWatch Agent                   |
| Monitor filesystem disk space | CloudWatch Agent                   |
| Collect EC2 application logs  | CloudWatch Agent + CloudWatch Logs |
| Search application errors     | CloudWatch Logs                    |
| Count ERROR occurrences       | CloudWatch Logs Metric Filter      |
| Detect metric threshold       | CloudWatch Alarm                   |
| Send notifications            | Amazon SNS                         |
| Monitor ALB 5xx               | CloudWatch Metrics                 |
| Monitor RDS connections       | CloudWatch Metrics                 |
| Monitor RDS CPU               | CloudWatch Metrics                 |
| Central metrics view          | CloudWatch Dashboard               |
| Audit AWS API activity        | CloudTrail                         |
| Find who changed SG           | CloudTrail                         |
| Find who terminated EC2       | CloudTrail                         |


---

# 19. Certification Quick Patterns

```text
EC2 CPU?
    ↓
CloudWatch Metric

EC2 Memory?
    ↓
CloudWatch Agent

EC2 Application Logs?
    ↓
CloudWatch Agent
    ↓
CloudWatch Logs

Search ERROR?
    ↓
CloudWatch Logs

Count ERROR events?
    ↓
Metric Filter

Threshold breached?
    ↓
CloudWatch Alarm

Notify Operations?
    ↓
SNS

ALB 5xx?
    ↓
CloudWatch Metrics

RDS DatabaseConnections?
    ↓
CloudWatch Metrics

Who changed something?
    ↓
CloudTrail

One monitoring screen?
    ↓
CloudWatch Dashboard
```
