# Hybrid Architecture Overview

CloudGuard AI is designed as a **hybrid cybersecurity log analysis platform** with three main operational zones: the **Edge Agent** at customer sites, the **AWS public cloud** as an internet-facing buffer and application layer, and the **HQ private data center** as the core environment for search, analytics, storage, and machine learning operations. This design avoids streaming all raw logs directly over VPN in real time. Instead, data is reduced at the edge, buffered in the cloud, and transferred to HQ in a controlled manner for deeper processing.

## System Tiers

At a high level, the system is organized as follows:

- **Tier 1: Edge Agent**
  - Runs on employee devices or customer sites.
  - Performs local filtering, tagging, and anomaly scoring.
  - Reduces bandwidth usage before any data leaves the endpoint.

- **Tier 2: Public Cloud (AWS)**
  - Hosts the web application entry path and public-facing APIs.
  - Acts as the ingestion buffer for incoming logs and metadata.
  - Supports batching, compression, rate-limiting, and temporary storage.

- **Tier 3: HQ Private Data Center**
  - Performs log normalization, searchable indexing, case management, ML inference, model training, and long-term operational control.
  - Stores hot investigation data locally for fast access.

This separation gives the system a practical balance between **internet accessibility**, **bandwidth control**, and **security-sensitive processing at HQ**.

## Hybrid Architecture Workflow

The end-to-end workflow of CloudGuard AI can be described in the following sequence:

1. **Event generation at the edge**
   A user device or monitored endpoint generates security logs such as process execution, access attempts, or suspicious activity.

2. **Local reduction by the CloudGuard Agent**
   The edge agent filters unnecessary events, tags useful attributes, and computes lightweight anomaly scores. This step reduces bandwidth usage and allows obvious attacks to be flagged immediately.

3. **Cloud buffering and staging**
   Selected logs or summarized data are sent to AWS, where Kinesis Firehose and S3 provide managed ingestion and buffering. Cloud-side forwarders can batch, compress, and rate-limit the transfer stream.

4. **Controlled transfer through secure tunnel**
   AWS Site-to-Site VPN connects the public cloud and HQ data center. The VPN is used for **secure, scheduled, and selective transfer**, not for unlimited real-time raw log streaming.

5. **HQ ingestion and normalization**
   At HQ, incoming data is parsed and normalized into a form suitable for search, alerting, and model inference.

6. **Operational storage and analytics**
   - **Elasticsearch** stores hot searchable security logs.
   - **PostgreSQL** stores alerts, investigations, and case records.
   - **FastAPI + PyTorch** provides centralized inference services.

7. **Investigation and feedback loop**
   Alerts are reviewed by SOC operators. Their outcomes, labels, and case decisions become feedback for future retraining and model improvement.
