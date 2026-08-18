# Amazon S3

## 1. What is Amazon S3?

Amazon S3 (Simple Storage Service) is AWS object storage.

It is designed to store and retrieve objects such as:

- Images
- Documents
- Videos
- Log files
- Backup files
- Application artifacts
- Static website files

Basic structure:

```text
Amazon S3
   |
   └── Bucket
        |
        ├── Object
        ├── Object
        └── Object
```

Example:

```text
company-backups
   |
   ├── database-backup-01.bak
   ├── database-backup-02.bak
   └── database-backup-03.bak
```

`company-backups` = Bucket

`database-backup-01.bak` = Object

---

# 2. S3 Bucket

A bucket is a container used to store S3 objects.

For general-purpose S3 buckets, bucket names must be globally unique within an AWS partition.

Example:

```text
company-backups-prod-sg-2026
```

---

# 3. S3 Object

An object is the data stored inside an S3 bucket.

Examples:

```text
logo.png
employee-report.pdf
database-backup.bak
application.log
```

An object includes information such as:

- Object data
- Object key
- Metadata
- Version ID when versioning is used

---

# 4. S3 Storage Classes

S3 provides different storage classes for different access patterns and cost requirements.

## S3 Standard

Designed for frequently accessed data.

Examples:

- Active application files
- Frequently accessed images
- Frequently accessed documents

Think:

```text
Frequent Access
      ↓
S3 Standard
```

---

## S3 Standard-IA

IA = Infrequent Access.

Designed for data that is accessed infrequently but still requires immediate retrieval.

Examples:

- Backups
- Disaster recovery files
- Long-lived documents accessed occasionally

```text
Infrequent Access
       +
Immediate Retrieval
       ↓
S3 Standard-IA
```

Standard-IA stores data redundantly across multiple Availability Zones.

---

## S3 One Zone-IA

Designed for infrequently accessed data that can be stored in a single Availability Zone.

```text
Infrequent Access
       +
Immediate Retrieval
       +
Single AZ acceptable
       ↓
S3 One Zone-IA
```

Suitable for re-creatable data where multi-AZ resilience is not required.

It should generally not be used as the only copy of critical data that must survive an AZ failure.

---

## S3 Intelligent-Tiering

Designed for data with unknown or changing access patterns.

S3 automatically moves objects between appropriate access tiers based on access patterns.

```text
Unknown / Changing Access Pattern
              ↓
      Intelligent-Tiering
              ↓
Automatic Cost Optimization
```

Exam clue:

```text
Unknown access pattern
        ↓
S3 Intelligent-Tiering
```

---

# 5. S3 Glacier Storage Classes

Glacier storage classes are designed for archival data.

## S3 Glacier Instant Retrieval

Used for rarely accessed archive data that still requires millisecond retrieval.

```text
Archive
   +
Rarely Accessed
   +
Immediate Retrieval
       ↓
Glacier Instant Retrieval
```

---

## S3 Glacier Flexible Retrieval

Used for archive data where retrieval can take minutes to hours.

```text
Archive
   +
Minutes / Hours acceptable
       ↓
Glacier Flexible Retrieval
```

---

## S3 Glacier Deep Archive

Designed for very rarely accessed, long-term archival data where retrieval can take hours.

Examples:

- Compliance records
- Long-term financial records
- Historical backups
- Regulatory archives

```text
Very Rare Access
       +
Long-Term Retention
       +
Hours acceptable
       ↓
Glacier Deep Archive
```

---

# 6. Storage Class Selection

| Requirement | Storage Class |
|---|---|
| Frequently accessed | S3 Standard |
| Infrequent + immediate access + Multi-AZ | S3 Standard-IA |
| Infrequent + immediate access + Single AZ | S3 One Zone-IA |
| Unknown/changing access pattern | S3 Intelligent-Tiering |
| Archive + millisecond retrieval | Glacier Instant Retrieval |
| Archive + minutes/hours retrieval | Glacier Flexible Retrieval |
| Very long-term archive + hours acceptable | Glacier Deep Archive |

---

# 7. S3 Lifecycle Policy

S3 Lifecycle rules automate storage management.

They can:

- Transition objects between storage classes
- Transition noncurrent versions
- Expire/delete objects
- Expire old versions

Example:

```text
0–30 Days
S3 Standard
     |
     | After 30 days
     v
S3 Standard-IA
     |
     | After 365 days
     v
S3 Glacier
     |
     | After 7 years
     v
Expire / Delete
```

Important distinction:

```text
Known age-based transition rules
            ↓
    S3 Lifecycle Policy

Unknown/changing access patterns
            ↓
    S3 Intelligent-Tiering
```

---

# 8. S3 Versioning

S3 Versioning preserves multiple versions of an object.

Example:

```text
employee-report.pdf
       |
       ├── Version 1
       ├── Version 2
       └── Version 3 ← Current
```

Versioning helps protect against:

- Accidental overwrites
- Accidental deletions

---

# 9. Delete Markers

With versioning enabled, a normal delete operation without specifying a version ID normally creates a delete marker.

Example:

```text
report.pdf
   |
   ├── Version 1
   ├── Version 2
   └── Delete Marker ← Current
```

The object appears deleted, but previous versions remain.

A specific version can still be permanently deleted if someone with sufficient permissions explicitly deletes that version.

---

# 10. Versioning + Lifecycle

Lifecycle rules can manage noncurrent versions.

Example:

```text
report.pdf

Version 1 ─┐
Version 2  ├── Noncurrent
Version 3 ─┘
     |
     | After 90 days
     v
Expire old versions

Version 4 ← Current
```

This can reduce storage costs created by retaining many old versions.

---

# 11. S3 Encryption

S3 supports encryption of objects at rest.

Three important server-side encryption options:

- SSE-S3
- SSE-KMS
- SSE-C

---

## SSE-S3

Server-Side Encryption with Amazon S3 managed keys.

```text
Application
     |
     v
Amazon S3
     |
     | SSE-S3
     v
Encrypted Object
```

Think:

```text
Simple server-side encryption
          ↓
SSE-S3
```

---

## SSE-KMS

Server-Side Encryption using AWS KMS.

Provides greater control over encryption-key usage and supports KMS permissions, policies, and auditing capabilities.

```text
Application
     |
     v
Amazon S3
     |
     v
AWS KMS
     |
     v
Encrypted Object
```

Think:

```text
Need more control over encryption keys
              ↓
           SSE-KMS
```

---

## SSE-C

Server-Side Encryption with Customer-Provided Keys.

The customer provides and manages the encryption key while S3 performs encryption and decryption.

S3 does not store the SSE-C encryption key itself.

Think:

```text
Customer provides encryption key
              ↓
            SSE-C
```

---

# 12. Encryption at Rest vs In Transit

Encryption at rest:

```text
Stored S3 Object
      ↓
Encrypted
```

Encryption in transit:

```text
Client
  |
  | HTTPS / TLS
  v
Amazon S3
```

---

# 13. S3 Block Public Access

S3 Block Public Access provides controls designed to prevent accidental public exposure of S3 buckets and objects.

For sensitive data:

```text
Private S3 Bucket
       |
       └── Block Public Access
```

Examples:

- Payroll documents
- Employee information
- Financial data
- Internal backups

---

# 14. IAM Policy vs S3 Bucket Policy

## IAM Policy

An IAM policy is attached to an IAM identity such as a user or role.

Think:

```text
"What is this identity allowed to do?"
```

Example:

```text
EC2
 |
 | IAM Role
 | s3:GetObject
 v
Private S3 Bucket
```

---

## S3 Bucket Policy

A bucket policy is a resource-based policy attached to an S3 bucket.

Think:

```text
"Who can access this S3 resource,
and what can they do?"
```

Bucket policies can also be useful for cross-account access.

---

# 15. EC2 Access to S3

Applications running on EC2 should generally use an IAM role rather than storing long-term AWS access keys on the instance.

```text
EC2 Application
       |
       v
EC2 IAM Role
       |
       | Temporary Credentials
       |
       | s3:GetObject
       v
Private S3 Bucket
```

Apply least-privilege permissions.

---

# 16. S3 Replication

S3 supports automatic object replication between buckets.

Two important types:

- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)

---

## Cross-Region Replication

CRR replicates eligible objects between buckets in different AWS Regions.

Example:

```text
Singapore S3
      |
      | CRR
      v
Sydney S3
```

Use cases include:

- Disaster recovery
- Compliance
- Geographic separation
- Multi-Region requirements

Versioning must be enabled on both source and destination buckets for replication.

---

## Same-Region Replication

SRR replicates eligible objects between buckets in the same AWS Region.

```text
S3 Bucket A
     |
     | SRR
     v
S3 Bucket B

Same Region
```

---

# 17. S3 Durability vs Availability

## Durability

Think:

```text
"Will my stored object remain intact?"
```

S3 Standard is designed for:

```text
99.999999999%
11 nines durability
```

Durability relates to protection against data loss.

## Availability

Think:

```text
"Can I access the service/data when required?"
```

Availability and durability are different concepts.

---

# 18. Static Website Content

S3 can store and serve static website content.

Examples:

- HTML
- CSS
- JavaScript
- Images

Example:

```text
index.html
about.html
styles.css
logo.png
```

No EC2 server is required simply to store and serve static content.

For a production architecture with a private S3 origin, CloudFront can be placed in front of S3.

---

# 19. S3 + CloudFront + OAC

Production architecture:

```text
Users
   |
   v
Route 53
   |
   v
CloudFront
   |
   | Authorized using OAC
   v
Private S3 Bucket
```

Roles:

Route 53:
DNS resolution

CloudFront:
Global content delivery and caching

OAC:
Allows CloudFront authorized access to the private S3 origin

S3:
Stores static website objects

---

# 20. S3 Pre-Signed URLs

A pre-signed URL provides temporary access to a private S3 object.

Example:

```text
Private S3 Bucket
       |
       └── employee-payslip.pdf
                    |
                    | Pre-Signed URL
                    | Valid for 30 minutes
                    v
               Authorized User
```

The bucket does not need to be made public.

Exam clue:

```text
Private S3 object
       +
Temporary access
       ↓
Pre-Signed URL
```

---

# 21. Production S3 Security Example

Requirement:

- Sensitive payroll documents
- No public access
- Encryption at rest
- Greater encryption-key control
- Recover accidental overwrites
- EC2 application requires read access

Architecture:

```text
EC2 Application
      |
      | IAM Role
      | Least Privilege
      v
Private S3 Bucket
      |
      +── Block Public Access
      |
      +── SSE-KMS
      |
      +── Versioning
```

---

# 22. S3 Exam Quick Notes

```text
S3 = Object Storage

Bucket = Container for objects

Object = Data/file stored in S3

S3 Standard = Frequent access

Standard-IA = Infrequent + immediate retrieval

One Zone-IA = Infrequent + single AZ

Intelligent-Tiering = Unknown/changing access pattern

Glacier Instant Retrieval = Archive + milliseconds

Glacier Flexible Retrieval = Archive + minutes/hours

Glacier Deep Archive = Long-term archive + hours

Lifecycle Policy = Automated transitions/expiration

Versioning = Preserve object versions

Delete Marker = Normal delete behavior for versioned objects

SSE-S3 = S3-managed encryption keys

SSE-KMS = Greater key control/auditing through KMS

SSE-C = Customer provides encryption key

Block Public Access = Guardrail against public exposure

Bucket Policy = Resource-based S3 permissions

IAM Policy = Identity-based permissions

CRR = Replication across Regions

SRR = Replication within same Region

Pre-Signed URL = Temporary private-object access

OAC = CloudFront authorized access to private S3
```
