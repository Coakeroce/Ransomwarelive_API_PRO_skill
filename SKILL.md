# Ransomware.live API Skills

基于 [Ransomware.live API PRO](https://www.ransomware.live/api) 构建的 AI Skills 集合，提供勒索软件威胁情报的全面查询能力。

## 认证方式

所有 API 请求需在 HTTP 请求头中携带 API Key：

```
X-API-KEY: <your-api-key>
```

> 免费申请 API Key：https://my.ransomware.live

---

## 目录结构

```
skills/
├── index.json              # 技能总览清单（机器可读）
├── README.md               # 本文件（人类可读）
│
├── filings/                # SEC 归档表单（1 个技能）
├── groups/                 # 勒索软件组织（2 个技能）
├── iocs/                   # 入侵指标 IOC（2 个技能）
├── negotiations/           # 谈判记录（3 个技能）
├── ransomnotes/            # 勒索信（3 个技能）
├── press/                  # 网络攻击新闻（2 个技能）
├── yara/                   # YARA 检测规则（2 个技能）
├── csirt/                  # CSIRT/CERT 机构（1 个技能）
├── victims/                # 受害者（4 个技能）
└── system/                 # 系统（2 个技能）
```

---

## 技能总览（共 23 个）

### 📁 filings — SEC 归档表单


| 技能名         | 端点      | 说明                            |
| -------------- | --------- | ------------------------------- |
| `get_forms_8k` | `GET /8k` | 查询网络安全事件相关的 8-K 表单 |

### 📁 groups — 勒索软件组织


| 技能名             | 端点                      | 说明                                     |
| ------------------ | ------------------------- | ---------------------------------------- |
| `get_group_list`   | `GET /groups`             | 获取所有已知勒索软件组织列表             |
| `get_group_detail` | `GET /groups/{groupname}` | 查询指定组织详情（TTPs、工具、受害者等） |

### 📁 iocs — 入侵指标


| 技能名               | 端点                | 说明                                        |
| -------------------- | ------------------- | ------------------------------------------- |
| `get_ioc_group_list` | `GET /iocs`         | 获取拥有 IOC 的组织列表                     |
| `get_group_iocs`     | `GET /iocs/{group}` | 获取指定组织的 IOC（IP、MD5、邮箱、BTC 等） |

### 📁 negotiations — 谈判记录


| 技能名                        | 端点                                  | 说明                           |
| ----------------------------- | ------------------------------------- | ------------------------------ |
| `get_negotiation_groups`      | `GET /negotiations`                   | 列出拥有谈判记录的组织         |
| `get_negotiation_group_chats` | `GET /negotiations/{group}`           | 获取组织谈判聊天元数据         |
| `get_negotiation_chat_detail` | `GET /negotiations/{group}/{chat_id}` | 获取具体谈判聊天全文及赎金信息 |

### 📁 ransomnotes — 勒索信


| 技能名                      | 端点                                   | 说明                       |
| --------------------------- | -------------------------------------- | -------------------------- |
| `get_ransomnote_groups`     | `GET /ransomnotes`                     | 列出拥有勒索信的组织       |
| `get_ransomnote_group_list` | `GET /ransomnotes/{group}`             | 获取组织的勒索信文件名列表 |
| `get_ransomnote_detail`     | `GET /ransomnotes/{group}/{note_name}` | 获取勒索信完整内容         |

### 📁 press — 网络攻击新闻


| 技能名             | 端点                | 说明                                       |
| ------------------ | ------------------- | ------------------------------------------ |
| `get_press_list`   | `GET /press/all`    | 获取所有网络攻击新闻（可按年/月/国家过滤） |
| `get_press_recent` | `GET /press/recent` | 获取最近 100 条网络攻击新闻                |

### 📁 yara — YARA 检测规则


| 技能名                  | 端点                | 说明                         |
| ----------------------- | ------------------- | ---------------------------- |
| `get_yara_rules_list`   | `GET /yara`         | 列出拥有 YARA 规则的组织     |
| `get_yara_rules_detail` | `GET /yara/{group}` | 获取指定组织的 YARA 规则内容 |

### 📁 csirt — CSIRT/CERT 机构


| 技能名                 | 端点                   | 说明                           |
| ---------------------- | ---------------------- | ------------------------------ |
| `get_csirt_by_country` | `GET /csirt/{country}` | 按国家代码查询 CSIRT/CERT 机构 |

### 📁 victims — 受害者


| 技能名               | 端点                      | 说明                            |
| -------------------- | ------------------------- | ------------------------------- |
| `get_victims_all`    | `GET /victims/`           | 按条件查询受害者列表            |
| `get_recent_victims` | `GET /victims/recent`     | 获取最近 100 个受害者           |
| `get_victim_search`  | `GET /victims/search`     | 关键词搜索受害者                |
| `get_single_victim`  | `GET /victim/{victim_id}` | 查询单个受害者详情（Base64 ID） |

### 📁 system — 系统


| 技能名             | 端点            | 说明                |
| ------------------ | --------------- | ------------------- |
| `get_stats`        | `GET /stats`    | 获取平台统计数据    |
| `get_validate_key` | `GET /validate` | 验证 API Key 有效性 |

---

## Skill 文件格式说明

每个 `.json` 技能文件包含以下字段：

```json
{
  "skill_id":     "全局唯一标识符",
  "name":         "函数名（snake_case）",
  "display_name": "中文展示名",
  "description":  "功能描述",
  "category":     "所属分类",
  "version":      "版本号",
  "api": {
    "base_url":     "API 基础地址",
    "endpoint":     "端点路径（含路径参数占位符）",
    "method":       "HTTP 方法",
    "content_type": "内容类型",
    "auth":         "认证配置"
  },
  "parameters_map": "参数位置映射（path/query 及是否必填）",
  "function":       "OpenAI function calling 标准格式定义",
  "examples":       "调用示例列表"
}
```
