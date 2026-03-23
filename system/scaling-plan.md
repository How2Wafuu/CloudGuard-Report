# Scaling Plan

The scaling approach for CloudGuard AI is different for each subsystem because not all components grow in the same way.

## Application and API Services

- Web and API containers can **scale out horizontally** through autoscaling.
- Stateless service design makes replication easier for both tenant APIs and inference APIs.

## Database Layer

- The main relational database can begin with **vertical scaling**.
- If read workload increases, **read replicas** can be introduced later.

## Search and Object Storage

- **Elasticsearch** capacity can be expanded by increasing nodes and storage tiers over time.
- **MinIO/object storage** scales by adding nodes for both capacity and throughput.

## Training Infrastructure

- ML training capacity scales by **adding GPU servers**.
- This avoids overloading operational backend nodes with heavy training workloads.

This plan is suitable for a capstone-scale design because it starts with a manageable baseline while keeping a clear path toward larger workloads.
