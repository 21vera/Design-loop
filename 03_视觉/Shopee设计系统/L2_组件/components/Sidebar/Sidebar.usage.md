# Sidebar 组件用法（AI 调用指南）

> 写给 AI 的"按这个调用就对了"说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注）：
> - **主**：旧 Shopee Guidelines [NG-Sidebar](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW?node-id=25-12592) — 3 类型 (基础 / 带层级 / 展开收起)
> - **架构 1:1 模板**：旧组件库 [Sidebar 4121:378](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4?node-id=4121-378) — Title Lv1 / Submenu-Lv2 / NormalMenu + SC侧边栏-全
> - **辅**：旧 Vue `Shopee前端组件源码/components/sidebar/` — EdsSidebar / EdsSidebarItem / EdsSidebarItemGroup
> - **架构参考**：[Ant Design Menu](https://www.figma.com/design/qjJSplS9q3tDVIXyhRPVvN?node-id=791-118) — 仅参考三层结构, 样式 NOT 抄
> - **新 Figma (三层)**：
>   - Layer 1: [Title 948:61](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=948-61) + [Submenu 948:74](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=948-74) + [Item 948:79](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=948-79) + [Rail Item 948:96](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=948-96)
>   - Layer 2: [Sidebar Group 949:85](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=949-85)
>   - Layer 3: [Sidebar 949:283](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=949-283)
> - **同步**: 2026-06-02 — 严格按旧库 1:1 (废弃 Ant-style 含 bg/indicator 的初版)

---

## 0. 依据来源映射（防越界）

| Prop / 子组件 | 来源 | Tier |
|---|---|---|
| `<Sidebar mode="grouped">` | 旧 Guidelines 带层级 + 旧 Vue EdsSidebar | T1 |
| `<Sidebar mode="flat">` | 旧 Guidelines 基础侧边栏 + 旧库 NormalMenu | T1 |
| `<Sidebar mode="collapsed">` | Ant inlineCollapsed | **T4** ⭐ 用户书面签字 |
| `<Sidebar.Group title icon>` | 旧库 SC侧边栏-全 (Order/Product/...) | T1 |
| `<Sidebar.Group dot>` | 旧库 Title Lv1 Dot=On | T2 |
| `<Sidebar.Group news>` | 旧库 Title Lv1 News=On | T2 |
| `<Sidebar.Group expanded>` | 旧 Guidelines 展开收起 + 旧 Vue (uncontrolled by default) | T1 |
| `<Sidebar.Submenu href selected>` | 旧库 Submenu-Lv2 Selected=On | T1 |
| `<Sidebar.Submenu news>` | 旧库 Submenu-Lv2 News=On | T2 |
| `<Sidebar.Item href selected>` | 旧库 NormalMenu Selected=On | T1 |
| `<Sidebar.RailItem icon>` | Ant inlineCollapsed | T4 用户签字 |
| Hover/Pressed (:hover/:active) | 现代 UX 标准 | T3 状态补齐 |
| Focus-Visible (:focus-visible) | a11y 现代标准 | T3 状态补齐 |

**砍掉的特性**（用户决定）：
- `theme` (light/dark) — 砍, 只 light
- bg 背景高亮 + 4px 左侧 indicator 条 — 砍 (旧库本就没有, 初版误抄 Ant)

---

## 1. 总览

- **组件名**：`Sidebar` (复合组件, 含 `.Group` / `.Title` / `.Submenu` / `.Item` / `.RailItem` 5 个子组件)
- **用途**：Seller Center 主导航 (左侧)
- **导入**：
  ```ts
  import {
    Sidebar,
    type SidebarProps,
    type SidebarMode,
  } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Sidebar` → Playground / Grouped / Flat / Collapsed / AllModes / AtomMatrix
- **Figma**：System Test → `Side Bar 侧边栏` 页

---

## 2. 决策树

**先决定 mode**:
- 多层路径 (Order > My Orders 等) → `mode="grouped"` (默认, 220 宽)
- 单层菜单 (Shop Profile / Decoration 等) → `mode="flat"` (176 宽)
- 全局收起态 (节省横向空间) → `mode="collapsed"` (80 宽, icon-only)

**Grouped mode 用法**：
- 每个一级菜单包成 `<Sidebar.Group title="Order" icon={<Icon name="order" />}>`
- 二级菜单项用 `<Sidebar.Submenu href="/orders">My Orders</Sidebar.Submenu>`
- 末位选中: 给 `selected` prop
- 红点: Group 加 `dot`
- NEW 徽标: Group 或 Submenu 加 `news`
- 默认 Group 展开, 用户点击 Title 切折叠 (uncontrolled)
- 想自己控制: 传 `expanded={state}` + `onTitleClick={() => setState(!state)}`

**Flat mode 用法**：
- 直接放 `<Sidebar.Item href selected>...</Sidebar.Item>`, 不嵌 Group

**Collapsed mode 用法**：
- 放 `<Sidebar.RailItem icon={<Icon name="x" />} aria-label="X" />`, 务必传 `aria-label`

---

## 3. Props 完整签名

### `<Sidebar>` (Layer 3 根)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `children` | `ReactNode` | — | Group / Item / RailItem 列表 (依 mode) |
| `mode` | `'grouped' \| 'flat' \| 'collapsed'` | `'grouped'` | 模式 |

### `<Sidebar.Group>` (Layer 2)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `title` | `ReactNode` | — | 一级标题文本 |
| `icon` | `ReactNode` | — | Title 左侧 icon (通常 `<Icon name="..." />`) |
| `dot` | `boolean` | `false` | 红点 (Dot=On) |
| `news` | `boolean` | `false` | NEW 徽标 (News=On) |
| `expanded` | `boolean` | uncontrolled, 默认 true | 是否展开. 不传 = 受组件内部 state 控制 |
| `onTitleClick` | `(e) => void` | — | 点击 Title 触发, 自定 expanded |
| `children` | `ReactNode` | — | Submenu 列表 (展开时显示) |

### `<Sidebar.Title>` (Layer 1, 一般通过 Group 间接用)
| Prop | 类型 | 说明 |
|---|---|---|
| `children` | `ReactNode` | 标题文本 |
| `icon` / `dot` / `news` / `expanded` | 同 Group | 直接渲染 Title |

### `<Sidebar.Submenu>` (Layer 1)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `children` | `ReactNode` | — | 文本 |
| `href` | `string` | — | 跳转 |
| `selected` | `boolean` | `false` | 当前页, 文字变橙, `aria-current="page"` |
| `news` | `boolean` | `false` | NEW 徽标 |

### `<Sidebar.Item>` (Layer 1, Flat mode)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `children` | `ReactNode` | — | 文本 |
| `href` | `string` | — | 跳转 |
| `selected` | `boolean` | `false` | 当前页, 文字变橙 |

### `<Sidebar.RailItem>` (Layer 1, Collapsed mode)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `icon` | `ReactNode` | — | 必填, 显示的 icon |
| `href` | `string` | — | 跳转 |
| `selected` | `boolean` | `false` | 当前页, icon 变橙 |
| `aria-label` | `string` | — | **必填**, 屏幕阅读器读 (无文字) |

---

## 4. 视觉规格速查

| 项 | 值 | Token |
|---|---|---|
| 字体 | Roboto | (写死) |
| Title 字号 | 14px Medium | `--Sidebar-titleFontSize` |
| Title 高度 | 32px | `--Sidebar-titleHeight` |
| Submenu/Item 字号 | 13px Regular (Selected→Medium) | `--Sidebar-submenuFontSize` |
| Submenu 高度 | 32px | `--Sidebar-submenuHeight` |
| Submenu 缩进 (左) | 40px | `--Sidebar-submenuIndent` |
| Item 高度 (flat) | 40px | `--Sidebar-itemHeight` |
| Group 间距 | 12px | `--Sidebar-groupGap` |
| 展开 sidebar 宽 | 220px | `--Sidebar-sidebarExpandedWidth` |
| 收起 sidebar 宽 | 80px | `--Sidebar-sidebarCollapsedWidth` |
| Title 文字色 | gray-7 (#999) | `--Sidebar-colorTitleText` |
| Submenu/Item 默认 | gray-8 | `--Sidebar-colorText` |
| Selected/Hover | orange (colorPrimary) | `--Sidebar-colorTextSelected` / `--Sidebar-colorTextHover` |
| Pressed | 深 orange | `--Sidebar-colorTextPressed` |
| 红点 | colorError (red) | `--Sidebar-colorDot` |
| NEW 徽标 bg | colorWarning (orange) | `--Sidebar-colorNewsBg` |
| Sidebar 背景 | 白 | `--Sidebar-colorBgSidebar` |
| 阴影 | 1px 0 4px rgba(0,0,0,0.08) | (写死) |

**注意**: 旧库无 hover/selected 背景高亮, 无 4px 左侧 indicator 条。Selected = 文字变橙 only。

---

## 5. Shopee 特有规则（提炼自旧 Guidelines）

1. **位置**: 通常在页面**左侧, 固定宽 220** (Grouped) / 176 (Flat) / 80 (Collapsed), 跟 Header 同行高度对齐
2. **主导航 = Sidebar; 辅助导航 = Breadcrumb**: 区分清楚 (旧 Guidelines 明确)
3. **Selected 仅文字变橙**: 没有底色高亮, 没有 indicator 条 (跟 Ant 不一样)
4. **Title 字号 14, Submenu 字号 13**: 一级比二级稍大
5. **红点 (Dot)**: 表示该组内有未读 / 待处理内容
6. **NEW 徽标**: 表示新功能上线
7. **长文本截断 + tooltip**: 最大宽度约 148px, 超出截断 (这一版用 CSS `text-overflow: ellipsis` 简单处理; 业务想加 tooltip 自己外包 `<Tooltip>`)

---

## 6. 场景示例

### 6.1 Seller Center 主导航 (Grouped mode)
```tsx
<Sidebar>
  <Sidebar.Group title="Order" icon={<Icon name="order" />} dot>
    <Sidebar.Submenu href="/orders" selected>My Orders</Sidebar.Submenu>
    <Sidebar.Submenu href="/cancel">Cancellation</Sidebar.Submenu>
    <Sidebar.Submenu href="/refund" news>Return / Refund</Sidebar.Submenu>
  </Sidebar.Group>
  <Sidebar.Group title="Product" icon={<Icon name="product" />}>
    <Sidebar.Submenu href="/products">My Product</Sidebar.Submenu>
    <Sidebar.Submenu href="/products/add" news>Add New Product</Sidebar.Submenu>
  </Sidebar.Group>
  <Sidebar.Group title="Finance" icon={<Icon name="wallet" />} expanded={false}>
    <Sidebar.Submenu href="/finance">My Income</Sidebar.Submenu>
  </Sidebar.Group>
</Sidebar>
```

### 6.2 单层菜单 (Flat mode)
```tsx
<Sidebar mode="flat">
  <Sidebar.Item href="/rating">Shop Rating</Sidebar.Item>
  <Sidebar.Item href="/profile" selected>Shop Profile</Sidebar.Item>
  <Sidebar.Item href="/decoration">Shop Decoration</Sidebar.Item>
</Sidebar>
```

### 6.3 收起态 (Collapsed mode)
```tsx
<Sidebar mode="collapsed">
  <Sidebar.RailItem href="/orders" icon={<Icon name="order" />} selected aria-label="Order" />
  <Sidebar.RailItem href="/products" icon={<Icon name="product" />} aria-label="Product" />
  <Sidebar.RailItem href="/marketing" icon={<Icon name="marketting" />} aria-label="Marketing" />
</Sidebar>
```

### 6.4 受控 Group 折叠 (业务自己控制)
```tsx
function ControlledSidebar() {
  const [openGroup, setOpenGroup] = useState<string | null>('order');
  return (
    <Sidebar>
      {['order', 'product', 'finance'].map(key => (
        <Sidebar.Group
          key={key}
          title={key}
          icon={<Icon name={key as any} />}
          expanded={openGroup === key}
          onTitleClick={() => setOpenGroup(openGroup === key ? null : key)}
        >
          <Sidebar.Submenu href={`/${key}`}>Item 1</Sidebar.Submenu>
        </Sidebar.Group>
      ))}
    </Sidebar>
  );
}
```

### 6.5 Mode 切换 (业务可在 Grouped ↔ Collapsed 切)
```tsx
const [collapsed, setCollapsed] = useState(false);
return collapsed
  ? <Sidebar mode="collapsed">{railItems}</Sidebar>
  : <Sidebar>{groupedItems}</Sidebar>;
```

---

## 7. 组合模式 (Sidebar × 其他组件)

- **Sidebar + Layout**: Sidebar 在 `<aside>` 里, content 在 `<main>` 里, 形成 Seller Center 经典 2 列布局
- **Sidebar + Header**: 通常 Sidebar 在 Header 下方 (Header 占顶, Sidebar 占左)
- **Sidebar + Breadcrumb**: Breadcrumb 在 content 顶部, 跟 Sidebar 配合使用 (Sidebar 是"我在哪个 section", Breadcrumb 是"我在哪一层")
- **Collapsed + Tooltip**: collapsed mode 下, hover RailItem 应弹 tooltip 显示 label (业务自己外包 `<Tooltip>`)

---

## 8. 反例

| ❌ 错误 | 原因 | ✅ 正确 |
|---|---|---|
| Selected item 加底色 / indicator 条 | 旧库无此设计 | 仅文字变橙 (selected prop) |
| `<Sidebar.Title>` 单独用 | Title 应该在 Group 里 | 用 `<Sidebar.Group title="..." />` |
| 在 mode="flat" 里放 `<Sidebar.Group>` | flat 是单层, 不嵌 group | 直接 `<Sidebar.Item />` |
| 在 mode="collapsed" 里放 `<Sidebar.Item>` 带文字 | collapsed 是 icon-only | 用 `<Sidebar.RailItem icon={...} />` |
| RailItem 不传 aria-label | 无文字, 屏幕阅读器无内容 | 必须 `aria-label="Order"` |
| 写中文 demo `<Sidebar.Submenu>我的订单</...>` | demo 一律英文 | `My Orders` |
| 用 svg 画 chevron | 违反铁律 #8 | 用 `<Icon name="arrow-down" />` |

---

## 9. a11y 要点

- 根元素 `<nav aria-label="Sidebar navigation">` — 屏幕阅读器读 "Sidebar navigation"
- Selected Submenu/Item: `aria-current="page"` 自动加
- Title `role="button" tabIndex={0}` — 可键盘聚焦, Enter/Space 切折叠 (UA 默认行为)
- Submenu/Item `<a>` — 自带键盘聚焦
- `:focus-visible` 2px controlOutline 描边 — 键盘聚焦可见
- RailItem `aria-label` 必填, 屏幕阅读器读

---

## 10. 与 Figma 对应

| Figma 节点 | React 组件 | 维度 |
|---|---|---|
| `Sidebar Title` (948:61) | `<Sidebar.Title>` (Group 内自动) | Dot × News = 4 |
| `Sidebar Submenu` (948:74) | `<Sidebar.Submenu>` | Selected × News = 4 |
| `Sidebar Item` (948:79) | `<Sidebar.Item>` | Selected = 2 |
| `Sidebar Rail Item` (948:96) | `<Sidebar.RailItem>` | Selected = 2 |
| `Sidebar Group` (949:85) | `<Sidebar.Group>` | Type = Expanded / Folded |
| `Sidebar` (949:283) | `<Sidebar>` | Mode = Grouped / Flat / Collapsed |

Code Connect 已写好 6 个映射 (`Sidebar.figma.tsx`)。
