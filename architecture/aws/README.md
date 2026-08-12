**Architecture Diagram**
```mermaid

Users Worldwide 
        │
        ▼
 CloudFront
        │
        ▼
Application Load Balancer
        │
 ┌──────┴──────┐
 ▼             ▼
EC2 (AZ-A)   EC2 (AZ-B)
        │
        ▼
RDS Multi-AZ

```
