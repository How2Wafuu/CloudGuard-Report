# Private Data Center

The **HQ private data center** is the operational core of CloudGuard AI. It hosts the components that require stronger control, fast local access, and tighter integration with SOC workflows.

## Networking and Edge Security

The private data center includes:

- **Cisco Nexus switches**
- **Palo Alto firewalls**
- **IDS/IPS**

These components provide high-speed internal connectivity, perimeter enforcement, and deeper inspection for sensitive operational traffic. They are appropriate for a centralized SOC and analytics environment where security controls must remain under local administrative control.

## Compute Layer

The compute layer includes:

- **GPU server(s)** for ML training
- **Dell PowerEdge servers** for backend, SOC, and application workloads

This separation allows training-intensive jobs to run on specialized hardware while keeping operational services on general-purpose enterprise servers.

## Data and Storage Layer

The storage design includes:

- **Elasticsearch on NVMe/SSD tiers** for hot search performance
- **Cold storage** for long-term retention
- **MinIO object storage** for model artifacts

The use of fast storage for hot investigative data is important because security analysts need low-latency search over recent events. Older data can move to colder tiers without slowing down the active SOC workflow.

## Operations and Physical Infrastructure

Operational and physical support components include:

- **Backup server (Veeam)**
- **Monitoring server**
- **Remote interface console**
- **Patch panels**
- **Blanking panels**
- **APC metered PDU**

These components show that the design considers not only logical services, but also maintainability, power management, remote administration, and rack-level physical discipline.

## Why the Private Data Center Is Useful

Using a private HQ data center is justified by four main reasons:

- **Local control**
  Sensitive security data and operational workflows remain under direct organizational control.

- **High-performance search and training**
  Recent logs, Elasticsearch indexes, and model training jobs benefit from local high-speed compute and storage.

- **Security isolation**
  Core analytics and SOC systems are separated from public-facing services.

- **Long-term operational ownership**
  The organization retains control over its main detection, investigation, and model operations platform.

## Identity and Access Management

Identity and access control follows a simple least-privilege model across both cloud and private infrastructure.

- On the **AWS side**, services use **least-privilege IAM roles**.
- Administrative and staff access should use **MFA** and **Single Sign-On**.
- Access into the **private data center** is restricted through **VPN access for employees and administrators only**.

This design reduces unnecessary credential exposure and helps separate public service access from internal administrative access.
