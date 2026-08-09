# 如何读取 Figma 本地变量（Local Variables）

> 写给未来会话的 AI / Claude：当用户提到"读取 Figma 本地变量"或类似需求时，**直接看这个文档**，不要走老路撞墙。
>
> 创建时间：2026-06-01 | 验证文件：[Shopee System Test](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test)

---

## 🔴 老路（会撞墙的方法）

**不要直接调用以下工具读变量值**：
- ❌ `mcp__bdc11575-a297-41db-81ab-6bbc657b60ab__get_variable_defs(nodeId)` — 会报错 `"You currently have nothing selected. You need to select a layer first before using this tool."`
- ❌ `mcp__bdc11575-a297-41db-81ab-6bbc657b60ab__get_design_context(nodeId)` — 同样报错
- ❌ `mcp__bdc11575-a297-41db-81ab-6bbc657b60ab__search_design_system(query)` — 只返回**已发布的库变量**（如 IDS UI-Kit），不返回本地变量

**原因**：这些工具要求用户在 Figma 桌面端**实际选中一个图层**才能工作。这是 Figma 官方的限制，Figma Forum 上有大量类似抱怨。Web 搜索 "Figma MCP local variables without selection" 可以确认。

---

## ✅ 正解：用 `use_figma` 执行 Plugin API

`use_figma` 工具能在 Figma 文件里执行任意 JavaScript（含 Figma Plugin API），可以直接调用 `figma.variables.getLocalVariablesAsync()` 一次性拿到**所有本地变量的精确值**。

**关键优势**：
- ✅ **不需要用户在 Figma 选中任何东西**
- ✅ **不算 API 配额**（Figma 官方文档明确写明 `use_figma` / write tools 豁免 rate limit）
- ✅ 一次拿到 hex 值 + 别名链 + Float 值 + Scope + 类型

---

## 📜 完整 Recipe — 读取所有本地变量

```javascript
// 调用前确保已加载 figma-use skill
// 工具调用：mcp__bdc11575-a297-41db-81ab-6bbc657b60ab__use_figma
// 参数：
//   - fileKey: 从 URL 提取（如 KTvcllui6OGgNPI5f1DfHe）
//   - skillNames: "figma-use"
//   - description: "读取所有本地Variables"
//   - code: 下方 JavaScript

const collections = await figma.variables.getLocalVariableCollectionsAsync();
const allVars = await figma.variables.getLocalVariablesAsync();

// Build ID -> variable lookup（用于解析别名）
const varById = {};
for (const v of allVars) varById[v.id] = v;

// Helper：把 {r,g,b,a} (0-1) 转成 hex 字符串
function toHex(c) {
  if (typeof c !== 'object' || c === null) return String(c);
  const r = Math.round((c.r ?? 0) * 255);
  const g = Math.round((c.g ?? 0) * 255);
  const b = Math.round((c.b ?? 0) * 255);
  const a = c.a ?? 1;
  const h = (n) => n.toString(16).padStart(2, '0').toUpperCase();
  const hex = `#${h(r)}${h(g)}${h(b)}`;
  return a < 1 ? `${hex} (a=${a.toFixed(2)})` : hex;
}

// Helper：格式化值（处理别名引用）
function formatValue(v, type) {
  if (v == null) return null;
  if (typeof v === 'object' && v.type === 'VARIABLE_ALIAS') {
    const alias = varById[v.id];
    return alias ? `→ ${alias.name}` : `→ unknown`;
  }
  if (type === 'COLOR') return toHex(v);
  return v; // FLOAT / STRING / BOOLEAN 直接返回
}

// Summary 信息
const summary = collections.map(c => ({
  name: c.name,
  id: c.id,
  modes: c.modes.map(m => ({ name: m.name, id: m.modeId })),
  variableCount: c.variableIds.length,
}));

// Variables 按 collection 分组
const variablesByCollection = {};
for (const v of allVars) {
  const coll = collections.find(c => c.id === v.variableCollectionId);
  const collName = coll ? coll.name : 'unknown';
  if (!variablesByCollection[collName]) variablesByCollection[collName] = [];
  const firstMode = coll && coll.modes[0];
  const rawVal = firstMode ? v.valuesByMode[firstMode.modeId] : null;
  variablesByCollection[collName].push({
    name: v.name,                    // 如 "Colors/Base/Orange/6"
    type: v.resolvedType,            // COLOR / FLOAT / STRING / BOOLEAN
    value: formatValue(rawVal, v.resolvedType),
    scopes: v.scopes,                // ["ALL_SCOPES"] or ["TEXT_FILL", "STROKE_COLOR"] etc.
  });
}

return { summary, variablesByCollection };
```

---

## ⚠️ 重要：输出大于 20KB 会被截断

如果一个文件有数百个变量（如 Shopee Tokens 有 473 个），返回值会超过 20KB 被自动截断。

**应对策略：分批调用**，每次按 name 前缀过滤：

```javascript
// 第二次调用：只取剩下部分
const allVars = await figma.variables.getLocalVariablesAsync();
// ... toHex / formatValue 定义同上 ...

// 只要特定前缀的
const prefixes = ['Border Radius', 'Size', 'Space', 'Typography'];
const result = {};
for (const v of allVars) {
  if (!prefixes.some(p => v.name.includes(p))) continue;
  const coll = (await figma.variables.getLocalVariableCollectionsAsync()).find(c => c.id === v.variableCollectionId);
  const val = formatValue(v.valuesByMode[coll.modes[0].modeId], v.resolvedType);
  result[v.name] = { type: v.resolvedType, value: val };
}
return result;
```

按经验：**最多 250 个变量/次** 能不被截断。Shopee Tokens 473 个建议分 2-3 批。

---

## 📐 数据格式速查

### Variable 对象关键字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `name` | string | 变量名（含分组路径，如 `Colors/Base/Orange/6`） |
| `resolvedType` | enum | `COLOR` / `FLOAT` / `STRING` / `BOOLEAN` |
| `valuesByMode` | object | `{[modeId]: value}` |
| `scopes` | string[] | `ALL_SCOPES` / `TEXT_FILL` / `STROKE_COLOR` / `FRAME_FILL` / `SHAPE_FILL` / `GAP` 等 |
| `variableCollectionId` | string | 所属 Collection ID |

### Color 值结构

```js
// 直接值
{r: 0.93, g: 0.30, b: 0.18, a: 1}  // 即 #EE4D2D
// → 转换：Math.round(r*255).toString(16) 拼起来

// 别名引用
{type: 'VARIABLE_ALIAS', id: 'VariableID:7:42'}
// → 用 varById[id] 解析为别名名称
```

### Mode 概念

- 一个 Collection 可以有多个 Mode（如 Light / Dark / 不同品牌）
- 每个变量值都按 mode 存储：`valuesByMode = {[modeId]: value}`
- Shopee Tokens 当前只有一个 Mode：`Light`（modeId `7:0`）

---

## 🔍 其他常用 Plugin API（按需调用）

```javascript
// 列出所有 Collections
const collections = await figma.variables.getLocalVariableCollectionsAsync();
// 返回：[{ name, id, modes: [{name, modeId}], variableIds: [...] }]

// 列出某个 Collection 下的变量
const vars = await figma.variables.getLocalVariablesAsync();
const inColl = vars.filter(v => v.variableCollectionId === 'COLL_ID');

// 创建新变量（写入，非读取）
const newVar = figma.variables.createVariable('newToken', collection, 'COLOR');
newVar.setValueForMode(modeId, { r: 1, g: 0, b: 0, a: 1 });

// 获取节点上绑定的变量
const node = await figma.getNodeByIdAsync('1:2');
const boundVars = node.boundVariables; // { fills: [{type: 'VARIABLE_ALIAS', id: 'xxx'}] }
```

---

## 📝 历史教训（避免重蹈覆辙）

**这次会话的撞墙过程**（2026-06-01）：

1. 用 `get_variable_defs` 报错"未选中"
2. 用 `get_design_context` 同样报错
3. 用 `search_design_system` 只能搜到 IDS UI-Kit 的库变量，搜不到本地的
4. 用 `get_metadata` 拿到 207K 字符的 XML 结构，但**不含 fill 的 hex 值**
5. 用 `get_screenshot` 渲染了 Token 页 PNG，能看但要肉眼读 473 个值
6. 走 web 搜索确认了官方 MCP 不支持，社区一直在 request feature
7. 最后用 `use_figma` 一次性 ✅ 拿到全部精确值

**结论**：以后遇到"读 Figma 本地变量/Styles/Components 内部数据"的需求，**第一选项就是 `use_figma` + Plugin API**，不要在其他工具上浪费时间。

---

## 🔗 参考链接

- [Figma Plugin API 文档（变量部分）](https://www.figma.com/plugin-docs/api/figma-variables/)
- [Figma MCP Tools 与 Rate Limits](https://developers.figma.com/docs/figma-mcp-server/rate-limits-access)
- [Figma Forum: get_variable_defs feature request](https://forum.figma.com/suggest-a-feature-11/figma-mcp-reading-variable-modes-42031)
