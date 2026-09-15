<div align="center">

<br/>

```
    __  ____  ______  ____  ____  __    ____  ________  __
   / / / /\ \/ / __ \/ __ \/ __ \/ /   / __ \/ ____/\ \/ /
  / /_/ /  \  / / / / /_/ / / / / /   / / / / / __   \  / 
 / __  /   / / /_/ / _, _/ /_/ / /___/ /_/ / /_/ /   / /  
/_/ /_/   /_/_____/_/ |_|\____/_____/\____/\____/   /_/
```

<h3>Environmental Hydrology & Flood Warning Pipeline</h3>

<br/>

[![n8n](https://img.shields.io/badge/Built%20on-n8n-FF6584?style=flat-square&logo=n8n&logoColor=white)](https://n8n.io/)
[![Status](https://img.shields.io/badge/Status-Live-3ECF8E?style=flat-square)](https://n8n.io/)
[![Nodes](https://img.shields.io/badge/Nodes-15%20Nodes-1C3A5F?style=flat-square)](https://n8n.io/)
[![License](https://img.shields.io/badge/License-MIT-F7DF1E?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-00C48C?style=flat-square)](http://makeapullrequest.com)

<br/>

[**Quick Start**](#-installation) | [**Architecture**](#-architecture) | [**Node Inventory**](#-node-inventory) | [**Usage**](#-usage-examples)

<br/>

</div>

---

## What is this?

An automated n8n workflow for **Environmental Hydrology & Flood Warning Pipeline**. It processes incoming events, transforms data payloads, and handles conditional dispatch to downstream services.

| | Component | Purpose |
|---|---|---|
| **📥** | **Sticky Note - Ingestion Layer** | Ingests incoming webhooks or scheduled telemetry payloads |
| **🧠** | **Sticky Note - Hydrology Engine** | Evaluates logic conditions and enriches message data |
| **🚨** | **Sticky Note - Alerting & Dispatch** | Dispatches notifications and updates database records |

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
    Sticky_Note_Ingestion_Layer["Sticky Note: Ingestion Layer<br/><i>(stickyNote)</i>"]
    Sticky_Note_Hydrology_Engine["Sticky Note: Hydrology Engine<br/><i>(stickyNote)</i>"]
    Sticky_Note_Alerting_Dispatch["Sticky Note: Alerting & Dispatch<br/><i>(stickyNote)</i>"]
    Sticky_Note_Supabase_Crisis_DB["Sticky Note: Supabase Crisis DB<br/><i>(stickyNote)</i>"]
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
Supports incoming webhooks and scheduled cron jobs for automatic background processing.

---

**⚡ &nbsp;Data Normalization**  
Standardizes raw input fields before forwarding payloads to analytics databases.

---

**🔒 &nbsp;Error Handling**  
Catches execution exceptions to prevent failed runs from stopping pipeline flow.

</td>
<td width="50%" valign="top">

**🧠 &nbsp;Conditional Logic**  
Filters high-priority alerts so team members only receive urgent notifications.

---

**📊 &nbsp;System Synchronization**  
Keeps external databases, logs, and notification channels in sync.

---

**🔌 &nbsp;Easy Import**  
Import the blueprint JSON directly into your n8n workspace to get started.

</td>
</tr>
</table>

---

## 🔧 Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Orchestration | [n8n](https://n8n.io/) | Workflow engine, cron scheduling, webhook routing |
| Execution Engine | Node.js / JavaScript | Payload parsing and custom data mapping |
| Transport Protocol | Webhook / REST APIs | API requests and notification delivery |
| Blueprint Format | JSON (n8n v1+) | Portable workflow definition file |

---

## ✅ Prerequisites

- **n8n instance** (self-hosted or [n8n Cloud](https://app.n8n.cloud))
- Relevant API credentials configured inside your n8n workspace

---

## ⚙️ Installation

### 1. Import the Workflow

```
Workflows -> Import from File -> workflow.json
```

### 2. Configure Credentials

```
+---------------------+-------------------+--------------------------------------+
| Credential          | Type              | Attach To                            |
+---------------------+-------------------+--------------------------------------+
| API / Webhook Keys  | HTTP / OAuth2     | Integration Nodes                    |
+---------------------+-------------------+--------------------------------------+
```

### 3. Activate Workflow

```
Workflows -> [Environmental Hydrology & Flood Warning Pipeline] -> Toggle Active
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

### cURL: Trigger Webhook

```bash
curl -X POST https://your-n8n-instance.com/webhook/environmental-hydrology-flood-warning \
  -H "Content-Type: application/json" \
  -d '{"timestamp": "2026-09-15T12:00:00Z", "event": "HEALTH_CHECK"}'
```

### Python: Send Event

```python
import requests

url = "https://your-n8n-instance.com/webhook/environmental-hydrology-flood-warning"
payload = {"event": "HEALTH_CHECK", "source": "python_script"}

res = requests.post(url, json=payload)
print("Response code:", res.status_code)
print("Data:", res.json())
```

---

## 📂 Project Structure

```
environmental-hydrology-flood-warning/
├── workflow.json      # Complete importable workflow definition
├── LICENSE            # MIT License file
└── README.md          # Project documentation
```

---

## 🤝 Contributing

Pull requests and issues are welcome.

```bash
# 1. Clone the repository
git clone https://github.com/abderrahman-ai/environmental-hydrology-flood-warning.git

# 2. Create your branch
git checkout -b patch/improvements

# 3. Commit your changes
git commit -m "docs: refine workflow description and node names"

# 4. Push to origin
git push origin patch/improvements
```

---

## 📄 License

Released under the **MIT License**. Check [`LICENSE`](LICENSE) for full details.

---

<div align="center">

<br/>

Built with [n8n](https://n8n.io/)

<br/>

**[Back to top](#)**

</div>
