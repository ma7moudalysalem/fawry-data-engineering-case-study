# Fawry Data Engineering: a Lambda Architecture for Payments

A data-engineering case study for **Fawry**, Egypt's payments network: how to process a very large daily volume of point-of-sale transactions so that payments stay **fast**, **secure** and **accurately recorded**.

📄 The full design is in **[Fawry Data Engineering Presentation.pdf](./Fawry%20Data%20Engineering%20Presentation.pdf)**.

## The problem

| Challenge | Requirement |
|---|---|
| **Real-time fraud detection** | Detect and block a suspicious transaction in **under 500 ms**, before it is finalised |
| **Financial reconciliation** | **Zero data loss**; every transaction matches across systems by the end of the day |
| **Scalability** | Absorb traffic spikes, such as salary payout days, without slowing down |

## The design

A **Lambda architecture**: a speed layer gives an answer in time to stop fraud, and a batch layer recomputes everything from the raw log so that the books are exact.

```
POS terminals ──► Kafka (ingestion buffer) ──┬──► Flink (speed layer)  ──► fraud decision < 500 ms
                                             │
                                             └──► Data lake (raw log) ──► Spark (batch layer) ──► end-of-day reconciliation
```

| Component | Technology | Role |
|---|---|---|
| Ingestion | Apache Kafka | A durable buffer that absorbs bursts of POS traffic |
| Speed layer | Apache Flink | Stream processing that scores each transaction for fraud |
| Batch layer | Apache Spark | Recomputes over the full history and produces end-of-day financial reports |
| Storage | Data lake (S3) | Immutable store of every raw transaction log |

## Why Lambda here

Fraud detection needs an answer in milliseconds, while reconciliation needs an exact answer over everything. One pipeline cannot give both: the stream is fast but approximate under failures, and the batch is exact but slow. Keeping the raw log as the source of truth lets the batch layer correct anything the speed layer got wrong.

---

By [Mahmoud Salem](https://github.com/ma7moudalysalem) · Data Engineering Project course.
