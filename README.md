# VectorDuct

**Self-Hosted AI Gateway, Protocol Middleware & Workflow Connectors.**

VectorDuct builds open-source infrastructure for engineering teams to standardize foundation model schemas, enforce multi-tenant token quotas, and wire asynchronous generation pipelines into existing tools—entirely within your own VPC.

- **Website & Architecture**: [https://vectorduct.com](https://vectorduct.com)
- **Commercial & Managed VPC Editions**: [https://vectorduct.com/#pricing](https://vectorduct.com/#pricing)
- **Engineering & Enterprise Inquiries**: [contact@vectorduct.com](mailto:contact@vectorduct.com)

---

### System Architecture & Request Pipeline

```text
  [ Client SDKs / Internal Tools / Chat Webhooks ]
                         │
                         ▼
  ┌──────────────────────────────────────────────┐
  │  01. vectorduct-bot-bridge (Build Layer)     │  ◄── Async Queues, Webhook Normalization
  └──────────────────────┬───────────────────────┘
                         │
                         ▼
  ┌──────────────────────────────────────────────┐
  │  02. vectorduct-gateway (Operate Layer)      │  ◄── Multi-Tenant RBAC, RPM/TPM Quotas,
  │      [Extended Distribution of new-api]      │      Circuit Breaking & Token Telemetry
  └──────────────────────┬───────────────────────┘
                         │
                         ▼
  ┌──────────────────────────────────────────────┐
  │  03. dsh-vertex-adapter (Connect Layer)      │  ◄── In-Memory Schema Translation &
  │      [Original Core Protocol Bridge]         │      Strict BYOC Credential Isolation
  └──────────────────────┬───────────────────────┘
                         │
                         ▼
  [ Google Cloud Vertex AI / Gemini API / Upstream Models ]
Core Open-Source StackRepositoryLayerLicense & LineageDescriptiondsh-vertex-adapterConnectApache-2.0 · OriginalZero-dependency protocol bridge translating OpenAI and Anthropic tool-calling schemas into native Google Gemini and Vertex AI wire formats.vectorduct-gatewayOperateMIT · Extended from new-apiHardened API gateway distribution featuring organization-level RBAC, deterministic budget ceilings, automatic failover, and structured log sinks.vectorduct-bot-bridgeBuildApache-2.0 · OriginalEvent-driven connectors bridging team messaging platforms and webhooks to asynchronous text and visual generation workflows.Open-Core & Enterprise DeliveryWhile our core routing adapters and single-node gateway distributions remain free and open-source under permissive licenses, VectorDuct provides commercial offerings for production teams:VectorDuct Cloud & Pro: Managed control plane with hybrid data-plane routing, multi-region active-active failover, and native Google Cloud Logging & BigQuery cost attribution exporters.Enterprise & Managed VPC: Private Terraform / GKE / Cloud Run fleet provisioning inside your own cloud account, SAML/OIDC SSO integration, custom protocol adapter engineering, and 99.95% uptime SLA support.For architecture reviews or commercial licensing, reach out to our founding team at founders@vectorduct.com.
