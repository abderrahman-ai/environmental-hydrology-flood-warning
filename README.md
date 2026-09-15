<div align="center">

<br/>

```
██████╗ ██████╗  ██████╗     ███╗   ██╗██████╗ ███╗   ██╗
██╔══██╗██╔══██╗██╔════╝     ████╗  ██║██╔══██╗████╗  ██║
██████╔╝██████╔╝██║  ███╗    ██╔██╗ ██║██████╔╝██╔██╗ ██║
██╔══██╗██╔═══╝ ██║   ██║    ██║╚██╗██║██╔═══╝ ██║╚██╗██║
██║  ██║██║     ╚██████╔╝    ██║ ╚████║██║     ██║ ╚████║
╚═╝  ╚═╝╚═╝      ╚═════╝     ╚═╝  ╚═══╝╚═╝     ╚═╝  ╚═══╝
                         HYDROLOGY
```

<h3>Environmental Hydrology & Flood Warning Pipeline</h3>

<br/>

[![n8n](https://img.shields.io/badge/Built%20on-n8n-FF6584?style=flat-square&logo=n8n&logoColor=white)](https://n8n.io/)
[![Status](https://img.shields.io/badge/Status-Live--Active-3ECF8E?style=flat-square)](https://n8n.io/)
[![Nodes](https://img.shields.io/badge/Nodes-15%20Nodes-1C3A5F?style=flat-square)](https://n8n.io/)
[![License](https://img.shields.io/badge/License-MIT-F7DF1E?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-00C48C?style=flat-square)](http://makeapullrequest.com)

<br/>

[**→ Quick Start**](#-installation) · [**→ Architecture**](#-architecture) · [**→ Node Inventory**](#-node-inventory) · [**→ Usage**](#-usage-examples)

<br/>

</div>

---

## What is this?

A production-ready, automated n8n pipeline for **Environmental Hydrology & Flood Warning Pipeline**. Designed for enterprise-grade execution, seamless API integration, and real-time operational dispatch.

| | Component | What it does |
|---|---|---|
| **📥** | **Sticky Note - Ingestion Layer** | Ingests triggers, webhooks, or scheduled telemetry payloads |
| **🧠** | **Sticky Note - Hydrology Engine** | Processes logic, evaluates conditions, and enriches data |
| **🚨** | **Sticky Note - Alerting & Dispatch** | Dispatches alert notifications, updates databases, and executes actions |

---

## 📑 Table of Contents

- [Architecture](#-architecture)
- [Core Features](#-core-features)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Node Inventory](#-node-inventory)
- [Usage Examples](#-usage-examples)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🏗 Architecture

```mermaid
%%{init: {'theme': 'dark', 'themeVariables': {'primaryColor': '#1a1a2e', 'primaryTextColor': '#e0e0e0', 'primaryBorderColor': '#3498DB', 'lineColor': '#3498DB', 'secondaryColor': '#16213e', 'edgeLabelBackground': '#0d0d0d', 'clusterBkg': '#0d0d0d'}}}%%
graph TD
    Sticky_Note_Ingestion_Layer["Sticky Note - Ingestion Layer<br/><i>(stickyNote)</i>"]
    Sticky_Note_Hydrology_Engine["Sticky Note - Hydrology Engine<br/><i>(stickyNote)</i>"]
    Sticky_Note_Alerting_Dispatch["Sticky Note - Alerting & Dispatch<br/><i>(stickyNote)</i>"]
    Sticky_Note_Supabase_Crisis_DB["Sticky Note - Supabase Crisis DB<br/><i>(stickyNote)</i>"]
    Schedule_Hourly_Cycle["Schedule_Hourly_Cycle<br/><i>(scheduleTrigger)</i>"]
    Webhook_Manual_Trigger["Webhook_Manual_Trigger<br/><i>(webhook)</i>"]
    Ingest_Hydrometry_and_Radar["Ingest_Hydrometry_and_Radar<br/><i>(code)</i>"]
    Ense3_Runoff_and_Crest_Projection["Ense3_Runoff_and_Crest_Projection<br/><i>(code)</i>"]
    Evaluate_Alert_Thresholds["Evaluate_Alert_Thresholds<br/><i>(if)</i>"]
    Format_Emergency_Dispatch_Payload["Format_Emergency_Dispatch_Payload<br/><i>(code)</i>"]
    Dispatch_Emergency_SMS["Dispatch_Emergency_SMS<br/><i>(httpRequest)</i>"]
    Dispatch_Telegram_Alert["Dispatch_Telegram_Alert<br/><i>(httpRequest)</i>"]
    Format_Crisis_Database_Payload["Format_Crisis_Database_Payload<br/><i>(code)</i>"]
    Format_Nominal_Baseline_Payload["Format_Nominal_Baseline_Payload<br/><i>(code)</i>"]
    Persist_to_Supabase_Crisis_DB["Persist_to_Supabase_Crisis_DB<br/><i>(httpRequest)</i>"]
    Dispatch_Emergency_SMS --> Dispatch_Telegram_Alert
    Dispatch_Telegram_Alert --> Format_Crisis_Database_Payload
    Ense3_Runoff_and_Crest_Projection --> Evaluate_Alert_Thresholds
    Evaluate_Alert_Thresholds --> Format_Emergency_Dispatch_Payload
    Evaluate_Alert_Thresholds --> Format_Nominal_Baseline_Payload
    Format_Crisis_Database_Payload --> Persist_to_Supabase_Crisis_DB
    Format_Emergency_Dispatch_Payload --> Dispatch_Emergency_SMS
    Format_Nominal_Baseline_Payload --> Persist_to_Supabase_Crisis_DB
    Ingest_Hydrometry_and_Radar --> Ense3_Runoff_and_Crest_Projection
    Schedule_Hourly_Cycle --> Ingest_Hydrometry_and_Radar
    Webhook_Manual_Trigger --> Ingest_Hydrometry_and_Radar
```

---

## ✦ Core Features

<table>
<tr>
<td width="50%" valign="top">

**📡 &nbsp;Event-Driven Triggering**  
Supports real-time webhooks and automated cron schedules for instant event evaluation without polling overhead.

---

**⚡ &nbsp;High-Throughput Processing**  
Structured data transformation nodes handle high payload concurrency with zero data degradation.

---

**🔒 &nbsp;Robust Error Handling**  
Built-in fallback handlers ensure graceful failures, detailed logging, and operational safety.

</td>
<td width="50%" valign="top">

**🧠 &nbsp;Intelligent Logic Routing**  
Conditional evaluation branches route high-priority anomalies directly to incident response teams.

---

**📊 &nbsp;Unified Telemetry Sync**  
Synchronizes metrics and operational logs across databases, analytical dashboards, and alert channels.

---

**🔌 &nbsp;Zero-Code Integration**  
Modular n8n blueprint imports directly into any n8n instance with zero extra dependencies.

</td>
</tr>
</table>

---

## 🔧 Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Orchestration | [n8n](https://n8n.io/) | Workflow engine, cron scheduling, webhook handling |
| Execution Engine | Node.js / JavaScript | Code execution and custom payload transformations |
| Communication | Webhook / REST APIs | Bi-directional API integrations & alert dispatch |
| Blueprint Format | JSON (n8n v1+) | Importable, version-controlled workflow definition |

---

## ✅ Prerequisites

- **n8n instance** — self-hosted (v1.0+) or [n8n Cloud](https://app.n8n.cloud)
- **API Credentials** — Configure relevant integration service credentials inside your n8n credentials panel.

---

## ⚙️ Installation

### 1 · Import the Workflow

```
Workflows → ⋯ → Import from File → workflow.json
```

### 2 · Attach Credentials

```
┌─────────────────────┬───────────────────┬──────────────────────────────────────┐
│ Credential          │ Type              │ Attach To                            │
├─────────────────────┼───────────────────┼──────────────────────────────────────┤
│ API / Webhook Keys  │ HTTP / OAuth2     │ Integration & Service Nodes          │
└─────────────────────┴───────────────────┴──────────────────────────────────────┘
```

### 3 · Activate

```
Workflows → [Environmental Hydrology & Flood Warning Pipeline] → Toggle to Active ✓
```

---

## 📑 Node Inventory

| # | Node Name | Type | Status |
|---|---|---|:---:|
| `01` | **Sticky Note - Ingestion Layer** | `stickyNote` | Active |
| `02` | **Sticky Note - Hydrology Engine** | `stickyNote` | Active |
| `03` | **Sticky Note - Alerting & Dispatch** | `stickyNote` | Active |
| `04` | **Sticky Note - Supabase Crisis DB** | `stickyNote` | Active |
| `05` | **Schedule_Hourly_Cycle** | `scheduleTrigger` | Active |
| `06` | **Webhook_Manual_Trigger** | `webhook` | Active |
| `07` | **Ingest_Hydrometry_and_Radar** | `code` | Active |
| `08` | **Ense3_Runoff_and_Crest_Projection** | `code` | Active |
| `09` | **Evaluate_Alert_Thresholds** | `if` | Active |
| `10` | **Format_Emergency_Dispatch_Payload** | `code` | Active |
| `11` | **Dispatch_Emergency_SMS** | `httpRequest` | Active |
| `12` | **Dispatch_Telegram_Alert** | `httpRequest` | Active |
| `13` | **Format_Crisis_Database_Payload** | `code` | Active |
| `14` | **Format_Nominal_Baseline_Payload** | `code` | Active |
| `15` | **Persist_to_Supabase_Crisis_DB** | `httpRequest` | Active |

---

## 🧪 Usage Examples

### cURL — Trigger Workflow Webhook

```bash
curl -X POST https://your-n8n-instance.com/webhook/environmental-hydrology-flood-warning \
  -H "Content-Type: application/json" \
  -d '{"timestamp": "2026-09-15T12:00:00Z", "status": "TRIGGER_EVALUATION"}'
```

### Python — Trigger Integration

```python
import requests

url = "https://your-n8n-instance.com/webhook/environmental-hydrology-flood-warning"
payload = {"event": "HEALTH_CHECK", "source": "python_agent"}

response = requests.post(url, json=payload)
print("Status Code:", response.status_code)
print("Response:", response.json())
```

---

## 📂 Project Structure

```
environmental-hydrology-flood-warning/
├── workflow.json      # Complete importable workflow definition
├── LICENSE            # MIT License file
└── README.md          # Comprehensive documentation
```

---

## 🤝 Contributing

Contributions, feature requests, and bug reports are welcome!

```bash
# 1. Fork the repository
git clone https://github.com/abderrahman-ai/environmental-hydrology-flood-warning.git

# 2. Create your feature branch
git checkout -b feat/new-capability

# 3. Commit your changes
git commit -m "feat: enhance node error handling"

# 4. Push and open a Pull Request
git push origin feat/new-capability
```

---

## 📄 License

Released under the **MIT License** — see [`LICENSE`](LICENSE) for full details.

---

<div align="center">

<br/>

Built with [n8n](https://n8n.io/) · Automated Enterprise Operations

<br/>

**[⬆ Back to top](#)**

</div>
