# S3 Cheat Sheet

## Definition

## Key Components

## Important Interview Points

## AWS Exam Tips

## Best Practices

## Common Mistakes

## One-Line Revision


# Amazon S3 Quick Reference

## Core Concepts

```text
S3
 ↓
Bucket
 ↓
Objects
```

S3 = Object Storage

Bucket = Container

Object = Stored data/file

---

## Storage Classes

| Requirement | Storage Class |
|---|---|
| Frequent access | S3 Standard |
| Infrequent + immediate + Multi-AZ | Standard-IA |
| Infrequent + immediate + Single AZ | One Zone-IA |
| Unknown/changing access | Intelligent-Tiering |
| Archive + milliseconds | Glacier Instant Retrieval |
| Archive + minutes/hours | Glacier Flexible Retrieval |
| Long-term archive + hours | Glacier Deep Archive |

---

## Intelligent-Tiering vs Lifecycle

```text
Unknown / unpredictable access
            ↓
Intelligent-Tiering

Known age-based rules
            ↓
Lifecycle Policy
```

---

## Lifecycle

```text
Standard
   ↓ 30 days
Standard-IA
   ↓ 365 days
Glacier
   ↓ 7 years
Delete
```

---

## Versioning

```text
report.pdf
 ├── Version 1
 ├── Version 2
 └── Version 3
```

Normal delete:

```text
Versioning Enabled
       ↓
Delete Object
       ↓
Delete Marker
```

---

## Encryption

```text
SSE-S3  → S3-managed keys

SSE-KMS → KMS + greater key control/auditing

SSE-C   → Customer-provided key
```

At rest → stored data encryption

In transit → HTTPS/TLS

---

## S3 Security

```text
Private Bucket
     |
     +-- Block Public Access
     |
     +-- Least-Privilege IAM/Bucket Policies
     |
     +-- Encryption
     |
     +-- Versioning
```

---

## IAM vs Bucket Policy

```text
IAM Policy
    ↓
What can this identity do?

Bucket Policy
    ↓
Who can access this S3 resource?
```

---

## EC2 → S3

```text
EC2
 ↓
IAM Role
 ↓
Temporary Credentials
 ↓
Private S3
```

Do not store long-term AWS access keys on EC2.

---

## Replication

```text
Different Regions → CRR

Same Region → SRR
```

S3 replication requires Versioning on source and destination buckets.

---

## Pre-Signed URL

```text
Private Object
      +
Temporary Access
      ↓
Pre-Signed URL
```

---

## Static Website Architecture

```text
Users
 ↓
Route 53
 ↓
CloudFront
 ↓
Private S3
```

CloudFront accesses the private S3 origin using OAC.

---

## Durability vs Availability

```text
Durability
    ↓
Will my data remain intact?

Availability
    ↓
Can I access it when required?
```

S3 Standard:

```text
99.999999999%
11 nines durability
```

---

## Exam Triggers

```text
Frequently accessed
→ S3 Standard

Infrequent but immediate
→ Standard-IA

Single AZ acceptable
→ One Zone-IA

Unknown access pattern
→ Intelligent-Tiering

Known transition schedule
→ Lifecycle Policy

Accidental overwrite/delete protection
→ Versioning

Archive + milliseconds
→ Glacier Instant Retrieval

Archive + minutes/hours
→ Glacier Flexible Retrieval

Very long-term archive
→ Glacier Deep Archive

Simple AWS-managed S3 encryption
→ SSE-S3

Greater encryption-key control
→ SSE-KMS

Customer provides encryption key
→ SSE-C

Prevent public exposure
→ Block Public Access

Cross-account S3 resource access
→ Bucket Policy

EC2 needs S3 access
→ IAM Role

Different-region replication
→ CRR

Temporary private object access
→ Pre-Signed URL

CloudFront → Private S3
→ OAC
```
