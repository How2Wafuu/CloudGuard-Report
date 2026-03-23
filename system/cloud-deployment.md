# Cloud Deployment

The AWS environment in CloudGuard AI is not the final destination for all security data. Its main purpose is to provide a **scalable public-facing service layer** and an **ingestion buffer** between distributed customer environments and the HQ private data center.

## Edge and Protection Layer

User-facing traffic first reaches the cloud edge, where AWS services provide delivery, security, and controlled entry:

- **CloudFront** serves as the CDN and TLS entry point.
- **AWS WAF** applies web-layer filtering rules.
- **AWS Shield** provides protection against volumetric and network-layer attacks.
- **AWS Amplify** hosts the web dashboard frontend.

This layer ensures that the dashboard and public application components are exposed through managed, protected services rather than directly exposing backend systems.

## Application Layer

The application layer supports API delivery and service routing:

- **API Gateway** provides a managed API entry point.
- **ALB** distributes requests to backend services.
- **Amazon ECS** runs containerized application and forwarder services.
- **CloudWatch** collects operational logs and metrics from cloud services.

This arrangement keeps the application tier modular and easier to scale, while allowing backend services to remain containerized and replaceable.

## Ingestion Buffer Layer

For telemetry and security events, AWS acts as a **buffering and staging environment**:

- **Amazon Kinesis Firehose** receives managed log ingest streams.
- **Amazon S3** stores buffered raw logs and long-term cloud copies.
- **ECS forwarder services** batch, compress, rate-limit, and selectively forward relevant content toward HQ.

This is an important architectural decision. Rather than pushing all raw logs over VPN continuously, the system uses AWS to absorb bursts, store temporary raw data, and forward only the most relevant anomalies, features, or scheduled data batches to HQ.
