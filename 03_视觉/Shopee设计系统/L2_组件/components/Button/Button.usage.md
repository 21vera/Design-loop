# Button 组件用法（AI 调用指南）

> 写给 AI（Claude 等）的"按这个在 Figma 里调用就对了"的说明书。**Figma-only 版**。
>
> **依据来源**：
> - **主**：System Test 里的 Button 组件（变体清晰、Token 完整）—— [Figma 节点 89:379](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=89-379)
> - **辅**：旧 Shopee Guidelines（仅提取仍适用的 Shopee 特有规则，如对齐方式、数量上限；分类体系不沿用）
>
> 跨组件/页面级规则见 [`../../../L3_全局规范/全局规范.md`](../../../L3_全局规范/全局规范.md)。
> 模板见 `AI操作手册/组件文档模板.md`（`_建设参考` 已于 2026-08-10 移出包，归档在包外 `Design-loop-归档/_建设参考/`）。

---

## 1. 总览

- **Figma 组件名**：`Button`
- **node-id**：`89:379`（ComponentSet 根节点）
- **用途**：触发任何用户操作——点击后立刻产生反馈（纯导航/跳转用 `Type=Link`）
- **变体维度**：`Type(5) × Size(3) × State(5)` = 75 变体；另含 `Danger` / `Loading` / `Ghost` / `Block` / `Icon` 等修饰属性
- **组成**：按钮容器 + Icon（可选，来自 Icon 库）+ 文字
- **依赖的基础组件**：`Icon`（[40:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=40-2)）

---

## 2. 何时用 / 何时不用

- ✅ 用 Button：任何**点击后立即产生反馈**的操作——提交、保存、确定、取消、删除、刷新、导出、批量操作、行内编辑等。
- ❌ 不要用 Button 做**纯页面跳转**（如导航到另一个页面/路由）——那是导航语义，用 `Type=Link`；大段可点文本也不要拿 Button 拼。
- ❌ 同一操作区按钮 > 3 个时，不要平铺——保留前 2–3 个，其余收进 `Dropdown`。

---

## 2.5 视觉强调级别（学 Ant：先讲清 Type 的语义）

| Type | 强调级别 | 什么时候用 |
|------|---------|-----------|
| `Primary` | 最高 | 区域主 CTA（完成/推荐动作）。**同区域最多 1 个** |
| `Outline` | 中 | 主操作的辅助（取消/返回/重置） |
| `Default` | 中低 | 普通中性操作（刷新/导出/筛选） |
| `Text` | 低 | 表格行内/卡片内的次级操作（编辑/删除/复制） |
| `Link` | 低 | 跳转/查看详情/查看更多 |

---

## 3. 决策树（AI 必读）

```
用户需要触发一个操作?
├─ 区域主 CTA（提交/保存/确定/创建/购买…）?
│    → Type=Primary           ⚠️ 同区域最多 1 个
├─ 主操作的辅助（取消/返回/重置…）?
│    → Type=Outline
├─ 普通中性操作（刷新/导出/筛选…）?
│    → Type=Default
├─ 表格行内 / 卡片内次级操作（编辑/删除/复制…）?
│    → Type=Text, Size=Small
└─ 跳转 / 查看详情 / 查看更多?
     → Type=Link

危险/破坏性操作（删除/下架…）?
└─ → Danger=true（叠加在任意 Type 上）  ⚠️ 必须包在二次确认弹窗里，不能独立直接执行

异步进行中?
└─ → Loading=true（自动禁用 + spinner）  ⚠️ 同区域最多 1 个 Loading

需要图标?
├─ 文字+图标 → Icon 实例 + 位置（默认 left）
├─ 仅图标（密集 UI 如表格行内）→ 只放 Icon，不填 Label  ⚠️ 必须有可访问名称（aria-label 语义）
└─ 仅文字 → 只填 Label

深色背景上?
└─ → Ghost=true（透明背景）

出静态设计稿时 State 一般用 Default；需要演示交互态时才切 Hover/Active/Focus/Disabled。
```

---

## 4. 变体属性契约（= Figma Component Properties）

> MCP 出稿时按此设属性。属性名/可选值与 Figma 组件**逐字一致**。

| 属性名 | 属性类型 | 可选值 | 默认 | 绑定 Token | 说明 |
|--------|---------|--------|------|-----------|------|
| `Type` | Variant | Primary / Outline / Default / Text / Link | Default | `Components/Button/*` | 视觉强调级别（见 §2.5） |
| `Size` | Variant | Small / Default / Large | Default | `Components/Button/Component/size*` | 高度 24 / 32 / 40px |
| `State` | Variant | Default / Hover / Active / Focus / Disabled | Default | — | 交互态；静态稿用 Default |
| `Danger` | Boolean | true / false | false | `…/colorError*` | 危险修饰，可叠加任意 Type |
| `Loading` | Boolean | true / false | false | — | 加载中（自动禁用 + spinner） |
| `Ghost` | Boolean | true / false | false | `…/defaultGhost*` | 透明背景，深色底上用 |
| `Block` | Boolean | true / false | false | — | 撑满父容器宽度 |
| `Icon` | Instance Swap | Icon 库任一图标 | — | — | **仅从 Icon 库选，禁止自创**；仅图标时不填 Label |
| `Label` | Text | 任意（demo 用英文） | "Button" | — | 按钮文字 |

---

## 5. 视觉规格（引用 Token，不写死）

| Size | 高度 | 水平内边距 | font-size | icon-size |
|------|------|----------|-----------|-----------|
| Small | 24px | 7px | 12px | 14px |
| Default | 32px | 15px | 14px | 16px |
| Large | 40px | 15px | 14px | 18px |

- **字重**：Medium (500) `--fontWeightStrong`　**字体**：Roboto
- **焦点环**：`--boxShadowFocusPrimary` = 内层白 2px + 外层 Shopee 橙 30% 4px

---

## 6. Shopee 特有规则（来自旧 Guidelines，⭐ 高价值）

### 6.1 按钮组的 4 种对齐

| 场景 | 对齐 | 原因 |
|------|-----|------|
| **表单** | 左对齐 | 视线 ↓ 跟随表单字段左边线 |
| **表格** | 右对齐 | 视线 ↘ 落在右下"自然落点" |
| **弹窗 / 卡片 / 消息** | 居中或右对齐 | 视线聚焦中间 |
| **卡片右上角单独按钮** | 右上对齐 | 作为隐藏式入口，不干扰主内容 |

### 6.2 数量上限

- 同区域最多 **1 个 Primary**（焦点唯一）
- 同区域最多 **1 个 Loading**
- 同区域最多 **3 个按钮**，超出用 Dropdown 折叠

### 6.3 危险操作流程（两步）

1. 入口：`Type=Outline, Danger=true` 触发二次确认弹窗
2. 确认：弹窗里 `Type=Primary, Danger=true` 才真正执行
理由：破坏性操作必须有撤回机会。

---

## 7. 组合模式

| 场景 | Button 配置 | 配合组件 | 排布 |
|------|------------|---------|------|
| 表单提交 | Primary（+ Outline 取消） | Form / Input | 左对齐 |
| 表格批量操作 | Outline + Primary | Table | 右对齐 |
| 弹窗底部 | Outline(取消) + Primary(确定) | Modal / Drawer | 居中或右对齐 |
| 卡片右上角 | Text, Size=Small, 仅 Icon | Card | 右上对齐 |
| 表格行操作 | 多个 Text, Size=Small | Table | 右对齐 |
| 危险确认 | Outline+Danger → 弹窗内 Primary+Danger | Modal | — |
| 操作 >3 个 | 前 2–3 个 + 其余折叠 | Dropdown | — |

---

## 8. 反例（AI 绝不能这样做）

| ❌ 错误 | ✅ 正确 | 原因 |
|---------|---------|------|
| 一个区域 2+ 个 `Type=Primary` | 只留最重要的 1 个 | 视觉焦点必须唯一 |
| 同区域多个 `Loading=true` | 最多 1 个 | 用户搞不清哪个在转 |
| 4+ 个按钮平铺一行 | 前 2–3 个 + Dropdown 折叠 | 按钮过多影响视觉 |
| 表单按钮右对齐 | 表单左对齐 | 视线 ↓ 跟随字段 |
| 表格按钮左对齐 | 表格右对齐 | 视线 ↘ 落右下 |
| 危险按钮直接执行 | 套二次确认弹窗 | 破坏性操作必须可撤回 |
| 纯跳转用普通 Button | `Type=Link` | 导航与操作语义不同 |
| 仅图标按钮没有可访问名称 | 补 aria-label 语义 | 屏幕阅读器无法识别 |
| 自己画/贴一个新图标 | 从 Icon 库选；缺则先入库 | 维持图标库单一来源 |
| 用纯色块覆盖按钮颜色 | 改 `Components/Button/*` Token | 破坏 Token 体系 |
| `Size=Large` 做表格行内按钮 | `Size=Small` 或 `Type=Text` | 视觉比例失衡 |

---

## 9. Token 主题化

| 需求 | 改哪个 Token |
|------|-------------|
| 提升整体圆角 | `Components/Button/Global/borderRadius` |
| 主按钮换金色（促销） | `Components/Button/Global/colorPrimary` |
| 文字加粗 | `Components/Button/Global/fontWeight` |
| 加大默认 padding | `Components/Button/Component/paddingInline` |
| ghost 自定义边框 | `Components/Button/Component/defaultGhostBorderColor` |

修改路径：**在 Figma 改 `Components/Button/*` Token（SSoT）** → 用 `use_figma` 拉取核对（Figma 本地变量为单一真源，无需另维护镜像表）。

---

## 10. 动效 / a11y（Phase 1 可略）

- 焦点环：`--boxShadowFocusPrimary`，Tab 导航清晰可见
- 仅图标按钮必须有可访问名称；Loading 态语义上等同 `aria-busy`
- 各 Type 文字/背景对比度由 Token 保证通过 WCAG AA

---

## 文档维护历史

- 2026-06-01 v1–v3：代码版（基于 React props）
- 2026-06-18 v4：**Figma-only 改写**——props 表 → 变体属性契约（Type/Size/State + Danger/Loading/Ghost/Block/Icon/Label），场景示例改为 Figma 变体设置；决策逻辑、Shopee 规则、反例保留。作为新模板的黄金示例。
