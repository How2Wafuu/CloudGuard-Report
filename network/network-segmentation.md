# Network Segmentation

### Headquarters (HQ) Segmentation

The HQ network requires heavy segmentation to isolate the sensitive Data Center and SOC operations from standard departments and public-facing services.

| VLAN ID | VLAN Name   | Users | Devices                    | Type           | Description                               |
| ------- | ----------- | ----- | -------------------------- | -------------- | ----------------------------------------- |
| **7**   | Data Center | 1     | Servers, Database, AAA     | LAN            | Application Servers & HCI Cluster         |
| **10**  | DMZ         | 1     | Proxy, Web Mail            | LAN            | Public-facing services                    |
| **20**  | Executive   | 3     | PC / Laptops               | Wireless       | High Priority / Unrestricted Access       |
| **30**  | Finance     | 10    | PC / Laptops               | Wireless       | High Security / Restricted Internet       |
| **40**  | Marketing   | 15    | PC / Laptops               | Wireless       | Standard Access                           |
| **50**  | HR          | 10    | PC / Laptops               | Wireless       | Standard Access                           |
| **60**  | IT          | 25    | PC / Laptops               | Wireless / LAN | PC Direct link for monitoring and testing |
| **70**  | SoC         | 50    | PC / Laptops               | Wireless / LAN | Restricted network for Security Analysts  |
| **80**  | IoT         | N/A   | CCTV, Door Access, Sensors | LAN            | Physical Security Devices                 |
| **99**  | Management  | N/A   | Switches, APs, Firewall    | LAN            | Network Infrastructure                    |
| **100** | Guest       | 50    | Personal Devices           | Wireless       | Personal Laptops, Phones                  |

***

### Branch Office Segmentation

The Branch office uses a mirrored VLAN ID structure for consistency across the organization, scaled down to meet regional operational needs.

| VLAN ID | VLAN Name  | Users | Devices                | Type           | Description                           |
| ------- | ---------- | ----- | ---------------------- | -------------- | ------------------------------------- |
| **20**  | Executive  | 1     | PC / Laptops           | Wireless       | Office Manager (High Priority Access) |
| **40**  | Marketing  | 10    | PC / Laptops           | Wireless       | Marketing Team (Standard Access)      |
| **60**  | IT         | 15    | PC / Laptops           | Wireless / LAN | Branch IT Staff (Main Workforce)      |
| **80**  | IoT        | N/A   | CCTV & Keycard Readers | LAN            | Physical Equipment                    |
| **99**  | Management | N/A   | Switch, Router, APs    | LAN            | Infrastructure                        |
| **100** | Guest      | 10    | Personal Devices       | Wireless       | Personal Laptops, Phones              |

### Segmentation Strategy Highlights

* **Operational Isolation (VLAN 7 & 70):** The SOC Team (VLAN 70) and Data Center (VLAN 7) are logically separated from all standard corporate traffic. This prevents lateral movement if a standard user's device is compromised.
* **Infrastructure Security (VLAN 99):** All network management interfaces (Switches, APs, Firewalls) are placed on a dedicated management VLAN that cannot be routed to or accessed from the Guest or standard departmental VLANs.
* **IoT Segregation (VLAN 80):** Physical security devices (CCTV, card readers) are placed on a dedicated LAN-only network to prevent external interference.
