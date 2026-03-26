# Task & Dataset

CloudGuard AI's effectiveness depends on processing large telemetry data and differentiating genuine system activity from security threats. This page details our main machine learning tasks and the data composition for training and inference.

### 1. The Machine Learning Task

The core objective of CloudGuard AI is **Unsupervised and Semi-Supervised Anomaly Detection**. Rather than relying solely on static, pre-defined attack signatures, the system learns the unique "normal" behavior of a specific network to identify outliers.

#### Tiered Detection Objectives:

* **Edge Task (Isolation Forest):** To perform rapid, point-in-time anomaly scoring to detect "loud" or high-signal attacks (e.g., sudden spikes in failed logins or unusual process executions) with minimal computational overhead.
* **HQ Task (Deep LSTM-Autoencoder):** To perform sequential behavioral analysis, identifying "low-and-slow" attacks and insider threats that appear normal in isolation but suspicious over a prolonged time window.

***

### 2. Dataset Composition

CloudGuard AI handles a massive volume of data, with a typical SMB generating tens of millions of security log lines daily\[1]. Our dataset is composed of three primary streams:

#### A. Raw Telemetry (Features)

The system captures diverse event data from monitored endpoints:

* **Process Execution:** Information on what applications are starting and their parent-child relationships.
* **Network Activity:** Source/Destination IPs, ports, and protocol types.
* **Access Attempts:** Login timestamps, user IDs, and authentication success/failure status.
* **System Metadata:** Hostnames, OS types, and agent versions.

#### B. The Baseline (Silent Learning)

Upon initial deployment, the system enters a **two-week "Silent Learning" phase**. During this period, the models ingest all local network activity to build a unique behavioral baseline for that specific organization. This historical "Hot Data" is stored at HQ for 1–4 weeks to facilitate this training window.

#### C. The Feedback Loop (Labels)

While the primary models are unsupervised, the dataset is enriched by human intelligence. When a SOC Analyst reviews an alert and marks it as a **True Positive (TP)** or **False Positive (FP)**, that decision is stored as a labeled case. This labeled data is fed back into the MLOps pipeline to retrain and tune the models for higher accuracy.

***

### 3. Feature Engineering

To make the raw logs digestible for AI models, we apply several encoding strategies:

* **Cyclical Encoding:** Used for time-based features (e.g., hour of the day) to help the model understand that 23:59 and 00:01 are close together.
* **One-Hot/Frequency Encoding:** Converts categorical data, such as process names or action types, into numerical values.
* **Perimeter Logic:** Identifies whether IP addresses are internal or external, focusing on perimeter-crossing anomalies.

\[1]Microsoft. “2024 Microsoft Digital Defense Report.” 2024.\
Microsoft reports observing 78 trillion security signals per day across cloud, endpoints, and other sources, highlighting the massive scale of modern security telemetry.
