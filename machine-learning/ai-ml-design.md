# AI / ML Design (Edge & HQ)

CloudGuard AI uses a **two-level AI architecture**. The edge model performs fast, lightweight anomaly detection, while the HQ model performs deeper analysis using richer context and aggregated data. This division reflects the difference between immediate endpoint decisions and centralized behavioral analysis.

## Edge Agent ML

The **Edge Agent** is designed for fast local detection and immediate response with minimal overhead.

### Model

- **Isolation Forest**

### Purpose

- Detect obvious or high-signal anomalies quickly
- Support instant blocking or early warning at the device/site level
- Minimize performance impact on endpoints

### Feature Engineering

- **Cyclical encoding** for time features
- **One-hot encoding** for categorical features such as process, action, or user-style attributes
- **External/internal IP logic** to identify perimeter-related anomalies

This model is appropriate for detecting loud attacks such as unusual access patterns, suspicious process activity, or clear deviations from normal local behavior.

## HQ ML

The **HQ layer** performs more computationally expensive and context-rich analysis.

### Models

- **Deep LSTM Autoencoder** for sequential anomaly detection
- **DistilBERT / semantic embedding layer** for text, email, or message understanding

### Purpose

- Detect low-and-slow attacks
- Detect insider threats
- Analyze multi-event or sequence-based behavior
- Use richer centralized context across devices, users, and cases

Compared with the edge model, HQ analysis can incorporate longer time windows, aggregated organizational behavior, and semantic context from textual security artifacts. This makes it more suitable for subtle attacks that are difficult to detect from a single local event.

## Risk Scoring and Enrichment

Model outputs can be converted into operational risk scores by combining:

- **Model confidence**
- **Asset criticality**

A practical interpretation is:

- High anomaly score on a low-value asset → lower response urgency
- High anomaly score on a critical server or executive device → higher response urgency

The design also supports **behavioral mapping to MITRE ATT&CK** and future enrichment through **threat intelligence APIs**. This allows anomaly detection results to be translated into security-relevant categories and enriched with external context when needed.
