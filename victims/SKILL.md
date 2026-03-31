# victims — 受害者

查询、搜索和浏览勒索软件受害者信息。数据来源于各勒索软件组织的"泄露站"（Leak Site）公开披露的受害者记录。

## 日期字段说明

| 字段 | 含义 |
|------|------|
| `discovered` | ransomware.live 首次发现该受害者的日期（默认） |
| `attacked` | 估计的实际攻击日期（可能不精确） |

---

## 推荐调用顺序

**场景一：按条件批量查询**
```
get_victims_all  →  按组织/行业/国家/时间筛选受害者列表
```

**场景二：搜索特定受害者**
```
get_victim_search  →  按关键词搜索，获取 victim_id
get_single_victim  →  用 victim_id 查询完整详情
```

**场景三：获取最新受害者**
```
get_recent_victims  →  获取最近 100 个受害者动态
```

---

## 技能列表

### `get_victims_all`
- **端点**：`GET /victims/`
- **说明**：按多种条件过滤受害者列表（至少提供一个参数）
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | query | 否 | 勒索软件组织名（例如：lockbit3） |
| `sector` | query | 否 | 行业（例如：healthcare、education、government） |
| `country` | query | 否 | 2位国家代码（例如：US、FR） |
| `year` | query | 否 | 4位年份（例如：2024） |
| `month` | query | 否 | 2位月份（例如：03） |
| `date` | query | 否 | 日期字段：`discovered`（默认）或 `attacked` |

**调用示例：**
```json
{ "group": "lockbit3" }
{ "country": "US", "sector": "healthcare", "year": "2024" }
{ "country": "FR", "year": "2024", "month": "03", "date": "attacked" }
```

---

### `get_recent_victims`
- **端点**：`GET /victims/recent`
- **说明**：返回最近 100 个受害者详情
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `order` | query | 否 | 排序方式：`discovered`（默认）或 `attacked` |

**调用示例：**
```json
{}
{ "order": "attacked" }
```

---

### `get_victim_search`
- **端点**：`GET /victims/search`
- **说明**：通过关键词在受害者名称（post_title）或网站（website）中搜索
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `q` | query | 否 | 搜索关键词 |
| `group` | query | 否 | 按组织名过滤 |
| `sector` | query | 否 | 按行业过滤 |
| `country` | query | 否 | 按国家代码过滤 |
| `order` | query | 否 | 排序方式：`discovered`（默认）或 `attacked` |

**调用示例：**
```json
{ "q": "hospital" }
{ "q": "bank", "group": "lockbit3" }
{ "sector": "healthcare", "country": "US", "order": "attacked" }
```

---

### `get_single_victim`
- **端点**：`GET /victim/{victim_id}`
- **说明**：通过 Base64 编码的 ID 查询单个受害者完整详情
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `victim_id` | path | 是 | Base64 编码的受害者 ID（原始格式：`post_title@group_name`） |

> **获取 victim_id**：通过 `get_victim_search` 或 `get_victims_all` 返回结果中获取，再进行 Base64 编码。

**调用示例：**
```json
{ "victim_id": "Q29tcGFueU5hbWVAbG9ja2JpdDM=" }
```
