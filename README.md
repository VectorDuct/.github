# VectorDuct

**[简体中文](./README.zh-CN.md)**

**Self-Hosted AI Gateway, Request Governance & Multimodal Workflow Connectors.**

VectorDuct builds open-source infrastructure for engineering teams to connect Google Cloud Vertex AI endpoints, validate model request payloads, track daily quota snapshots, and wire visual generation pipelines into messaging tools—entirely within your own VPC.

- **Official Website**: [https://vectorduct.com](https://vectorduct.com)
- **Commercial & Managed VPC Editions**: [https://vectorduct.com/#pricing](https://vectorduct.com/#pricing)
- **Engineering & Enterprise Inquiries**: [contact@vectorduct.com](mailto:contact@vectorduct.com)

---

### System Architecture & Request Pipeline

```text
[ Client SDKs / AstrBot Messaging / Internal Tools ]
                         │
                         ▼
┌────────────────────────────────────────────────────────┐
│  01. astrbot_plugin_visual_pipeline (Build Layer)      │  ◄── Explicit Command Parsing &
│      Event-Driven Bot & Visual Generation Connector    │      Self-Hosted Image API Dispatch
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  02. input-check & usage-dashboard (Operate Layer)     │  ◄── Request Schema Validation,
│      Fixed-Upstream Gateway & Daily Quota Snapshots    │      Quota Tracking & Telemetry
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  03. dsh-vertex-plugin (Connect Layer)                 │  ◄── Vertex AI Service-Account Auth
│      Native Google Cloud Vertex AI Access Plugin       │      & Strict BYOC Isolation
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
    [ Google Cloud Vertex AI / Gemini / Upstream APIs ]
```

### Core Open-Source Repositories

| Repository | Layer | License | Description |
| --- | --- | --- | --- |
| **[`dsh-vertex-plugin`](https://github.com/VectorDuct/dsh-vertex-plugin)** | **Connect** | `MIT` | Native Google Cloud Vertex AI service-account authentication and model access plugin for DSH with strict BYOC credential isolation. |
| **[`input-check`](https://github.com/VectorDuct/input-check)** | **Operate** | `MIT` | Model request structure validator and configurable fixed-upstream routing gateway for deterministic API governance. |
| **[`usage-dashboard`](https://github.com/VectorDuct/usage-dashboard)** | **Operate** | `MIT` | Read-only quota monitoring, token consumption analytics, and automated SQLite daily historical snapshot dashboard. |
| **[`astrbot_plugin_visual_pipeline`](https://github.com/VectorDuct/astrbot_plugin_visual_pipeline)** | **Build** | `MIT` | AstrBot workflow connector executing explicit image generation pipelines against self-hosted multimodal APIs. |
| **[`vectorduct-web`](https://github.com/VectorDuct/vectorduct-web)** | **Web** | `Proprietary` | Official documentation and architecture portal deployed at [`vectorduct.com`](https://vectorduct.com). |

### Open-Core & Enterprise Delivery

While our core routing plugins, request validators, and telemetry dashboards are open-source under permissive licenses, VectorDuct provides commercial engineering and managed services for production teams:

- **VectorDuct Cloud & Pro**: Managed control plane with centralized quota snapshots, multi-region routing, and native **Google Cloud Logging & BigQuery** cost attribution exports.
- **Enterprise & Managed VPC**: Private Terraform / GKE / Cloud Run fleet provisioning inside your own cloud account, SAML/OIDC SSO integration, custom adapter engineering, and 99.95% uptime SLA support.

For architecture reviews or commercial licensing, reach out to our founding team at **[founders@vectorduct.com](mailto:founders@vectorduct.com)**.
