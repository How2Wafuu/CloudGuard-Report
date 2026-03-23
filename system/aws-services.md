# AWS Services

## AWS Amplify

AWS Amplify hosts the CloudGuard AI web application frontend. In this project, it is responsible for delivering the dashboard interface while keeping frontend hosting separate from backend services.

## CloudFront

CloudFront acts as the CDN and TLS entry point. It improves frontend delivery performance and provides a controlled edge entry before requests reach application components.

## AWS WAF

AWS WAF protects the web-facing application by filtering malicious or unwanted HTTP requests. It is used to reduce exposure to common web attacks before traffic reaches the application layer.

## AWS Shield

AWS Shield provides protection against denial-of-service style attacks at the cloud edge. In this architecture, it complements WAF by strengthening the resilience of public-facing endpoints.

## API Gateway

API Gateway is the managed entry point for application APIs. It provides structured access to backend services and helps separate public API access from the internal implementation of those services.

## ALB (Application Load Balancer)

The Application Load Balancer distributes requests to backend services, including containerized application components. It supports service availability and simplifies horizontal scaling.

## Amazon ECS

Amazon ECS runs the project's containerized services, including application services and cloud-side forwarders. It is the main compute platform for scalable cloud workloads in this design.

## Amazon Kinesis Firehose

Amazon Kinesis Firehose is used for managed log ingest and streaming into the cloud buffer layer. It helps absorb incoming telemetry and move it toward storage or downstream processing with low operational overhead.

## Amazon S3

Amazon S3 serves two roles:

- **Raw log buffer** in the ingestion path
- **Long-term cloud storage** for warm/cold retention

Its object storage model makes it suitable for buffered telemetry, archival data, and cloud-side retention.

## CloudWatch

CloudWatch collects metrics and logs from AWS components. It supports operational monitoring for the forwarder layer, container services, and other cloud resources.

## AWS Site-to-Site VPN

AWS Site-to-Site VPN provides the secure tunnel between AWS and the HQ private data center. In CloudGuard AI, it is used for controlled transfer between cloud buffer services and on-premise core systems rather than for unrestricted real-time raw log streaming.
