# Client Onboarding & Response Flow

This flow tracks the journey of an SME client from their initial visit to the platform through to active threat mitigation.

#### Onboarding & Setup

* **Entry Point**: Users begin on the CloudGuard landing page, where they can create a new organization/tenant or sign in to an existing account.
* **Hybrid Setup Choice**: To accommodate different technical capabilities, we offer two paths:
  * **Managed Service**: For clients requiring "white-glove" support, a technician is booked to perform on-site activation and system validation.
  * **Self-Service**: IT-capable teams use the **Smart Agent Wizard** to download a master agent. The system then utilizes **Auto-Discovery** to identify network devices, allowing the user to select specific targets and run automated installation scripts.
* **Validation**: Once the agent connects, the system generates a profile for approval before the dashboard becomes fully active.

#### Monitoring & Mitigation

* **Real-Time Detection**: When a critical anomaly is identified, the system immediately issues push notifications and emails to the client.
* **Decision Path**:
  * **Direct Action: The client can choose to immediately isolate the Host or block the IP through the dashboard.**
  * **Expert Escalation**: Alternatively, the client can request help, which escalates the incident directly to the Tier 2 HQ analysts for professional intervention.

```mermaid
flowchart TD

%% --- ONBOARDING FLOW ---
A([Start]) --> B[Visit CloudGuard Landing Page]
B --> C{User Already Have Account?}

C -- No --> D[Create/Sign-in Account]
C -- Yes --> R

D --> E
E[Create Tenant/Organization] --> F{Choose Setup Method}

%% Managed Service Path
F -- Managed Service --> G[Book On-Site Technician]
G --> H[Status: Waiting for Setup]
H --> I[Technician Activates System]

%% Self-Service Path
F -- Self Service --> J[Smart Agent Wizard]
J --> K[Download & Install Master Agent]
K --> L[Auto-Discovery Services]
L --> M[Select Devices to Monitor]
M --> N[Get Installation Script]
N --> O[User runs script on server]
O --> P[Status: Waiting for Connection]

%% Approval Decision
P --> Q{Approve Profile?}
Q -- Yes --> R[Dashboard Active]
Q -- No --> M

%% Connect Managed Service to Dashboard
I --> R

%% --- MONITORING & RESPONSE FLOW ---
R --> S[Critical Anomaly Detected]
S --> T[Send Push Notification / Email]
T --> U{User Decision?}

%% User Takes Action
U -- Take Action --> V[Isolate Host / Block IP]
V --> W[System Apply Rules]
W --> X[Status: Mitigated]

%% Escalation Path
U -- Request Help --> Y[Escalate to Analyst]
Y --> Z[Notify HQ Tier 2]
Z --> AA[Analyst Takes Action]
AA --> X
```
