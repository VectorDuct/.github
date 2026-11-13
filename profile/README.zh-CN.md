# VectorDuct

**[English](./README.md)**

**自托管 AI 网关、请求治理与多模态工作流连接器。**

VectorDuct 为工程团队构建开源基础设施，连接 Google Cloud Vertex AI 端点、校验模型请求结构、追踪每日配额快照，并将图像生成工作流接入消息工具，支持部署于自有基础设施。

- **官方网站**：[https://vectorduct.com](https://vectorduct.com)
- **商业与托管 VPC 版本**：[https://vectorduct.com/#pricing](https://vectorduct.com/#pricing)
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
    [ Google Cloud Vertex AI / Gemini / Upstream APIs ]
```

### 核心开源仓库

| 仓库 | 层次 | 许可 | 说明 |
| --- | --- | --- | --- |
| [dsh-vertex-plugin](https://github.com/VectorDuct/dsh-vertex-plugin) | Connect | MIT | 面向 DSH 的原生 Google Cloud Vertex AI 服务账号鉴权与模型接入插件，使用部署者自有凭据。 |
| [input-check](https://github.com/VectorDuct/input-check) | Operate | MIT | 模型请求结构检查器与可配置的固定上游网关。 |
| [usage-dashboard](https://github.com/VectorDuct/usage-dashboard) | Operate | MIT | 只读配额监控、Token 用量分析与 SQLite 每日历史快照看板。 |
| [astrbot_plugin_visual_pipeline](https://github.com/VectorDuct/astrbot_plugin_visual_pipeline) | Build | MIT | 通过显式指令连接自托管多模态 API 的 AstrBot 图像生成工作流插件。 |
| [vectorduct-web](https://github.com/VectorDuct/vectorduct-web) | Web | 专有 | 部署于 [vectorduct.com](https://vectorduct.com) 的官方网站与架构门户。 |

### Open-Core 与企业交付

核心接入插件、请求校验器和用量看板以宽松开源许可提供；VectorDuct 面向生产团队提供商业工程及托管服务：

- **VectorDuct Cloud & Pro**：托管控制平面、集中式配额快照、多区域路由，以及 Google Cloud Logging 和 BigQuery 成本归属导出。
- **Enterprise & Managed VPC**：在客户云账号内使用 Terraform、GKE 或 Cloud Run 部署，集成 SAML/OIDC SSO，提供定制适配器工程及 99.95% 可用性 SLA 支持。

架构评审或商业许可咨询，请联系 [founders@vectorduct.com](mailto:founders@vectorduct.com)。
