# Shopee 组件导入流程

> **范围：Figma-only**。当前阶段只在 Figma 中搭建完整组件库，AI 通过 Figma MCP 直接出稿对设计师提效；前端 React / Storybook / Code Connect 暂缓，待 Figma 库成熟后再评估。
>
> 📖 **本文是「概览/计划」**（背景、产出物、Token 结构、命名、里程碑）。**AI 实际导入组件时逐步照做的 SOP** 在 👉 [`AI操作手册/导入新组件的完整流程.md`](./导入新组件的完整流程.md)（含 6 阶段 + 十六条铁律 + Display 排版规范）。**两份配合使用，缺一不可。**
>
> Notion 原文档：https://www.notion.so/372b09d5573780f39b17eb9decc825af

---

# 一 背景

Shopee 的 Seller Center 业务逐渐成熟，很多组件和业务场景已经沉淀。我们计划把 Shopee 原本的组件库打包成 AI 能读懂的组件库，再利用 AI 直接调用，在 Figma 中生成设计稿。

## 1.1 产出物

**产物1：Figma 组件使用文档（`*.usage.md`）** ⭐
- 每组件一份 Markdown，指导 AI **在 Figma 里调用组件**——用哪个组件、设哪个变体属性、怎么和其他组件拼。
- 来源：旧版「Seller Center Guidelines」+ Figma 库真实实现；模板见 `AI操作手册/组件文档模板.md`，黄金示例 `Button.usage.md`。

**产物2：Figma 设计组件库.fig** ⭐
- Figma 设计文件（**Seller Center Library（For AI）**，正式库），作为 AI 出稿的素材库——MCP 直接读取调用。
- 来源：旧版「Enterprise Library」，在 Figma 中重建（三级 Token + ComponentSet 变体）。

> 产物1 + 产物2 并行产出、互相配套，即可支撑「AI 在 Figma 出稿」这一核心目标。AI 出稿时：读产物1 决策 → 通过 MCP 调产物2 出图。
>
> （前端 React 组件库为后续可选产物，当前暂缓。）

## 1.2 可参考的素材

| 素材 | 说明 | 地址 |
|------|------|------|
| Shopee 旧设计规范 | 描述组件使用场景；部分组件有多版本/与旧库不一致，需确认终版 | [New-Enterprise-Guideline](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/🚧-New-Enterprise-Guideline?node-id=13-18) |
| Shopee 旧组件库 | 存放组件的 Figma 文件（视觉真实源） | [Main-Enterprise-Library](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/-Main--Enterprise-Library?node-id=4131-122) |
| Ant Design Figma 组件库 | 参考文件，有完整 Design Token 结构 + 命名 | [Ant-Design-System](https://www.figma.com/design/qjJSplS9q3tDVIXyhRPVvN/Ant-Design-System?node-id=783-2068) |
| Seller Center Library（For AI）⭐ | **正式组件库**（Design Token + 组件）；AI 出稿的目标文件，MCP 直接读取 | [Seller-Center-Library](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/Seller-Center-Library?node-id=1-3) |
| Shopee 旧前端组件库 | Vue 2.0 源码，仅作扒精确数值参考，不迁移 | 本地 `Shopee前端组件源码/` |

## 1.3 范围约束

- **主题**：仅 light 模式 ｜ **响应式**：仅 desktop（考虑浏览器宽度自适应，不做 mobile/tablet）
- **多语言**：组件库仅 EN（业务层多语言不在范围）｜ **a11y**：当前阶段不考虑
- **浏览器**：Chrome / Edge / Safari / Firefox 最新 2 个版本

---

# 二 搭建 Figma 组件库

## 2.1 三级 Design Token 结构

参考 Ant Design，构建三级 Token：

- **原子 Token（第一级）**：设计时能用到的素材（颜色、间距、圆角等）。设计之初确定。
- **语义 Token（第二级）**：引用原子 Token，描述用在什么地方。尽量详尽建立，遗漏处参考 Ant 补全。
- **组件 Token（第三级）**：引用语义 Token，绑定到具体组件。随组件构建逐步补全。

> Shopee 旧库 Token 现状：原子层未建；语义层用 Style 建了部分但不在本地变量、覆盖不全；组件层未建、颜色绑定随意。Token 统一放 Figma 本地变量、作为单一真源（SSoT），展示形式 follow Ant Design。AI/设计师直接从 Figma 读取，无需另维护镜像表。

## 2.2 组件构建顺序

优先「基础组件」→ 高频「复合组件」→「页面组件」：

- **基础组件**：Button、Input 等不可再拆分的组件。有这些后 AI 才能拼装。
- **复合组件**：Filter、Table 等由基础组件拼接的集合，优先做高频的。
- **页面组件**：Homepage、Order List 等高频页面，减少设计师重复调用。

> 进度追踪：`组件清单.xlsx`。

## 2.3 单组件导入流程

单个组件「从理解到完成」的完整分阶段 SOP（Phase 1 理解 → 2 分析 → 2.5 Scope 契约 → 3 Token → 4 Figma 组件 + Display → 收尾文档），以及十六条铁律、Display 排版统一规范，全部见：

➡️ **[`AI操作手册/导入新组件的完整流程.md`](./导入新组件的完整流程.md)**（AI 导入新组件时必读，本文不重复）

收尾两件事：更新 `组件清单.xlsx` 状态、AI 试调用验证 `*.usage.md` 可用。（新增的 `Components/{X}/*` Token 直接建在 Figma 本地变量里即可，Figma 为单一真源。）

## 2.4 命名规范（全部英文，参考 Ant Design）

| 对象 | 命名风格 | 示例 |
|------|---------|------|
| Figma 组件名 | PascalCase | `Button`, `DatePicker`, `NumberInput` |
| Figma 变体属性名 / 值 | PascalCase | `Type`, `Size`, `State` / `Primary`, `Small` |
| 原子 Token | 描述性、kebab-case | `blue-6`, `spacing-md`, `radius-lg` |
| 语义 Token | camelCase、场景化 | `colorPrimary`, `colorTextSecondary`, `colorBgContainer` |
| 组件 Token | 组件名/属性 | `Components/Button/colorPrimary` |
| 使用文档文件名 | `{Component}.usage.md` | `Button.usage.md` |

## 2.5 组件分类判定标准

| 分类 | 判定标准 | 例子 |
|------|---------|------|
| **基础组件** | 不依赖其他业务组件，仅由原生 HTML + Token 构成 | Button, Input, Icon, Tag, Checkbox |
| **复合组件** | 至少引用 1 个基础组件 | Form, Filter, Table, Pagination, Steps |
| **页面组件** | 完整业务场景，可直接代入页面 | Homepage, Order List, Ads Dashboard |

---

# 三 完善组件库

- **审核**：人工 + AI 审核每个 ComponentSet——变体是否穷举（Type×Size×State 等）、是否全部绑定 Token、是否复用基础组件、`*.usage.md` 是否与 Figma 实现一致。
- **成品页面**：组件库基本完成后，在 Figma 里搭好完整界面（页面组件），方便设计师直接调用。

---

# 四 里程碑计划

> 一人负责的最小可行路径（MVP）。**原则**：先跑通 1 个组件的全链路，再扩展到全部组件。
>
> 📌 进度现状（2026-06-23，以正式库 Seller Center Library / For AI 为准）：Token 体系已基本完成；**25/49 组件已建（51%）**。进行中 3 个（Form、DatePicker、Tooltip）；未开始 21 个（Anchor、Steps、Table、Popover、Upload、Image、Slider、Rate、Timeline、Tree、Chart、Progress、Spin、Skeleton + 公共模组等）。实时进度见 `组件清单.xlsx`「进度统计」。
>
> （注：Table / Popover / Steps 已在 System Test 文件建好，尚未并入正式库。）

| 阶段 | 内容 |
|------|------|
| **Phase 1 地基** | 原子/语义 Token 清单 → Figma 建变量 → 可视化展示 |
| **Phase 2 试点** ⭐ | Button 端到端跑通（Figma 组件 + Token + usage.md + AI 试调用），验证 Figma-only 工作流 |
| **Phase 3 基础组件** | Input/Select/Checkbox/Radio/Switch、Card/Modal/Toast/Tooltip/Popover、Icon/Tag/Badge/Avatar/Spin |
| **Phase 4 复合组件** | Form/Table/Pagination、Filter/Steps/Tabs/Dropdown/Cascader |
| **Phase 5 页面组件** | Order List、Product Management、Ads Dashboard 等高频页面 |
| **Phase 6 审核 + 内测** | Figma 全量审核 + usage.md 校对 + 1-2 团队试用收集反馈 |

**风险与对策**：战线长易搁置 → 严格按 Phase 顺序、Phase 2 跑通前不扩展；Token 缺漏返工 → 用 Ant Design 兜底；usage.md 与 Figma 不一致 → 变体属性契约逐字对齐、写完 MCP 试调用验证；旧规范多版本 → 冲突以旧组件库实际值为准。

---

# 附录：配套文件

| 文件 | 用途 |
|------|------|
| `Shopee组件导入流程.md` | 本文件，整体流程与计划 |
| `组件清单.xlsx` | 组件清单、分类、优先级、状态、进度统计 |
| `AI操作手册/导入新组件的完整流程.md` | 单组件导入全链路 SOP（十六条铁律 + 6 阶段 + Display 规范） |
| `AI操作手册/组件文档模板.md` | Figma 版 `*.usage.md` 模板 |
| `figma-library/` | 组件使用文档（`*.usage.md`）+ 图标/插画 svg 资产 |
| `Shopee前端组件源码/` | 旧 Vue 2.0 组件库，仅作扒值参考，不迁移 |
