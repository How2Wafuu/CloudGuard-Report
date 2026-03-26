# Physical Topology

## Physical Topology

The physical topology of CloudGuard AI outlines the hardware distribution and cabling infrastructure across our operational sites. This design ensures high availability, secure data segmentation, and optimal performance for our specialized SOC workloads.

### 1. Branch Office (Physical Distribution)

Our 20m x 17m Branch Office utilizes a straightforward but robust network design to support regional operations.

<figure><img src="../../.gitbook/assets/branch Physical.png" alt=""><figcaption></figcaption></figure>

#### Infrastructure Details:

* **Core Distribution:** The network is anchored by two **Distribute Switches** located in the secured Server Room.
* **Access Layer:** Two **Access Switches** provide wired connectivity to the workstations in the IT and Marketing departments.
* **Cabling:** \* The backbone connection between the Distribute and Access switches utilizes **OM4 Multi-Mode Fiber** for high throughput.
  * Endpoint connections (workstations to switches) utilize standard **CAT7** copper cabling.
* **Wireless:** A single **Access Point (AP)** ensures wireless coverage for the meeting rooms and general office areas.

***

### 2. HQ 1st Floor (Physical Distribution)

The 35m x 20m first floor of HQ handles general corporate traffic and requires broad wireless coverage.

<figure><img src="../../.gitbook/assets/HQ 1st floor Physical.png" alt=""><figcaption></figcaption></figure>

#### Infrastructure Details:

* **Wired Access:** The floor utilizes **OM4 Multi-Mode Fiber** to link back to the core network (located on the 2nd floor), distributing to three **Access Switches** strategically placed to serve the Security Control, HR, Marketing, and Finance departments.
* **Wireless Coverage:** To support a mobile corporate workforce, six **Access Points (APs)** are distributed across the floor, providing overlapping coverage for the Reception, Pantry, Guest Meeting room, and general open areas.

***

### 3. HQ 2nd Floor (The Core Network)

The 2nd floor houses the "brain" of CloudGuard AI. The physical topology here is highly dense, prioritizing redundancy and focusing on extreme throughput for the AI training clusters and SOC analysts.

<figure><img src="../../.gitbook/assets/HQ 2nd floor Physical.png" alt=""><figcaption></figcaption></figure>

#### Infrastructure Details:

* **The Server Room Core:** \* The network boundary is protected by a dedicated **Firewall**.
  * The core routing and switching are handled by redundant **Core Switches (x2)** and **Distribute Switches (x2)**.
  * **Datacenter Switches** manage the massive data flows required by the NVIDIA DGX clusters and storage arrays.
* **High-Speed Cabling:** The connections within the Server Room and to the primary operational zones use OS2 Single-Mode Fiber to maximize bandwidth and minimize latency.
* **Operational Access:** The SOC Team relies on a dedicated **Access Switch** connected via fiber to the core, ensuring analyst workstations have uninterrupted, high-speed access to the security logs and AI dashboards. **CAT7** cabling connects the individual SOC workstations to this switch.
