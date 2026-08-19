# Amazon RDS

## 1. What is Amazon RDS?

Amazon RDS (Relational Database Service) is a managed relational database service provided by AWS.

AWS manages many infrastructure and operational tasks such as:

- Database infrastructure provisioning
- Operating system maintenance
- Database software patching
- Automated backups
- Monitoring integrations
- High availability through Multi-AZ deployments

The customer still manages areas such as:

- Database schema
- Tables
- Indexes
- SQL queries
- Database users and permissions
- Application database connections
- Application/database performance tuning

---

# 2. RDS vs Database on EC2

A relational database can either run using a managed service such as RDS or be installed directly on EC2.

## Amazon RDS

Choose RDS when you want AWS to manage much of the underlying database infrastructure.

```text
Application
     |
     v
Amazon RDS
     |
     v
AWS Managed Infrastructure
```

Advantages:

- Managed backups
- Managed patching
- Multi-AZ support
- Automated failover
- Monitoring integration
- Reduced infrastructure administration

---

## Database on EC2

Choose EC2 when you require greater control over the database host.

```text
Application
     |
     v
EC2
     |
     v
Database Software
```

The customer manages:

- Operating system
- OS patching
- Database installation
- Database patching
- Backups
- High availability architecture
- Host-level software

Exam clue:

```text
Managed database
      ↓
Amazon RDS

Full OS / root access
      ↓
Database on EC2
```

---

# 3. RDS Database Engines

Amazon RDS supports several relational database engines, including:

- Amazon Aurora
- PostgreSQL
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- IBM Db2

---

# 4. RDS Multi-AZ

RDS Multi-AZ is primarily used for:

- High availability
- Database resilience
- Automatic failover

Typical architecture:

```text
Application
     |
     v
RDS Endpoint
     |
     v
Primary RDS
    AZ-A
     |
     | Synchronous Replication
     v
Standby RDS
    AZ-B
```

If the primary database or Availability Zone fails:

```text
Primary RDS
   FAILED
      |
      v
Automatic Failover
      |
      v
Standby becomes Primary
```

The application continues using the RDS DNS endpoint.

Important:

```text
Multi-AZ
   ↓
HIGH AVAILABILITY
```

Multi-AZ should not be confused with Read Replicas.

---

# 5. RDS Read Replicas

Read Replicas are primarily used for read scalability.

Example:

```text
                  Application
                      |
              +-------+-------+
              |               |
            WRITES           READS
              |               |
              v               v
         Primary RDS      Read Replica
              |
              | Asynchronous
              | Replication
              v
         Read Replica
```

Read-heavy workloads can send SELECT queries to Read Replicas.

Benefits:

- Reduce read load on primary
- Improve read scalability
- Support read-heavy applications

Important:

```text
Read Replica
     ↓
READ SCALING
```

A Read Replica does not provide the same automatic HA failover mechanism as a Multi-AZ standby.

A Read Replica can be promoted when appropriate, but should not be treated as equivalent to Multi-AZ automatic failover.

---

# 6. Multi-AZ vs Read Replica

| Feature | Multi-AZ | Read Replica |
|---|---|---|
| Primary purpose | High Availability | Read Scaling |
| Replication | Synchronous | Typically Asynchronous |
| Automatic failover | Yes | Not the same Multi-AZ failover mechanism |
| Application reads from copy | Standby generally not used for reads | Yes |
| Reduce SELECT workload | No | Yes |
| Protect against AZ failure | Yes | Not primary purpose |

Exam shortcut:

```text
Database/AZ Failure
       ↓
Multi-AZ

High Read Load
       ↓
Read Replica

Need Both
       ↓
Multi-AZ + Read Replicas
```

---

# 7. Automated Backups

RDS Automated Backups allow AWS to automatically back up the database.

They support Point-in-Time Recovery within the configured backup retention period.

Conceptually:

```text
RDS Database
     |
     v
Automated Backups
     |
     +--> Backup Data
     |
     +--> Transaction Logs
              |
              v
      Point-in-Time Recovery
```

Use when:

```text
"Restore database to a specific time"
              ↓
Automated Backups + PITR
```

---

# 8. Point-in-Time Recovery

Point-in-Time Recovery allows a database to be restored to a specific point within the configured retention period.

Example:

```text
10:00 AM  Database Healthy

10:36 AM  ← Restore Point

10:37 AM  Records Accidentally Deleted

10:45 AM  Problem Discovered
```

Restore:

```text
Automated Backups
       |
       | PITR to ~10:36
       v
New RDS DB Instance
```

Important:

PITR restores to a new DB instance rather than rewinding the existing DB instance in place.

---

# 9. Manual DB Snapshots

A Manual DB Snapshot is initiated by the customer.

Example:

```text
Production RDS
      |
      | Before Major Upgrade
      v
Manual Snapshot
      |
      v
Application Upgrade
```

Manual snapshots remain until explicitly deleted.

Typical use cases:

- Before application upgrades
- Before major database changes
- Long-term backup points
- Before risky maintenance

Exam clue:

```text
Backup automatically + PITR
          ↓
Automated Backup

Take backup NOW and retain
until manually deleted
          ↓
Manual Snapshot
```

---

# 10. RDS Security

Production databases should generally not be directly exposed to the public internet.

Typical architecture:

```text
Internet
   |
   v
ALB
Public Subnets
   |
   v
Application EC2
Private Subnets
   |
   v
Amazon RDS
Private DB Subnets
```

The application tier communicates with the database internally.

---

# 11. RDS Security Groups

Security Groups can restrict which application resources can connect to RDS.

Example:

```text
EC2 Application
     |
     | APP-SG
     |
     | TCP 3306
     v
Amazon RDS
     |
     | DB-SG
```

Example MySQL DB Security Group inbound rule:

```text
Protocol: TCP
Port: 3306
Source: APP-SG
```

Avoid:

```text
Port: 3306
Source: 0.0.0.0/0
```

for a private production database.

Exam clue:

```text
Only application servers
should access database
        ↓
DB-SG allows APP-SG
on database port
```

---

# 12. RDS Encryption at Rest

Amazon RDS supports encryption at rest using AWS KMS.

Conceptually:

```text
Amazon RDS
     |
     +--> Database Storage
     |
     +--> Automated Backups
     |
     +--> Snapshots
     |
     +--> Read Replicas
              |
              v
          Encryption
              |
              v
           AWS KMS
```

For an encrypted RDS DB instance, underlying storage is encrypted and associated backups, snapshots, and read replicas are also encrypted.

---

# 13. Encryption in Transit

Applications can use SSL/TLS to protect database traffic in transit.

```text
Application
     |
     | SSL / TLS
     v
Amazon RDS
```

Remember:

```text
Encryption at Rest
       ↓
AWS KMS

Encryption in Transit
       ↓
SSL / TLS
```

---

# 14. RDS Endpoint

Applications should connect to RDS using the RDS DNS endpoint rather than hard-coding database IP addresses.

Example:

```text
Application
     |
     v
RDS DNS Endpoint
     |
     v
Primary Database
```

With Multi-AZ failover:

```text
Primary AZ-A
   FAILED
      |
      v
Automatic Failover
      |
      v
Standby AZ-B becomes Primary
```

The application continues using the RDS endpoint.

---

# 15. RDS Proxy

Amazon RDS Proxy sits between an application and the database and manages database connections.

Example:

```text
Lambda Functions
      |
      | Many Connections
      v
   RDS Proxy
      |
      | Connection Pool
      | Reuses Connections
      v
     RDS
```

Benefits include:

- Database connection pooling
- Reusing connections
- Handling connection surges
- Reducing database connection overhead
- Improving application resilience around database connections

Common use case:

```text
Large number of Lambda invocations
            +
Too many DB connections
            ↓
        RDS Proxy
```

---

# 16. RDS Problem-to-Solution Mapping

| Problem | RDS Solution |
|---|---|
| AZ/database failure | Multi-AZ |
| Automatic database failover | Multi-AZ |
| High SELECT/read workload | Read Replica |
| Too many DB connections | RDS Proxy |
| Restore to specific time | PITR |
| Automatic backups | RDS Automated Backups |
| Backup kept until manually deleted | Manual Snapshot |
| Encryption at rest | AWS KMS |
| Restrict DB access to app servers | Security Groups |
| Full OS access required | Database on EC2 |

---

# 17. Production RDS Architecture

A highly available production application could use:

```text
Users
  |
  v
Route 53
  |
  v
Internet-Facing ALB
Public Subnets
  |
  v
EC2 Application Servers
Auto Scaling Group
Private Subnets
APP-SG
  |
  v
RDS DNS Endpoint
  |
  v
Amazon RDS Multi-AZ
Private DB Subnets
DB-SG
  |
  +--> Standby DB
  |    Another AZ
  |
  +--> Read Replica(s)
       Read Scaling

AWS KMS
  |
  v
RDS Encryption at Rest
```

Security:

```text
DB-SG
Inbound:
Database Port
Source: APP-SG
```

---

# 18. Multi-AZ + Read Replica Architecture

Use both when the application requires:

- High availability
- Automatic failover
- Read scalability

```text
                    Application
                        |
              +---------+---------+
              |                   |
            WRITES               READS
              |                   |
              v                   v
        Primary RDS          Read Replica
           AZ-A
              |
              | Synchronous
              | Replication
              v
        Multi-AZ Standby
           AZ-B
```

Multi-AZ:

```text
High Availability
```

Read Replica:

```text
Read Scalability
```

---

# 19. Important RDS Exam Patterns

```text
Managed relational database
        ↓
Amazon RDS

Full OS/root access required
        ↓
Database on EC2

AZ failure + automatic failover
        ↓
RDS Multi-AZ

Heavy SELECT workload
        ↓
Read Replica

High Availability + Read Scaling
        ↓
Multi-AZ + Read Replica

Restore database to specific time
        ↓
PITR

Take backup before major upgrade
        ↓
Manual Snapshot

Too many database connections
        ↓
RDS Proxy

Database should not be internet-facing
        ↓
Private DB Subnets

Only application servers need DB access
        ↓
DB-SG allows APP-SG

Encryption at rest
        ↓
AWS KMS

Encryption in transit
        ↓
SSL/TLS
```
