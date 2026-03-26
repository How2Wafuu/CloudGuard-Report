# Operations and Maintenance

Maintaining 100% uptime and data integrity is critical for a Security Operations Center (SOC). The CloudGuard AI Private Data Center is equipped with dedicated hardware and software specifically designed for resilient operations and remote management.

### Core Operational Infrastructure

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

### Server Room Power & Cooling Budget (HQ 2nd Floor)

Hosting centralized AI training models requires strict thermodynamic management. Given the physical deployment of our NVIDIA DGX H100 architecture, the Server Room is provisioned to support extreme density.

* **Cluster Sizing:** A single standard rack housing 4x NVIDIA DGX H100 nodes.
* **Power Draw:** \~40.8 kW peak draw per rack (10.2 kW per node).
* **Redundancy:** N+1 power redundancy utilizing 3 separate circuits per rack.
* **Thermal Output:** \~154,000 BTU/hr per rack.
* **Cooling Strategy:** The 35m x 20m floor plan provides ample space for strict hot-aisle/cold-aisle containment, utilizing blanking panels and precision Computer Room Air Conditioning (CRAC) units to maintain the required 5–30°C operating environment.
