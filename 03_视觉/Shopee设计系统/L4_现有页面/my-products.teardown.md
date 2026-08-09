# My Products 页拆解 → 组件需求 + 模板

## 参考边界

**可参考**：AppShell 与内容区关系、列表页骨架、已确认的组件与变体、信息密度和操作层级。

**不可直接照抄**：具体业务字段和顺序、页面历史问题、与当前需求或 L1–L3 冲突的做法、截图中的裸数值。无法确认的内容标记为待验证。

> 用真实线上 Seller Center「My Products」页反推：要还原到实战水准，需要哪些组件、用哪个变体、还缺什么。
> 这是"页面模板"层的第一份样本，目的是把决策文档的页面配方做到**指明确切变体**的颗粒度。
>
> 关键结论（探针实测各组件变体后）：**库的能力比首次出稿体现的强得多**。首次出稿差的主因是
> ①决策/配方层选错变体（用了 Filter 默认、Tabs 没用 DigitalTabs、没调 Alert、按钮全默认 Primary）
> ②没有整页骨架（缺 Sidebar + 页头操作区）。
>
> ⚠️ **2026-08-09 更新**：本文原结论「仍缺失 Toolbar / ResultBar」已过时。**Toolbar 已建成**（`e6d43de7fc80165583c9290d6243c9136f08d390`），library 中还有 `Seller Center / My Product (Full Page)` 整页模板可直接起手。**当前只剩 ResultBar 与通用 PageHeader 确无组件。**
>
> ⚠️ 本文原表中的 node-id 已有失效（Tabs、Table）。**引用组件一律用 componentKey**，见 [`../L2_组件/组件索引.md`](../L2_组件/组件索引.md)。

---

## 一 整页骨架（AppShell）

真实页面是一个"壳 + 正文"，不是一串控件：

```
AppShell
├─ GlobalTopBar   logo · 面包屑 · 右侧图标簇(下载/应用/指南/通知•/客服•) · 用户▾
├─ Sidebar        分组导航(Order/Product/Marketing/CS/Finance)，当前=My Products
└─ Content (灰底, 可滚动)
   ├─ PageHeader  「My Products」 + 右上: [Product Settings ▾•] [Mass Function ▾] [+ Add a New Product]
   ├─ Tabs        All · Live(109) · Violation(22) · Under Shopee Review(0) · Unpublished(75)
   ├─ Alert ×2    info 横幅(带链接 + 可关闭)
   └─ 白色内容卡
      ├─ FilterBar   Search · Category · Key Focus · [Apply] [Reset] · Expand▾
      ├─ ResultBar   「199 Products」+ Listing Limit 标签  |  Sort By Recommend · 列表/网格切换
      ├─ Table       表头(可排序) + 商品富行(缩略图+标题+SKU+标签 / Price / Stock / Performance / Smart Diagnosis / Action) + 可展开变体子行(View More 9 SKUs)
      └─ Pagination
```

---

## 二 逐区组件需求（含确切变体）

> 状态：✅ 直接可用（选对变体即可）｜🔧 需扩展变体｜🔴 需新建

| # | 区块 | 用什么组件 + **确切变体** | componentKey / node-id | 状态 |
|---|------|--------------------------|---------|------|
| 1 | 全局顶栏 | `Header` Type=**WithBreadcrumb** | node `1020:611` ✓ | 🔧 右侧图标簇比真实少（下载/应用/指南/通知/客服）——可扩展或接受简版 |
| 2 | 左侧导航 | `Sidebar` Mode=**Grouped**，填真实菜单 + 当前项高亮 | node `949:283` ✓ | ✅ 支持分组，只缺真实内容 |
| 3 | 页头标题 | 文本样式 **`Heading/l`**（20px · Medium · 28px 行高） | — | ✅ 用命名文本样式，不手拼字号 |
| 3 | 主操作按钮 | `Button` Type=Primary, Icon=Left, LeftIcon=`add` | node `104:4263` ✓ | ✅ |
| 3 | 下拉按钮 ▾ | `Button` Type=Default, RightIcon=`arrow-down-s`（即"Product Settings ▾"） | node `104:4263` ✓ | ✅ 用 RightIcon 即可，不必新建 |
| 3 | 按钮上红点 | `Badge` dot | node `874:19` ✓ | ✅ |
| 4 | Tabs(带计数) | `Tabs` Type=**DigitalTabs**, Count=5 | `340b4efce72697f5c3331798218cb0b489271bfc` | ✅ 支持计数；原 node `1241:675` 已失效 |
| 5 | 提示横幅 | `Alert` Status=**Info**, HasLink=Yes, HasClose=Yes | node `1430:94` ✓ | ✅ 本来就支持 |
| 6 | 筛选区 | `Filter` Mode=**Manual**, Count=3（插槽放 Search + Cascader[类目] + Dropdown[焦点]，Manual 自带 Apply/Reset） | `5c06c91e406437519ac1636b9c9aa4a08dd2238f` | ✅ 基本覆盖（首次用错成 Count=1） · 待核：插槽控件类型是否齐 |
| 6 | 搜索框 | `Search` Type=Simple（作 Filter 插槽） | node `1313:109` ✓ | ✅ |
| 6 | 类目选择 | `Cascader` | node `1307:178` ✓ | ✅ |
| 7 | 批量操作栏 | **`Toolbar`** | `e6d43de7fc80165583c9290d6243c9136f08d390` | ✅ **已建成**（本文原判断为缺失，已更正） |
| 7 | 结果计数栏 | ResultBar = 计数文本 + `Tag`(Listing Limit) + `Dropdown`(Sort) + 视图切换(图标按钮组) | — | 🔴 **仍缺**；按 L5 降级规则用 Toolbar + Text + Dropdown 组合并登记 |
| 8 | 数据表 | `Table`，按列配置复用现有基础组件 | `bbf7b147adbb2a6e3b794e4f732132c6bd0f950c` | ✅ 已建；原 node `1845:589` 已失效。原子层可用 `TableRow` / `TableHeaderCell` / `TableBodyCell` |
| 9 | 分页 | `Pagination` Mode=basic / combined | node `344:144` ✓ | ✅ |

---

## 三 Table 组合方式

真实表格远不止"网格"，按复合组件拆成多层：

```
Table
├─ TableHeader        列定义 + 可排序(↕) + 表头 ? tooltip
├─ TableRow (可勾选)
│  ├─ ProductCell     缩略图 + 标题 + Parent SKU + Item ID + Tag("Special Dimensions")   ← 领域分子, 新建
│  ├─ PriceCell       Rp500.000
│  ├─ StockCell       多行: "3k (Available 2.4k)" / Out Of Stock 徽标
│  ├─ PerformanceCell 多行: Sales 0 / L30D Sales 0 / L30D Impression 0
│  ├─ DiagnosisCell   状态行(图标 + 彩色文字 "Opportunity New Product") + 链接(Optimise/Check)
│  └─ ActionCell      Edit / Boost / More (Button Type=Link 或文本链接)
└─ 可展开变体子行 + "View More (N Products SKUs) ▾"
```

复用现有 Table 框架，并组合 Tag、Badge、Button(Link)、Icon、Avatar。若 ProductCell 在多个页面重复出现，再按组件库流程提议新增；单次页面不得先行自建。

---

## 四 建造清单（按优先级）

**🔴 P0 — 新建组件**（My Products 的硬缺口）
1. ~~Toolbar~~ —— **已于 2026-07-10 建成**，本条关闭。
2. **ResultBar**（计数 + Tag + Sort 下拉 + 视图切换）—— 小分子，仍缺，是列表页骨架唯一无法用组合完整替代的缺口。

**🟡 P0 — 改决策文档（不建组件，改配方）**
2. 维护 **My Products 精确配方**：每个区块指明“用哪个组件 + 哪个变体”（Tabs=DigitalTabs、Alert=Info+Link+Close、Filter=Manual Count=N、下拉按钮=Button+RightIcon），并要求覆盖默认占位、填真实英文业务数据。
3. 在决策文档保持 **AppShell / 整页模板** 这一层，规定“先搭壳（Sidebar + 顶栏）再填正文”。

**🟡 P1 — 封装"分子/模板"层**（介于组件和页面之间，提升生成可靠性）
4. PageHeader（标题 + 操作区）、FilterBar（Filter + 控件预设）、ResultBar。
   —— **AppShell 整页模板已存在**：library 中的 `Seller Center / My Product (Full Page)`（`32f7035e7b01dc623612e9f6e84c051904cd918c`）就是本页的整页模板，出稿应从它起手。
5. Header 右侧图标簇扩展（下载/应用/指南/通知/客服）——可选。

> ⚠️ 该整页模板的描述注明：banner 与商品表格是**从原设计直接复制**（无本地等价组件）、instance 已 detach、仅重新绑定了 Token。这两块**不是 library 组件**，不随 library 更新，也不能当作组件契约的依据。

**✅ 直接复用（选对变体即可）**
Sidebar(Grouped)、Tabs(DigitalTabs)、Alert(Info)、Filter(Manual)、Search、Cascader、Dropdown、Pagination、Button、Badge、Tag、Avatar。

---

## 五 给决策文档的启示（结构层面）

- 加一层 **页面模板 / 分子**：AI 从最接近的整页模板起手 + 改内容，比从原子组件拼可靠得多。
- 配方颗粒度要到 **"区块 → 组件 + 确切变体"**，不能停在"列表页=Header+Filter+Table"。
- 配方要带 **内容保真要求**（真实业务文案/数据，覆盖所有默认占位）。
- 组件 usage.md 要强调 **显式设全变体属性**（别吃默认）。
