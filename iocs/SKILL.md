# iocs — 入侵指标 (Indicators of Compromise)

查询勒索软件组织的入侵指标（IOC），用于威胁检测、网络防御和安全工具集成。

## 支持的 IOC 类型

| 类型 | 说明 |
|------|------|
| `ip` | IP 地址 |
| `domain` | 域名 |
| `url` | URL 链接 |
| `md5` | MD5 哈希值 |
| `sha1` | SHA-1 哈希值 |
| `sha256` | SHA-256 哈希值 |
| `email` | 电子邮件地址 |
| `btc` | 比特币钱包地址 |

> **注意**：IOC 接口无速率限制，但请合理使用。

---

## 技能列表

### `get_ioc_group_list`
- **端点**：`GET /iocs`
- **说明**：返回所有拥有 IOC 的勒索软件组织列表，以及各组织的 IOC 类型和数量
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `type` | query | 否 | 按 IOC 类型过滤（例如：ip、md5、btc） |

**调用示例：**
```json
{}
{ "type": "btc" }
{ "type": "ip" }
```

---

### `get_group_iocs`
- **端点**：`GET /iocs/{group}`
- **说明**：返回指定组织的所有 IOC，可按类型过滤
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | path | 是 | 勒索软件组织名称（例如：lockbit3） |
| `type` | query | 否 | IOC 类型过滤（例如：ip、md5、email） |

**调用示例：**
```json
{ "group": "lockbit3" }
{ "group": "lockbit3", "type": "ip" }
{ "group": "clop", "type": "md5" }
```
