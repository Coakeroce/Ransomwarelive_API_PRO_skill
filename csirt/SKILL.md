# csirt — CSIRT/CERT 机构

按国家查询计算机安全事件响应机构（CSIRT / CERT）的联系和资源信息。

- **CSIRT**（Computer Security Incident Response Team）：计算机安全事件响应小组
- **CERT**（Computer Emergency Response Team）：计算机应急响应小组

---

## 技能列表

### `get_csirt_by_country`
- **端点**：`GET /csirt/{country}`
- **说明**：根据 ISO 国家代码返回该国所有 CSIRT/CERT 条目
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `country` | path | 是 | ISO 国家代码，支持 Alpha-2（2位）或 Alpha-3（3位） |

**常用国家代码：**

| 国家 | Alpha-2 | Alpha-3 |
|------|---------|---------|
| 美国 | US | USA |
| 法国 | FR | FRA |
| 德国 | DE | DEU |
| 英国 | GB | GBR |
| 中国 | CN | CHN |
| 日本 | JP | JPN |
| 澳大利亚 | AU | AUS |

**调用示例：**
```json
{ "country": "FR" }
{ "country": "US" }
{ "country": "DEU" }
```
