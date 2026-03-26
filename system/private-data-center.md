# Private Data Center

The **HQ private data center** is the operational core of CloudGuard AI. It hosts the components that require stronger control, fast local access, and tighter integration with SOC workflows.

<figure><img src="../.gitbook/assets/Private Data Center.png" alt=""><figcaption></figcaption></figure>

### Networking and Edge Security

The private data center includes:

* Cisco Nexus switches
* Palo Alto firewalls
* IDS/IPS

These components provide high-speed internal connectivity, perimeter enforcement, and deeper inspection for sensitive operational traffic. They are appropriate for a centralized SOC and analytics environment where security controls must remain under local administrative control.

### Compute Layer

The compute layer includes:

* GPU server(s) for ML training
* Dell PowerEdge servers for backend, SOC, and application workloads

This separation allows training-intensive jobs to run on specialized hardware while keeping operational services on general-purpose enterprise servers.

### Data and Storage Layer

The storage design includes:

* Elasticsearch on NVMe/SSD tiers for hot search performance
* Cold storage for long-term retention
* MinIO object storage for model artifacts

The use of fast storage for hot investigative data is important because security analysts need low-latency search over recent events. Older data can move to colder tiers without slowing down the active SOC workflow.

### Operations and Physical Infrastructure

Maintaining 100% uptime and data integrity is critical for a Security Operations Center (SOC). The physical support components consider not only logical services, but also maintainability, power management, remote administration, and rack-level physical discipline:

#### 1. Backup and Disaster Recovery

* **System:** Veeam Backup Server.
* **Strategy:** All critical configurations, Active Directory states, and PostgreSQL Case Databases are backed up locally and mirrored to AWS S3 Cold Storage to ensure recovery in the event of catastrophic hardware failure or ransomware targeting the SOC itself.

#### 2. Infrastructure Monitoring

* **System:** Dedicated Monitoring Server.
* **Strategy:** Continuously tracks the health, CPU/GPU utilization, and internal bandwidth of the NVIDIA DGX training clusters and Dell PowerEdge core nodes. This ties directly into our MLOps pipeline to alert engineers if model training degrades system performance.

#### 3. Remote Administration

* **System:** Remote Interface Console.
* **Strategy:** Provides Out-of-Band (OOB) management. If the primary network goes down, system administrators can still access the core switches and servers at the BIOS level to perform emergency diagnostics and reboots.

#### 4. Power & Environmental Management

* **System:** APC Metered Power Distribution Units (PDUs) and Blanking Panels.
* **Strategy:** Blanking panels maintain strict hot-aisle/cold-aisle airflow to prevent thermal throttling of the GPUs. The metered PDUs allow the IT team to monitor power draw per rack in real-time, ensuring we do not trip breakers during heavy ML training cycles.

#### 5. Server Room Power & Cooling Budget (HQ 2nd Floor)

Hosting centralized AI training models requires strict thermodynamic management. Given the physical deployment of our NVIDIA DGX H100 architecture, the Server Room is provisioned to support extreme density.

* **Cluster Sizing:** A single standard rack housing 4x NVIDIA DGX H100 nodes.
* **Power Draw:** \~40.8 kW peak draw per rack (10.2 kW per node).
* **Redundancy:** N+1 power redundancy utilizing 3 separate circuits per rack.
* **Thermal Output:** \~154,000 BTU/hr per rack.
* **Cooling Strategy:** The 35m x 20m floor plan provides ample space for strict hot-aisle/cold-aisle containment, utilizing blanking panels and precision Computer Room Air Conditioning (CRAC) units to maintain the required 5–30°C operating environment.

### Why the Private Data Center Is Useful

Using a private HQ data center is justified by four main reasons:

* **Local control:** Sensitive security data and operational workflows remain under direct organizational control.
* **High-performance search and training:** Recent logs, Elasticsearch indexes, and model training jobs benefit from local high-speed compute and storage.
* **Security isolation:** Core analytics and SOC systems are separated from public-facing services.
* **Long-term operational ownership:** The organization retains control over its main detection, investigation, and model operations platform.

### Identity and Access Management

Identity and access control follow a simple least-privilege model across both cloud and private infrastructure.

* On the **AWS side**, services use least-privilege IAM roles.
* Administrative and staff access should use **MFA** and **Single Sign-On**.
* Access to the **private data center** is restricted through VPN access for employees and administrators only.

This design reduces unnecessary credential exposure and helps separate public service access from internal administrative access.
