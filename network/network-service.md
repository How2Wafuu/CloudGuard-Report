# Network Service

To support our hybrid cloud architecture and distributed workforce, CloudGuard AI relies on premium external ISPs and managed network services. Our connectivity strategy is built on redundancy, high availability, and secure remote access.

### External Connectivity & Redundancy

#### 1. Primary Corporate Internet

* **Provider:** AIS Business Network.
* **Features:** Provides enterprise-grade, high-speed connectivity with guaranteed SLA and 24/7 engineering support. This line handles the heavy traffic steering to our AWS Cloud services and S3 ingestion buffers.

#### 2. Backup Internet (Failover)

* **Provider:** NT Corporate Internet.
* **Features:** Ensures physical path diversity by using a completely separate infrastructure from AIS. It connects to 6 international submarine cable routes, guaranteeing that the HQ SOC remains online even if a major local ISP experiences a national outage.

### Branch and Remote Operations

#### 3. Branch Connectivity

* **Provider:** AIS SD-WAN.
* **Features:** An end-to-end managed service that utilizes Active-Active multi-path networking. Intelligent traffic steering dynamically routes our Branch data over MPLS, Broadband, or Mobile networks, depending on which path offers the best performance at that exact moment.

#### 4. Work-From-Home (Remote Access)

* **Provider:** Palo Alto GlobalProtect (Prisma SASE).
* **Features:** Provides secure SSL/IPsec VPN access to the HQ private data center for up to 100 concurrent remote users (SOC Analysts and Engineers). It enforces consistent security policies across all traffic while using split tunneling to optimize bandwidth.
