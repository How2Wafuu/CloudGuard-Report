# Storage & Bandwidth Strategy

## Tiered Storage Strategy

CloudGuard AI uses tiered storage so that performance-sensitive data stays close to HQ while older data is kept more economically:

- **HQ Hot Storage (1–4 weeks)**
  Used for fast search, active investigations, and the model training window.

- **Cloud Warm Storage (1–3 months)**
  Used for lower-cost storage of less frequently accessed data.

- **Cloud Cold Storage (6+ months / years)**
  Used for archive and long-term retention.

This storage lifecycle matches the operational needs of a SOC: recent data must be searchable and actionable, while older data should remain available at lower storage cost and lower retrieval priority.

## Bandwidth Strategy

To keep the hybrid design practical, the system applies bandwidth reduction at multiple stages:

- **Edge reduction:** filter + tag + sample
- **Cloud buffer:** batching + compression
- **HQ selective pull:** anomalies, features, and scheduled transfer only

This layered reduction strategy prevents the VPN link from becoming the main ingestion bottleneck.
