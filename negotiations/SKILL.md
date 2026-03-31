# negotiations — 谈判记录

查询勒索软件受害者与攻击者之间的真实谈判聊天记录，包括赎金要求、讨价还价过程和最终支付金额。

这些数据来源于泄露的谈判日志，对于研究勒索软件攻击模式、赎金定价策略和攻击者行为具有重要价值。

---

## 推荐调用顺序

```
1. get_negotiation_groups          → 查看哪些组织有谈判记录
2. get_negotiation_group_chats     → 获取某组织的聊天记录列表（含 chat_id）
3. get_negotiation_chat_detail     → 获取某次谈判的完整对话内容
```

---

## 技能列表

### `get_negotiation_groups`
- **端点**：`GET /negotiations`
- **说明**：列出所有拥有谈判聊天记录的组织及聊天数量
- **参数**：无

**调用示例：**
```json
{}
```

---

### `get_negotiation_group_chats`
- **端点**：`GET /negotiations/{group}`
- **说明**：返回指定组织所有谈判聊天的元数据（ID、日期等）
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | path | 是 | 勒索软件组织名称（例如：lockbit） |

**调用示例：**
```json
{ "group": "lockbit" }
```

---

### `get_negotiation_chat_detail`
- **端点**：`GET /negotiations/{group}/{chat_id}`
- **说明**：返回某次谈判的所有消息内容，以及初始赎金、谈判金额、实际支付金额
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | path | 是 | 勒索软件组织名称 |
| `chat_id` | path | 是 | 聊天 ID（不含扩展名，例如：20240517） |

**调用示例：**
```json
{ "group": "lockbit", "chat_id": "20240517" }
```
