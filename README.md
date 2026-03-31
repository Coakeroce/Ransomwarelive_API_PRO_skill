# Ransomware.live API PRO — OpenClaw AgentSkill

<p align="center">
  <strong>AI-Powered Ransomware Threat Intelligence</strong><br>
  <em>23 API endpoints · 10 categories · OpenClaw compatible</em>
</p>

---

## Overview

This is an **OpenClaw AgentSkill** that integrates the [Ransomware.live API PRO](https://www.ransomware.live/api) into AI assistants, enabling comprehensive ransomware threat intelligence queries directly through natural language.

The skill covers **23 endpoints** across **10 categories**: victim tracking, group profiling, IOC extraction, negotiation logs, ransom notes, press coverage, SEC filings, YARA rules, CSIRT directories, and system utilities.

## Features

- **Victim Intelligence** — Search, filter, and retrieve victim details by date, country, group, keyword
- **Group Profiling** — TTPs, tooling, victim counts, and operational history for 327+ tracked groups
- **IOC Extraction** — IPs, MD5 hashes, email addresses, BTC wallets per group
- **Negotiation Logs** — Full chat transcripts with ransom demands and timelines
- **Ransom Notes** — Original ransom notes from active groups
- **Press Coverage** — Aggregated news reports on ransomware incidents
- **SEC 8-K Filings** — US cybersecurity incident disclosures
- **YARA Rules** — Detection signatures for specific ransomware families
- **CSIRT Directory** — National CERT/CSIRT contacts by country

## Prerequisites

- [OpenClaw](https://github.com/openclaw/openclaw) installed and configured
- A Ransomware.live API PRO key — [free signup](https://my.ransomware.live)

## Installation

### Via ClawdHub (recommended)

```bash
clawdhub install ransomware-live
```

### Manual

```bash
git clone https://github.com/your-repo/ransomware-live-skill.git ~/.openclaw/skills/ransomware-live
```

## Configuration

All API requests require authentication via the `X-API-KEY` header. Set your key in the skill configuration or `SKILL.md`:

```http
X-API-KEY: <your-api-key>
```

## API Endpoints

| Category | Endpoint | Method | Description |
|----------|----------|--------|-------------|
| **Victims** | `/victims/` | GET | Query victims with filters |
| | `/victims/recent` | GET | Latest 100 victims |
| | `/victims/search` | GET | Keyword search |
| | `/victim/{id}` | GET | Single victim detail (Base64 ID) |
| **Groups** | `/groups` | GET | All tracked ransomware groups |
| | `/groups/{name}` | GET | Group details (TTPs, tools, victims) |
| **IOCs** | `/iocs` | GET | Groups with IOCs |
| | `/iocs/{group}` | GET | Group IOCs (IP, MD5, email, BTC) |
| **Negotiations** | `/negotiations` | GET | Groups with negotiation logs |
| | `/negotiations/{group}` | GET | Chat metadata |
| | `/negotiations/{group}/{chat_id}` | GET | Full chat transcript + ransom |
| **Ransom Notes** | `/ransomnotes` | GET | Groups with ransom notes |
| | `/ransomnotes/{group}` | GET | Note file listing |
| | `/ransomnotes/{group}/{note}` | GET | Full ransom note content |
| **Press** | `/press/all` | GET | All press reports (filterable) |
| | `/press/recent` | GET | Latest 100 press reports |
| **YARA** | `/yara` | GET | Groups with YARA rules |
| | `/yara/{group}` | GET | YARA rule content |
| **CSIRT** | `/csirt/{country}` | GET | National CERT/CSIRT directory |
| **SEC** | `/8k` | GET | SEC 8-K cybersecurity filings |
| **System** | `/stats` | GET | Platform statistics |
| | `/validate` | GET | Validate API key |

**Base URL:** `https://api-pro.ransomware.live`

## Directory Structure

```
skills/ransomware-live/
├── SKILL.md                    # Skill definition (this file)
├── index.json                  # Machine-readable skill manifest
│
├── filings/                    # SEC 8-K filings
│   └── get_forms_8k.json
├── groups/                     # Ransomware group profiling
│   ├── get_group_list.json
│   └── get_group_detail.json
├── iocs/                       # Indicators of compromise
│   ├── get_ioc_group_list.json
│   └── get_group_iocs.json
├── negotiations/               # Ransom negotiation logs
│   ├── get_negotiation_groups.json
│   ├── get_negotiation_group_chats.json
│   └── get_negotiation_chat_detail.json
├── ransomnotes/                # Ransom note samples
│   ├── get_ransomnote_groups.json
│   ├── get_ransomnote_group_list.json
│   └── get_ransomnote_detail.json
├── press/                      # Media coverage
│   ├── get_press_list.json
│   └── get_press_recent.json
├── yara/                       # YARA detection rules
│   ├── get_yara_rules_list.json
│   └── get_yara_rules_detail.json
├── csirt/                      # CSIRT/CERT directory
│   └── get_csirt_by_country.json
├── victims/                    # Victim tracking
│   ├── get_victims_all.json
│   ├── get_recent_victims.json
│   ├── get_victim_search.json
│   └── get_single_victim.json
└── system/                     # System utilities
    ├── get_stats.json
    └── get_validate_key.json
```

## Skill File Format

Each `.json` skill file follows the OpenAI function calling schema:

```json
{
  "skill_id": "unique-identifier",
  "name": "function_name",
  "display_name": "Display Name",
  "description": "What this skill does",
  "category": "victims",
  "version": "1.0",
  "api": {
    "base_url": "https://api-pro.ransomware.live",
    "endpoint": "/victims/search",
    "method": "GET",
    "content_type": "application/json",
    "auth": {
      "type": "header",
      "key": "X-API-KEY"
    }
  },
  "parameters_map": {
    "query": { "type": "query", "required": false },
    "group": { "type": "query", "required": false },
    "country": { "type": "query", "required": false },
    "limit": { "type": "query", "required": false }
  },
  "function": {
    "name": "get_victim_search",
    "description": "Search ransomware victims by keyword, group, or country",
    "parameters": {
      "type": "object",
      "properties": { ... },
      "required": []
    }
  },
  "examples": [
    {
      "input": { "query": "bank", "limit": 10 },
      "description": "Search for banking-related victims"
    }
  ]
}
```

## Usage Examples

Once installed, interact with the skill through natural language in OpenClaw:

```
You: 查询 Akira 勒索组织最近的受害者
You: 搜索三月份中国的勒索事件
You: 获取 Qilin 组织的 IOC 信息
You: 查看最近的勒索软件谈判记录
You: 下载 LockBit 的勒索信样本
```

## Version

**Current:** v0.3  
**Endpoints:** 23  
**Categories:** 10  
**Tracked Groups:** 327+  
**Total Victims:** 26,000+

## License

MIT

## Credits

- API Provider: [Ransomware.live](https://www.ransomware.live)
- Skill Author: Ghost
- Platform: [OpenClaw](https://github.com/openclaw/openclaw)
