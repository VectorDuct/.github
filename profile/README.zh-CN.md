# VectorDuct

**[English](./README.md)**

**Intelligence should flow through infrastructure you trust.**

VectorDuct 是面向工程团队的多模型可靠性与 FinOps 技术栈，提供自托管请求校验、原生云端接入、自主掌控的用量遥测及白名单多模态工作流，覆盖 OpenAI 兼容接口、DeepSeek、Anthropic 与 Google Cloud Vertex AI。

- **官方网站**：[https://vectorduct.com](https://vectorduct.com)
- **商业平台订阅版本**：[https://vectorduct.com/#pricing](https://vectorduct.com/#pricing)
- **工程与企业咨询**：[contact@vectorduct.com](mailto:contact@vectorduct.com)

---

### 系统架构与请求处理

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

### 核心开源仓库

| 仓库 | 层次 | 许可 | 说明 |
| --- | --- | --- | --- |
| [dsh-vertex-plugin](https://github.com/VectorDuct/dsh-vertex-plugin) (Direct Cloud Bridge) | Connect | MIT | 面向 DSH 的原生 Google Cloud Vertex AI 服务账号鉴权与模型接入插件，使用部署者自有凭据。 |
| [input-check](https://github.com/VectorDuct/input-check) (Wire-Level Guard) | Operate | MIT | 模型请求结构检查器与可配置的固定上游网关。 |
| [usage-dashboard](https://github.com/VectorDuct/usage-dashboard) (Sovereign Telemetry) | Operate | MIT | 只读配额监控、Token 用量分析与 SQLite 每日历史快照看板。 |
| [astrbot_plugin_visual_pipeline](https://github.com/VectorDuct/astrbot_plugin_visual_pipeline) (Workflow Conduit) | Build | MIT | 通过显式指令连接自托管多模态 API 的 AstrBot 图像生成工作流插件。 |
| [vectorduct-web](https://github.com/VectorDuct/vectorduct-web) | Web | 专有 | 部署于 [vectorduct.com](https://vectorduct.com) 的官方网站与架构门户。 |

### Open-Core 与企业交付

四个产品原语均以 MIT 协议开源；生产团队可订阅商业平台，获取托管混合云控制面、FinOps 成本归因与企业 VPC 治理：

- **VectorDuct Pro — $99/mo Managed Hybrid Cloud**：每月 99 美元的托管混合云版本，提供托管控制平面、集中式配额快照、多区域路由、Token FinOps 成本归因、部门费用分摊账单，以及 Google Cloud Logging 和 BigQuery 导出。
- **VectorDuct Enterprise VPC Edition**：在客户云账号内使用 Terraform、GKE 或 Cloud Run 部署，集成 SAML/OIDC SSO，提供定制适配器工程及 99.95% 可用性 SLA 支持。

架构评审或平台订阅咨询，请联系 [founders@vectorduct.com](mailto:founders@vectorduct.com)。
