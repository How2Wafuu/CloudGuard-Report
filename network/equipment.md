# Equipment & Hardware

To support the heavy data flow of the CloudGuard AI MLOps pipeline and ensure zero-downtime operations, we selected enterprise-grade Cisco, Palo Alto, and Aruba networking hardware.

### Network Devices

Our hardware footprint is designed with high availability (HA) in mind, utilizing redundant core and distribution switches across both the HQ and Branch locations.

| Device Role                      | Brand & Model                 | Quantity | Location           |
| -------------------------------- | ----------------------------- | -------- | ------------------ |
| **Firewall / Edge Security**     | Palo Alto Networks PA-3220    | 2        | HQ Core            |
| **Core Switch**                  | Cisco Catalyst 9500-48Y4C     | 2        | HQ Data Center     |
| **Distribution Switch (HQ)**     | Cisco Catalyst 9300-48P-A     | 2        | HQ Server Room     |
| **Distribution Switch (Branch)** | Cisco Catalyst C9300L-48PF-4X | 2        | Branch Server Room |
| **Access Switch**                | Cisco Catalyst 9200-48T-A     | 7        | HQ & Branch Floors |
| **Wireless Access Point (AP)**   | HPE Aruba AP-635              | 12       | Campus-Wide        |

***

### Estimated Infrastructure Cost

Below is the estimated capital expenditure (CapEx) for the network hardware components required to build out the physical topologies. _(Note: Pricing is estimated in THB based on vendor quotes)._

| Item                              | Qty | Unit Cost (THB) | Subtotal (THB) |
| --------------------------------- | --- | --------------- | -------------- |
| **Palo Alto Firewall PA-3220**    | 2   | 887,000         | 1,774,000      |
| **Cisco Catalyst 9500-48Y4C**     | 2   | 644,400         | 1,288,800      |
| **Cisco Catalyst 9300-48P-A**     | 2   | 174,000         | 348,000        |
| **Cisco Catalyst C9300L-48PF-4X** | 2   | 115,000         | 230,000        |
| **Cisco Catalyst 9200-48T-A**     | 7   | 59,600          | 417,200        |
| **HPE AP-635 Aruba**              | 12  | 45,350          | 544,200        |
| **Total Estimated Cost**          |     |                 | **3,715,200**  |

***

### Physical Layer (Cabling)

The physical transmission media are tiered based on bandwidth requirements and Distance, ensuring that the NVIDIA GPU clusters achieve maximum throughput while maintaining cost-efficiency at the access layer.

#### 1. OS2 Single-Mode Fiber

* **Purpose:** High-speed, long-distance interconnects (Core to Firewalls/Datacenter).
* **Speed & Distance:** \* 10 Gbps (10–80 km)
  * 40 Gbps (10–40 km)
  * 100 Gbps (10–40 km)
* **Redundancy:** LACP (EtherChannel) with dual physical paths.

#### 2. OM4 Multi-Mode Fiber

* **Purpose:** Backbone connections between the Core and Distribution layers within the building.
* **Speed & Distance:** \* 10 Gbps (up to 400 m)
  * 40 Gbps (up to 150 m)
  * 100 Gbps (up to 150 m)
* **Redundancy:** Dual uplinks with LACP configured for Active/Standby.

#### 3. CAT 7 (Shielded Copper)

* **Purpose:** Endpoint connections (Switches to PCs, Laptops, and Access Points).
* **SpeedDistance:** \* 1 Gbps standard user access.
  * 2.5 / 5 Gbps for Wi-Fi 6 / 6E APs.
  * Up to 10 Gbps (max 100 meters).
* **Redundancy:** Direct connect (No physical redundancy to individual workstations).
