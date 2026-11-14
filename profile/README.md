# VectorDuct

**[简体中文](./README.zh-CN.md)**

**Intelligence should flow through infrastructure you trust.**

VectorDuct is a multi-model reliability & FinOps stack for engineering teams: self-hosted request validation, native cloud access, sovereign usage telemetry, and allowlisted multimodal workflows across OpenAI-compatible APIs, DeepSeek, Anthropic, and Google Cloud Vertex AI.

- **Official Website**: [https://vectorduct.com](https://vectorduct.com)
- **Commercial Platform Subscriptions**: [https://vectorduct.com/#pricing](https://vectorduct.com/#pricing)
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
    [ OpenAI-compatible / DeepSeek / Anthropic / Vertex AI ]
```

### Core Open-Source Repositories

| Repository | Layer | License | Description |
| --- | --- | --- | --- |
| **[`dsh-vertex-plugin`](https://github.com/VectorDuct/dsh-vertex-plugin)** (Direct Cloud Bridge) | **Connect** | `MIT` | Native Google Cloud Vertex AI service-account authentication and model access plugin for DSH with strict BYOC credential isolation. |
| **[`input-check`](https://github.com/VectorDuct/input-check)** (Wire-Level Guard) | **Operate** | `MIT` | Model request structure validator and configurable fixed-upstream routing gateway for deterministic API governance. |
| **[`usage-dashboard`](https://github.com/VectorDuct/usage-dashboard)** (Sovereign Telemetry) | **Operate** | `MIT` | Read-only quota monitoring, token consumption analytics, and automated SQLite daily historical snapshot dashboard. |
| **[`astrbot_plugin_visual_pipeline`](https://github.com/VectorDuct/astrbot_plugin_visual_pipeline)** (Workflow Conduit) | **Build** | `MIT` | AstrBot workflow connector executing explicit image generation pipelines against self-hosted multimodal APIs. |
| **[`vectorduct-web`](https://github.com/VectorDuct/vectorduct-web)** | **Web** | `Proprietary` | Official documentation and architecture portal deployed at [`vectorduct.com`](https://vectorduct.com). |

### Open-Core & Enterprise Delivery

All four product primitives are available under the MIT license. Production teams can subscribe to commercial platforms for managed hybrid control planes, FinOps attribution, and enterprise VPC governance:

- **VectorDuct Pro — $99/mo Managed Hybrid Cloud**: Managed control plane with centralized quota snapshots, multi-region routing, token FinOps attribution, department chargeback ledgers, and native **Google Cloud Logging & BigQuery** exports.
- **VectorDuct Enterprise VPC Edition**: Private Terraform / GKE / Cloud Run fleet provisioning inside your own cloud account, SAML/OIDC SSO integration, custom adapter engineering, and 99.95% uptime SLA support.

For architecture reviews or platform subscriptions, reach out to our founding team at **[founders@vectorduct.com](mailto:founders@vectorduct.com)**.
