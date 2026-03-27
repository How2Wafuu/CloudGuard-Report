# Project management

Delivering a complex, multi-tiered architecture like CloudGuard AI requires strict coordination across our Software, Network, and Machine Learning workstreams. We utilized a modern, agile-inspired stack to ensure continuous integration, clear communication, and timely delivery.

### 1. Methodology & Communication

To manage the moving parts of the Edge-Cloud-HQ architecture, we implemented the following strategies:

* **Continuous Communication (Discord):** We utilized dedicated Discord channels for daily cross-functional communication. This allowed for rapid troubleshooting between the Network and Software teams.
* **Milestone Syncs:** We held regular voice/video alignment syncs on Discord, such as **Progress Meeting 4**, to address specific technical roadblocks (e.g., designing logic to handle unknown log events at the Edge).

### 2. Task Delegation & Oversight (ClickUp)

<figure><img src=".gitbook/assets/Screenshot 2569-03-26 at 17.04.07.png" alt=""><figcaption></figcaption></figure>

We utilize **ClickUp** as our primary project management platform to track tasks, plan sprints, and monitor completed milestones. Task tracking was categorized by engineering domains to ensure strict accountability:

* **Network Engineering:** Focused on the hardware BOM, physical and logical topologies, WiFi heatmap, and network service.
* **UI/UX & Machine Learning:** Managed Figma prototyping, client onboarding flows, and the multi-tenant database schema design.
* **Systems Engineering:** Handled data engineering, the deployment of the Isolation Forest and LSTM-Autoencoder models, as well as AWS cloud ingestion buffers and the HQ data center design and equipment selection.

> 🔒 **Access Control Note for Evaluators:** _To maintain workspace security and prevent unauthorized edits to our live production board, the direct access link to the CloudGuard AI ClickUp workspace is not published publicly. The secure access link has been provided directly via the Canvas submission portal._

### 3. Version Control & Code Repositories

To maintain strict version control over our documentation and codebase, we utilize **GitHub**:

* **Documentation:** All technical documentation, code snippets, and architectural diagrams are maintained centrally using GitBook, which syncs directly to our documentation repository.
* **AI/ML Mockup:** The proof-of-concept code and Jupyter Notebooks for our Machine Learning models (Isolation Forest and LSTM) are hosted in a dedicated, public repository for evaluator review.

{% embed url="https://github.com/How2Wafuu/CloudGuard-Report" %}

{% embed url="https://github.com/How2Wafuu/CloudGuard-ML-Mockup" %}
