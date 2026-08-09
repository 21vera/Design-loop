# Table 组件用法（AI 调用指南）

> 写给 AI 的"按这个在 Figma 里调用就对了"的说明书。
>
> **依据来源**：
> - **主**：System Test 里的 Table 组件（变体清晰、Token 完整）—— [Figma ComponentSet 1845:589](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1845-589)
> - **辅**：旧 Shopee Guidelines「DD-Table」7 类场景 + 旧 Vue `EdsTable`/`EdsTableColumn` props（仅提取仍适用的 Shopee 特有规则；旧分类不沿用）
> - **精确数值**：旧组件库 Figma `4131:744`（行高/字号/颜色/分割线全部从此扒取，非凭 SCSS 估算）
>
> 跨组件/页面级规则见 [../../../L3_全局规范/全局规范.md](../../../L3_全局规范/全局规范.md)。

## 1. 总览

- **Figma 组件名**：`Table`（与 Figma 图层名完全一致，PascalCase）
- **node-id**：`1845:589`（Table ComponentSet 根节点；MCP 用它定位）
- **用途**：在 Web 列表/管理页里**以行列结构展示结构化数据**，支持表头排序/提示、行复选、分页、固定列。一句话区分：要"展示并操作多条同结构记录"用 Table；只展示少量键值对用 `Card`；纵向罗列单列条目用 `Sidebar`/`Menu`。
- **变体维度**：`Type(Basic/FixedColumn) × Selectable(No/Yes)` = 4 变体
- **复合层级（3 层，改下层 master 上层自动同步）**：
  - L1 原子 `TableHeaderCell`（[1842:62](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1842-62)）+ `TableBodyCell`（[1842:76](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1842-76)）
  - L2 行 `TableRow`（[1843:138](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1843-138)）
  - L3 表 `Table`（1845:589）
- **依赖的基础组件**：`Checkbox`（850:34，行复选/全选）· `Pagination`（344:144，表尾分页）· `Icon`（排序 `arrow-updown-s`/`arrow-up-s`/`arrow-down-s`、提示 `question-mark`，均 16px）
- **Display**：`Table — Display`（1848:1066）· `TableCell — Display`（1848:1158）

## 2. 何时用 / 何时不用（When to use）

- ✅ 用 Table：商品列表、订单列表、配置项列表等**多行同结构数据**，需要表头、排序、批量选择、分页中的任意组合。
- ❌ 不要用 Table，改用别的：
  - 单条记录的字段展示 → 用 `Card`（Table 是为"多行"设计的）。
  - 列特别多、横向远超屏宽且无主次 → 优先精简列或用 `FixedColumn` 固定关键列，不要硬塞。
  - 仅 2–5 个并列选项的选择 → 用 `Radio`/`Checkbox` 组，不要做成单列表。

## 3. 决策树（AI 必读）

```
要展示多行同结构数据?
├─ 列总宽 ≤ 容器, 无需固定 → Table: Type=Basic
└─ 列多/横向滚动, 需固定操作列或首列 → Table: Type=FixedColumn   （Action 列右侧出现左阴影）
需要批量操作(批删/批改/全选)?
├─ 是 → Selectable=Yes   （首列出现 Checkbox 列, 宽 48, 居中; 全选放表头）
└─ 否 → Selectable=No    （无复选列）
某列要排序?
├─ 可排序未激活 → 该表头 cell Sort=Default   （灰 ⇅）
├─ 升序激活     → Sort=Asc                   （橙 ↑）
├─ 降序激活     → Sort=Desc                  （橙 ↓）
└─ 不可排序     → Sort=None                  （无图标）
某列表头要解释说明? → 该表头 cell Info=On     （? 提示图标, 配 Tooltip）
单元格内容类型?
├─ 纯文本/数字 → BodyCell Content=Text
├─ 行内操作链接(Edit/Delete) → Content=Link
├─ 行复选框 → Content=Selection
└─ 头像/多行/富文本 → Content=Custom
```

## 4. 变体属性契约（= Figma Component Properties，逐字对齐 Figma）

**Table（根，1845:589）**

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `Type` | Variant | `Basic` / `FixedColumn` | Basic | FixedColumn 时 Action 列左侧加阴影示意固定 |
| `Selectable` | Variant | `No` / `Yes` | No | Yes 显示首列复选 + 全选表头 |

**TableRow（行，1843:138）**

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `State` | Variant | `Header` / `Default` / `Hover` / `Selected` | Default | Header=表头灰底；Hover/Selected 为行级高亮（非 cell 级） |

**TableHeaderCell（表头单元格，1842:62）**

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `Type` | Variant | `Label` / `Selection` | Label | Selection=全选复选框（Sort/Info 固定为 None/Off） |
| `Sort` | Variant | `None` / `Default` / `Asc` / `Desc` | None | None 无图标；Default 灰 ⇅；Asc 橙 ↑；Desc 橙 ↓ |
| `Info` | Variant | `Off` / `On` | Off | On 显示 ? 提示图标 |

**TableBodyCell（数据单元格，1842:76）**

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `Content` | Variant | `Text` / `Link` / `Selection` / `Custom` | Text | Text=正文；Link=蓝色操作链接；Selection=复选框；Custom=多行/富内容 |

> **Align（左/右/中）不是变体，是布局 prop**：在拼表时由列容器的 `primaryAxisAlignItems`（MIN/CENTER/MAX）控制，避免变体翻倍。文本默认左对齐。

## 5. 视觉规格（全部引用 Token，不写死值）

| 维度 | 值 | Token |
|------|----|----|
| 表头行高 | 40 | `Components/Table/Component/headerHeight` |
| 数据行高 | 48（pad 16 上下 + 内容 16） | `cellPaddingY` ×2 + 内容 |
| 单元格水平内边距 | 16 | `Components/Table/Component/cellPaddingX` |
| 单元格间距 | 16 | `cellGap` |
| 表头顶部内边距 | 12 | `headerPaddingTop` |
| 容器圆角 | 4 | `borderRadius` |
| 复选列宽 | 48 | `selectionColWidth` |
| 操作列宽 | 120 | `actionColWidth` |
| 图标尺寸 | 16 | `iconSize` |
| 字号 / 行高 | 14 / 16 | `fontSize` / `lineHeight`（字体 Roboto Regular） |
| 容器底 / 边框 | 白 / #E5 | `Global/colorBg` / `colorBorder` |
| 表头底色 | #F6 | `colorHeaderBg` |
| 行分割线 | 黑·低透明 | `colorSplit` |
| 正文 / 表头文字 | #333 / #666 | `colorText` / `colorTextHeader` |
| 操作链接 | 蓝 | `colorLink` |
| 排序激活 | 橙 | `colorSortActive` |
| Hover 行底 / 选中行底 | 浅灰 / 浅橙 | `colorRowHover` / `colorRowSelected` |
| 图标常态色 | #999 | `colorIcon` |

## 6. Shopee 特有规则（来自旧 Guidelines，⭐ 高价值）

- **单元格文本超长 → 省略号截断 + hover 出 Tooltip**（旧 GP「常规表格」明确）；不要换行撑高行（Custom 列除外，可主动多行）。
- **分页器与表格右对齐**，放表尾独立区，右侧固定（旧 GP「分页加载表格」）。
- **固定列用阴影区分**：被固定的列在与滚动区交界处加左向阴影（本组件 FixedColumn 变体已内置），不是用粗边框。
- **排序激活用主题橙**，未激活用灰 ⇅；同一时刻通常只有一列处于激活排序。
- **全选放表头复选格**，行选放各行首格；选中行整行变浅橙底（行级，不是只染某格）。
- 旧 GP 7 类场景：常规 / 斑马纹 / 固定表头 / 分页加载 / 固定列 / 综合型 / 父子表格。**首版实现：常规 + 固定列 + 行复选**；斑马纹、固定表头(sticky)、综合型富内容靠 Custom cell 拼、父子树(expand-tree) 为后续迭代。

## 7. 组合模式

| 场景 | 本组件配置 | 配合组件（node-id） | 排布 |
|------|-----------|--------------------|------|
| 商品/订单列表页 | Type=Basic, Selectable=Yes | `Filter`(1500:164) + `Toolbar`(待建) + `Pagination`(344:144) | Filter 在上、表居中、分页右下 |
| 宽表/多列 | Type=FixedColumn | — | Action 列固定右，数据列横向滚动 |
| 行内操作 | BodyCell Content=Link | — | Edit/Delete 蓝链接，左对齐留 16 左边距避开固定阴影 |
| 批量操作 | Selectable=Yes | `Checkbox`(850:34) + `Toolbar` | 选中后 Toolbar 出批量按钮 |
| 富内容单元格 | BodyCell Content=Custom | `Avatar`(头像) / `Tag`(状态) | 在 Custom 槽内 instance，禁止裸画 |

## 8. 反例（AI 绝不能这样做）

| ❌ 错误 | ✅ 正确 | 原因 |
|---------|---------|------|
| 在 Table 里裸画矩形当行/单元格 | instance `TableRow` / cell 原子 | 裸图形改 Token 不同步，破坏 3 层联动 |
| 给 BodyCell 加 Hover/Selected 变体 | 状态放在 `TableRow.State` | hover/选中是**行级**高亮；cell 带状态会重复且不一致 |
| 自画排序/提示小箭头 SVG | instance `Icon` 库 `arrow-updown-s`/`question-mark` | 违反"不自创 icon"；自画的图标尺寸/色不受 Token 管控 |
| 复选格直接放完整 Checkbox（带 "Checkbox" 文案） | 隐藏 Checkbox 内文字标签，只留勾选框 | 表格复选列只需框；带标签会在 48px 列里截断 |
| 全列固定 px 宽不跟随容器 | 数据列 `layoutGrow/FILL` 均分，仅 Selection 48 / Action 120 固定 | Table 要随浏览器宽自适应（业务明确要求） |
| 固定列用粗黑边框表示 | 用左向阴影（FixedColumn 变体内置） | Shopee 规范用阴影区分固定区，边框语义错且突兀 |
| 文本超长直接换行撑高 | 省略号 + Tooltip | 保持行高一致；旧 GP 明确截断 |

## 9. Token 主题化

| 需求 | 改哪个 Token |
|------|-------------|
| 调整行高/密度 | `Components/Table/Component/cellPaddingY` |
| 改容器圆角 | `Components/Table/Component/borderRadius` |
| 改表头底色 | `Components/Table/Global/colorHeaderBg` |
| 改选中行底色 | `Components/Table/Global/colorRowSelected` |
| 改排序激活色 | `Components/Table/Global/colorSortActive` |
| 改操作链接色 | `Components/Table/Global/colorLink` |
| 调操作/复选列宽 | `actionColWidth` / `selectionColWidth` |

## 10.（选填）动效 / a11y

- 行 hover 过渡、排序点击翻转、固定列滚动阴影渐显等动效在业务侧实现，Figma 不画过渡帧。
- a11y：表头 `<th>` + `scope`，复选框带 aria-label，排序状态用 `aria-sort`（业务实现）。

## 文档维护历史
- 2026-06-21：首次导入完成。4 ComponentSet（TableHeaderCell 9 / TableBodyCell 4 / TableRow 4 / Table 4）+ 22 token（11 Component + 11 Global）+ 2 Display。严格按旧库 4131:744 数值；复用 Checkbox/Pagination/Icon；数据列均分自适应 + Action 固定列左阴影。
