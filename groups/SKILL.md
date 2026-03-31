# groups — 勒索软件组织

查询已知勒索软件组织的档案信息，包括战术技术程序（TTPs）、使用工具、活跃周期和受害者统计。

---

## 技能列表

### `get_group_list`
- **端点**：`GET /groups`
- **说明**：返回所有已知勒索软件组织及其受害者数量
- **参数**：无

**调用示例：**
```json
{}
```

---

### `get_group_detail`
- **端点**：`GET /groups/{groupname}`
- **说明**：返回指定组织的完整档案，包括 TTPs、使用工具、活跃时间、受害者数量、勒索信和谈判记录
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `groupname` | path | 是 | 组织名称（例如：lockbit3、blackcat、clop） |

**调用示例：**
```json
{ "groupname": "lockbit3" }
{ "groupname": "blackcat" }
{ "groupname": "clop" }
```

> **提示**：组织名称使用小写，可先通过 `get_group_list` 获取完整的组织名称列表。
