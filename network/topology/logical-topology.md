# Logical Topology

The CloudGuard AI network architecture is built upon the industry-standard **Three-Tier Hierarchical Model**. This logical design ensures high availability, strict fault isolation, and scalable performance across both our Headquarters (HQ) and Branch office.

<figure><img src="../../.gitbook/assets/logical topology.png" alt=""><figcaption></figcaption></figure>

### Perimeter and Security Zones

At the top of the logical topology, traffic is strictly managed before it ever reaches our internal corporate network:

* **Internet Edge & Firewall:** All inbound and outbound traffic passes through a unified Threat Prevention Firewall equipped with Intrusion Prevention System (IPS) and VPN capabilities. This secures the Site-to-Site tunnel to our AWS Cloud environment.
* **Demilitarized Zone (DMZ):** Public-facing or externally communicating services are isolated in their own switch block. This includes our Web Server, Mail Server, and Proxy Server.
* **Data Center Block:** Our most critical assets are segregated into a dedicated Data Center block. This zone houses the core **SOC Server** (for ML inference and log normalization), the central **Database** (PostgreSQL/Elasticsearch), the **DHCP Server**, and the **WLAN Controller** managing all campus access points.

### The Three-Tier Architecture

#### 1. Core Layer (Layer 3)

The backbone of the network consists of two fully redundant Layer 3 Core Switches.

* **Function:** Designed for pure, unhindered speed and rapid packet switching. It interconnects the DMZ, Data Center, and lower distribution layers without applying complex routing policies that could slow traffic.
* **Redundancy:** The cross-linked mesh design ensures that if one core switch fails, the entire network remains operational.

#### 2. Distribution Layer (Layer 3)

This layer serves as the boundary between the Core and Access layers, enforcing network policies and routing traffic between VLANs.

* **HQ Block:** Two redundant distribution switches aggregate all traffic from the HQ departments.
* **Branch Block:** Two redundant distribution switches aggregate traffic for the remote branch office.
* **Function:** This layer handles packet filtering, Inter-VLAN routing, and limits broadcast domains, ensuring that a broadcast storm in the HR department does not impact the SOC Data Center.

#### 3. Access Layer (Layer 2)

The Access Layer is where end-user devices (PCs, laptops, Access Points) connect to the network.

* **VLAN Segmentation:** To ensure security and manage traffic flow, access switches are logically divided by department.
  * **HQ Access:** Dedicated switches/VLANs for Executive (Exe), Finance, Marketing, Human Resources (HR), and IT/SOC.
  * **Branch Access:** Dedicated switches/VLANs for Marketing and IT.
* **Function:** Operates entirely at Layer 2, providing port security, PoE (Power over Ethernet) for the wireless Access Points, and initial QoS (Quality of Service) tagging.
