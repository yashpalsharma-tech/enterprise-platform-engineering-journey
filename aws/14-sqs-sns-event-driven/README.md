# Amazon SQS, SNS and Event-Driven Architecture

This module covers:

- Amazon SQS
- Producers and Consumers
- Message Queues
- Decoupling
- Buffering
- Visibility Timeout
- Message Retention
- Long Polling
- Dead-Letter Queues
- Standard vs FIFO Queues
- Idempotency
- CloudWatch + SQS Auto Scaling
- Amazon SNS
- SNS Fan-Out
- SNS + SQS Architecture

---

# 1. What is Amazon SQS?

Amazon SQS (Simple Queue Service) is a fully managed message queue service.

Its main purpose is to:

- Decouple application components
- Buffer workloads
- Process messages asynchronously
- Improve resilience
- Handle traffic spikes

Basic architecture:

```text
Producer
   ↓
SQS Queue
   ↓
Consumer
```

Example:

```text
Web Application
      ↓
   SQS Queue
      ↓
Order Processing Workers
```

If the backend workers are temporarily unavailable, messages can remain in the queue until consumers are available again.

Think:

```text
SQS
 ↓
Queue + Buffer + Decoupling
```

---

# 2. Producer and Consumer

## Producer

A producer sends messages to an SQS queue.

Example:

```text
Order Application
      ↓
 Sends Message
      ↓
   SQS Queue
```

## Consumer

A consumer receives and processes messages from the queue.

Example:

```text
SQS Queue
    ↓
EC2 Worker
    ↓
Process Order
```

---

# 3. Why Use SQS?

Suppose the application normally receives:

```text
100 orders/minute
```

but suddenly receives:

```text
10,000 orders/minute
```

Without a queue, backend services may become overloaded.

With SQS:

```text
10,000 Orders
      ↓
   SQS Queue
      ↓
Workers process at
their own rate
```

Benefits:

- Decoupling
- Workload buffering
- Asynchronous processing
- Improved fault tolerance
- Better scaling

---

# 4. Consumer Failure

If a consumer crashes, messages still waiting in the queue remain available until another consumer processes them or the retention period expires.

Example:

```text
SQS Queue
    ↓
Worker-A ❌
    ↓
Messages remain
    ↓
Worker-B
    ↓
Processes messages
```

This is one of the key benefits of decoupling.

---

# 5. Visibility Timeout

When a consumer receives a message, the message is temporarily hidden from other consumers.

This period is called the Visibility Timeout.

```text
SQS Queue
    ↓
Worker-A receives Message-123
    ↓
Message becomes invisible
    ↓
Visibility Timeout
    ↓
Worker-A processes message
    ↓
Worker-A deletes message
```

Important:

```text
Receive ≠ Delete
```

A consumer should delete the message after successful processing.

---

# 6. What Happens if Processing Fails?

Example:

```text
Worker-A receives Message-123
        ↓
Message becomes invisible
        ↓
Worker-A crashes
        ↓
Message is not deleted
        ↓
Visibility Timeout expires
        ↓
Message becomes visible again
        ↓
Worker-B can receive it
```

---

# 7. Visibility Timeout Configuration

The visibility timeout should normally be long enough for the consumer to complete expected processing.

Example:

```text
Processing Time = 4 minutes
Visibility Timeout = 1 minute
```

Problem:

```text
Worker-A is still processing
        ↓
Visibility timeout expires
        ↓
Message becomes visible again
        ↓
Worker-B may also receive it
```

This can lead to duplicate processing.

---

# 8. Idempotency

Consumers should be designed to handle the possibility of duplicate message processing.

Idempotent means:

```text
Processing the same message more than once
should not create an incorrect extra effect.
```

Example:

```text
Order 123
Charge $100
```

If the same message is received again:

```text
Do NOT charge another $100
```

A unique transaction or order ID can help the application determine whether a message has already been processed.

---

# 9. Message Retention Period

The Message Retention Period controls how long SQS keeps a message if it has not been deleted.

SQS supports a configurable retention period.

Typical exam point:

```text
How long does SQS keep an unprocessed message?
        ↓
Message Retention Period
```

---

# 10. Long Polling

Long Polling allows a consumer request to wait for a message instead of immediately returning an empty response.

Without Long Polling:

```text
Consumer → SQS: Message?
SQS → Empty

Consumer → SQS: Message?
SQS → Empty
```

With Long Polling:

```text
Consumer → SQS
             ↓
       Wait for message
             ↓
        Message arrives
             ↓
Consumer receives message
```

Benefits:

- Fewer empty responses
- Fewer unnecessary API calls
- Better efficiency
- Potential cost reduction

---

# 11. Dead-Letter Queue

A Dead-Letter Queue (DLQ) stores messages that repeatedly fail processing.

Example:

```text
Main SQS Queue
      ↓
Processing fails
      ↓
Retry
      ↓
Fails repeatedly
      ↓
Dead-Letter Queue
      ↓
Investigation
```

A DLQ helps isolate problematic messages.

---

# 12. Redrive Policy and maxReceiveCount

The source queue can have a redrive policy.

Example:

```text
maxReceiveCount = 5
```

Flow:

```text
Attempt 1 → Fail
Attempt 2 → Fail
Attempt 3 → Fail
Attempt 4 → Fail
Attempt 5 → Fail
        ↓
       DLQ
```

The DLQ does not fix the message automatically. It isolates the message for investigation or later redrive/reprocessing.

---

# 13. SQS Standard Queue

SQS Standard Queue is designed for very high throughput and general-purpose asynchronous workloads.

Characteristics:

- At-least-once delivery
- Best-effort ordering
- Duplicate delivery is possible
- Very high scalability

Exam clue:

```text
Ordering is not critical
        ↓
SQS Standard
```

Consumers should be idempotent.

---

# 14. SQS FIFO Queue

FIFO = First-In-First-Out.

FIFO Queues are used when ordering and deduplication are important.

Characteristics:

- Ordered processing within a message group
- Deduplication capabilities
- Useful for transactions and workflows requiring strict sequence

Exam clue:

```text
Strict ordering required
        ↓
SQS FIFO
```

---

# 15. MessageGroupId

FIFO ordering is maintained within a Message Group.

Example:

```text
Account-A:
A1 → A2 → A3

Account-B:
B1 → B2 → B3
```

Use:

```text
MessageGroupId = Account-A
MessageGroupId = Account-B
```

Ordering is preserved within each group while different groups can progress independently.

---

# 16. Standard vs FIFO

| Feature | Standard | FIFO |
|---|---|---|
| Ordering | Best-effort | Strict within message group |
| Delivery | At-least-once | Deduplication features |
| Duplicate delivery | Possible | Designed to prevent duplicates |
| Throughput | Very high | High, FIFO-specific |
| Typical use | General workloads | Ordered transactions |

---

# 17. SQS + Auto Scaling

SQS backlog can be used as an Auto Scaling signal.

Architecture:

```text
Application
     ↓
SQS Queue
     ↓
CloudWatch Metric
     ↓
Auto Scaling
     ↓
EC2 Worker ASG
```

Example:

```text
Queue backlog increases
       ↓
CloudWatch metric increases
       ↓
Scale Out
       ↓
More Workers
```

When backlog falls:

```text
Queue backlog decreases
       ↓
Scale In
```

An important metric is:

```text
ApproximateNumberOfMessagesVisible
```

This represents the approximate number of messages currently available for retrieval.

---

# 18. Amazon SNS

Amazon SNS (Simple Notification Service) is a publish/subscribe messaging service.

One message can be delivered to multiple subscribers.

Basic architecture:

```text
Publisher
   ↓
SNS Topic
   ↓
Subscribers
```

Subscribers can include:

- SQS
- Lambda
- Email
- SMS
- HTTP/S endpoints

---

# 19. SNS Publish/Subscribe Pattern

Example:

```text
OrderCreated
     ↓
SNS Topic
   ┌──┼─────────┐
   ↓  ↓         ↓
Email Analytics Inventory
```

Think:

```text
SNS
 ↓
One message → Multiple subscribers
```

---

# 20. SNS vs SQS

## SQS

```text
Producer
   ↓
Queue
   ↓
Consumer
```

Use for:

- Buffering
- Decoupling
- Asynchronous processing
- Work queues

## SNS

```text
Publisher
   ↓
SNS Topic
   ↓
Multiple Subscribers
```

Use for:

- Fan-out
- Publish/subscribe
- Notifications
- Broadcasting events

---

# 21. SNS + SQS Fan-Out

SNS and SQS can be combined when multiple independent services must each receive their own copy of an event.

Example:

```text
                OrderCreated
                     ↓
                  SNS Topic
          ┌──────────┼──────────┐
          ↓          ↓          ↓
      SQS-Pay    SQS-Inv    SQS-Analytics
          ↓          ↓          ↓
      Payment     Inventory    Analytics
```

Benefits:

- Every service gets its own copy
- Each service processes independently
- Messages are buffered in separate queues
- One service failure does not stop the others
- Each queue can have its own DLQ
- Each consumer can scale independently

---

# 22. Why Not One Shared SQS Queue?

Suppose:

```text
One SQS Queue
      ↓
Payment
Inventory
Analytics
```

These consumers would compete for messages.

That is not appropriate if every service must receive every event.

Correct design:

```text
SNS Topic
   ↓
Separate SQS queue per consumer
```

---

# 23. SNS + SQS + DLQ Architecture

```text
                   Order Application
                         ↓
                      SNS Topic
              ┌──────────┼──────────┐
              ↓          ↓          ↓
           SQS-Pay    SQS-Inv   SQS-Analytics
              ↓          ↓          ↓
           Payment    Inventory   Analytics
              │          │          │
             DLQ        DLQ        DLQ
```

This architecture provides:

- Fan-out
- Decoupling
- Buffering
- Independent processing
- Failure isolation

---

# 24. SQS Timer Comparison

| Setting | Purpose |
|---|---|
| Visibility Timeout | How long a received message is hidden |
| Message Retention Period | How long SQS keeps a message |
| Long Polling | How long receive request waits |
| maxReceiveCount | Number of receives before DLQ |

---

# 25. Problem-to-Solution Mapping

| Requirement | AWS Solution |
|---|---|
| Decouple components | SQS |
| Buffer burst traffic | SQS |
| Async processing | SQS |
| Keep message while consumer is down | SQS |
| Temporarily hide received message | Visibility Timeout |
| Retain unprocessed message | Message Retention |
| Reduce empty receives | Long Polling |
| Isolate failed messages | DLQ |
| Control retries before DLQ | maxReceiveCount |
| Very high throughput/general queue | Standard Queue |
| Strict ordering | FIFO Queue |
| Prevent duplicate effects | Idempotent Consumer |
| Scale workers based on backlog | SQS Metric + Auto Scaling |
| One message to many subscribers | SNS |
| Reliable fan-out to independent services | SNS + separate SQS queues |

---

# 26. Exam Quick Notes

```text
SQS
→ Queue
→ Buffer
→ Decouple
→ Async Processing

Producer
→ Sends Message

Consumer
→ Receives / Processes / Deletes

Visibility Timeout
→ Hide received message temporarily

Message Retention
→ How long SQS stores message

Long Polling
→ Reduce empty receives

DLQ
→ Failed messages

maxReceiveCount
→ Receives before DLQ

Standard Queue
→ At-least-once
→ Best-effort ordering

FIFO Queue
→ Ordered within MessageGroupId
→ Deduplication features

Idempotent Consumer
→ Safe duplicate processing

SNS
→ Pub/Sub
→ Fan-Out

SNS + SQS
→ One event
→ Multiple reliable independent consumers
```entation
