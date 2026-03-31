# yara — YARA 检测规则

获取针对特定勒索软件家族的 YARA 规则，可直接集成到安全扫描工具（如 YARA、VirusTotal、ClamAV 等）中用于恶意软件检测和分类。

---

## 技能列表

### `get_yara_rules_list`
- **端点**：`GET /yara`
- **说明**：列出所有拥有关联 YARA 规则文件的勒索软件组织
- **参数**：无

**调用示例：**
```json
{}
```

---

### `get_yara_rules_detail`
- **端点**：`GET /yara/{group}`
- **说明**：返回指定组织的 YARA 规则文件内容，可直接用于安全工具
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | path | 是 | 勒索软件组织名称（例如：lockbit） |

**调用示例：**
```json
{ "group": "lockbit" }
{ "group": "conti" }
{ "group": "blackcat" }
```

> **提示**：返回的 YARA 规则可直接保存为 `.yar` 文件后使用 `yara` 命令行工具进行扫描。
