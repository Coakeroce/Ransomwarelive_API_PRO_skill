# ransomnotes — 勒索信

查询和获取勒索软件组织的勒索信（Ransom Note）原文内容。勒索信是勒索软件在加密受害者文件后留下的通知文件，通常包含支付说明、联系方式和截止期限。

支持的文件格式：`.txt`、`.html`、`.md`

---

## 推荐调用顺序

```
1. get_ransomnote_groups        → 查看哪些组织有勒索信
2. get_ransomnote_group_list    → 获取某组织的勒索信文件名列表
3. get_ransomnote_detail        → 获取具体勒索信的完整内容
```

---

## 技能列表

### `get_ransomnote_groups`
- **端点**：`GET /ransomnotes`
- **说明**：列出所有拥有可用勒索信的组织及勒索信数量
- **参数**：无

**调用示例：**
```json
{}
```

---

### `get_ransomnote_group_list`
- **端点**：`GET /ransomnotes/{group}`
- **说明**：返回指定组织的所有勒索信文件名列表
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | path | 是 | 勒索软件组织名称（例如：lockbit） |

**调用示例：**
```json
{ "group": "lockbit" }
{ "group": "clop" }
```

---

### `get_ransomnote_detail`
- **端点**：`GET /ransomnotes/{group}/{note_name}`
- **说明**：返回指定勒索信文件的完整原文内容
- **参数**：

| 参数 | 位置 | 必填 | 说明 |
|------|------|------|------|
| `group` | path | 是 | 勒索软件组织名称 |
| `note_name` | path | 是 | 勒索信文件名，含扩展名（例如：README.txt） |

**调用示例：**
```json
{ "group": "lockbit", "note_name": "README.txt" }
```
