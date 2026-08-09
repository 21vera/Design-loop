# Breadcrumb 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注）：
> - **主**：旧 Shopee Guidelines [GP-Breadcrumb](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW?node-id=25-9246)
> - **辅**：旧 Vue `Shopee前端组件源码/components/breadcrumb/`
> - **架构参考**：[Ant Design Breadcrumb](https://www.figma.com/design/qjJSplS9q3tDVIXyhRPVvN?node-id=791-116) — 双层 ComponentSet
> - **新 Figma (双层)**：
>   - Layer 1: [Link 924:21](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=924-21) + [Separator 925:14](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=925-14) + [Ellipsis 925:21](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=925-21)
>   - Layer 2: [Breadcrumb 926:50](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=926-50)
> - **同步**: 2026-06-02 — 按更新后流程铁律 #8 重做, 双层模式 (废弃旧"4 链整体复刻")

---

## 0. 依据来源映射（防越界）

| Prop / 子组件 | 来源 | 证据 |
|---|---|---|
| `Breadcrumb.children` (Item 列表) | ✅ Tier 1 | 旧 Vue routes[] + 旧 Guidelines |
| `Breadcrumb.separator` | ✅ Tier 2 | 旧 Vue `separator` + `separatorIcon`, 默认 `<Icon name="arrow-right" />` |
| `Breadcrumb.maxItems` | ✅ Tier 2 | 旧 Vue `maxNode` (默认 4) |
| `Breadcrumb.itemsAfterCollapse` | ✅ Tier 2 | 旧 Vue `mustDisplayNum` |
| `Breadcrumb.Item.children` | ✅ Tier 1 | 文本内容 |
| `Breadcrumb.Item.href` | ✅ Tier 2 | 旧 Vue routes[i].path |
| `Breadcrumb.Item.current` | ✅ Tier 1 | 末位自动判定, 显式覆盖兜底 |
| `Breadcrumb.Item` :hover | ✅ Tier 1 | 旧 Guidelines + 旧 Vue `&:hover` |
| `Breadcrumb.Item` :active (Pressed) | ⚠️ Tier 3 状态补齐 | 旧版没画, 现代 UX 标准 |
| `Breadcrumb.Item` :focus-visible | ⚠️ Tier 3 状态补齐 | 旧版没画, a11y 键盘焦点 |
| `Breadcrumb.Separator` | ✅ Tier 1 | 旧 Guidelines arrow-right icon |
| `Breadcrumb.Ellipsis` | ✅ Tier 1 | 旧 Guidelines 多层级面包屑 ··· 元素 (Default/Hover/Expanded) |

**无 Tier 4**。所有特性都有旧规范 / 旧 Vue / a11y 补齐依据。

**双层 Compound Component 架构**（与 Figma 一一对应）：
- React Layer 1: `<Breadcrumb.Item>` / `<Breadcrumb.Separator>` / `<Breadcrumb.Ellipsis>` — Figma Layer 1 三个独立 ComponentSet
- React Layer 2: `<Breadcrumb>` — Figma Layer 2 的 Breadcrumb ComponentSet, 内部 100% 用 Layer 1 instance 拼

**砍掉的 prop**（用户决定）：
- `theme` (light/dark) — 砍, 只做 light
- `Icon × Label` 二维 — Cell 只做 Label 一维, icon 走 children slot

---

## 1. 总览

- **组件名**：`Breadcrumb` (复合组件, 含 `.Item` / `.Separator` / `.Ellipsis` 子组件)
- **用途**：层级导航, 显示当前页所在路径; 支持长路径自动折叠
- **导入**：
  ```ts
  import {
    Breadcrumb,
    type BreadcrumbProps,
    type BreadcrumbItemProps,
  } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Breadcrumb` → Playground / Basic / WithEllipsis / CustomSeparator / WithIcon / LinkStateMatrix / SellerCenterScenario
- **Figma**：System Test → `Breadcrumb 面包屑` 页

---

## 2. 决策树

**先决定**：要不要折叠？
- 层级 **≤ 4** → 不传 `maxItems`, 全部展示
- 层级 **> 4** → 传 `maxItems={4}`, 自动折叠 (旧 Guidelines 推荐)

**再决定**：分隔符要哪个？
- 默认 (Shopee 风格) → 不传 `separator`, 自动 `<Icon name="arrow-right" />`
- 文字 → `separator="/"`
- 其他 icon → `separator={<Icon name="arrow-down-s" />}`

**末位 Item**：不要手动写 `current`, 让 Breadcrumb 自动判定（最后一项 = current）。

**示例决策**：
| 用户场景 | 写法 |
|---|---|
| 普通页头 3-4 层导航 | `<Breadcrumb><Item href/>...<Item/></Breadcrumb>` |
| 深路径 (>4 层) | `<Breadcrumb maxItems={4}>...</Breadcrumb>` |
| 自定义 separator | `<Breadcrumb separator="/">...</Breadcrumb>` |
| 业务想自己控制省略号 (挂自己的 dropdown) | 手动放 `<Breadcrumb.Ellipsis onClick={...} />` |

---

## 3. Props 完整签名

### `<Breadcrumb>` (Layer 2 根)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `children` | `ReactNode` | — | 通常是 `Breadcrumb.Item` 列表 |
| `separator` | `ReactNode` | `<Icon name="arrow-right" />` | 分隔符, 自动插在每两个 Item 之间 |
| `maxItems` | `number` | `0` (不折叠) | 超过则折叠成 `Home > ··· > 最后 N 项` |
| `itemsAfterCollapse` | `number` | `2` | 折叠时末位保留几项 (含末位) |
| 其它 | `HTMLAttributes<HTMLElement>` | — | 透传到 `<nav>` 根元素 |

### `<Breadcrumb.Item>` (Layer 1)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `children` | `ReactNode` | — | 文本或文本+Icon 组合 |
| `href` | `string` | — | 传 → `<a>` 可点击; 不传 → `<span>` 不可点 |
| `current` | `boolean` | 自动 (末位=true) | 当前页, 渲染 `<span aria-current="page">`, 深色不可点 |
| 其它 | `AnchorHTMLAttributes` | — | 透传到 `<a>` (如 `onClick`, `target`) |

### `<Breadcrumb.Separator>` (Layer 1, 一般无需手动用)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `children` | `ReactNode` | `<Icon name="arrow-right" />` | 自定义分隔符内容 |

### `<Breadcrumb.Ellipsis>` (Layer 1)
| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `onClick` | `MouseEventHandler` | — | 点击事件, 业务自己挂 dropdown 展示隐藏项 |

---

## 4. 视觉规格速查

| 项 | 值 | Token |
|---|---|---|
| 字体 | Roboto Regular | (写死, 旧 Guidelines) |
| 字号 | 16px | `--Breadcrumb-itemFontSize` |
| 行高 | 22px | `--Breadcrumb-itemLineHeight` |
| Item padding (横) | 4px | `--Breadcrumb-itemPaddingInline` (→ `--paddingXXS`) |
| Item 圆角 | 4px | `--Breadcrumb-itemBorderRadius` (→ `--borderRadiusSM`) |
| Separator 横向 margin | 8px | `--Breadcrumb-separatorMarginInline` (→ `--marginXS`) |
| Separator icon 尺寸 | 16px | `--Breadcrumb-separatorIconSize` |
| Item 内 icon 尺寸 | 14px | `--Breadcrumb-itemIconSize` |
| Default 文字色 | gray-7 (#999) | `--Breadcrumb-colorText` (→ `--colorTextTertiary`) |
| Hover / Current 文字色 | gray-9 (#333) | `--Breadcrumb-colorTextHover` (→ `--colorText`) |
| Pressed 文字色 | gray-10 (#1f1f1f) | `--Breadcrumb-colorTextPressed` (→ `--colorTextHeading`) |
| Hover 背景 | colorFillSecondary | `--Breadcrumb-colorBgTextHover` |
| Pressed 背景 | colorFill | `--Breadcrumb-colorBgTextActive` |
| Focus 描边 | controlOutline 2px | `--Breadcrumb-colorBorderFocus` + `--Breadcrumb-focusOutlineWidth` |
| Separator 色 | gray-6 | `--Breadcrumb-colorSeparator` (→ `--colorTextQuaternary`) |

---

## 5. Shopee 特有规则（提炼自旧 Guidelines）

1. **位置**：面包屑通常出现在**页面头部下方、内容区上方**, 通常嵌在 Header Bar 内, 带阴影 `0 1px 4px 0 rgba(0,0,0,0.12)`
2. **层级 ≤ 4 层**：完整显示, 不折叠 (旧 Guidelines 基础面包屑)
3. **层级 > 4 层**：用 `maxItems={4}`, 自动折叠成 `Home > ··· > 倒数2项` (旧 Guidelines 多层级面包屑)
4. **分隔符是 `>` (arrow-right) 不是 `/`**：跟 Ant 不一样, 这是 Shopee 特色
5. **末位 Item 不可点**：自动是 current, 深色, 鼠标不会变 pointer
6. **响应式自适应宽度**：旧 Vue 有 `minWidth: 600` / `maxWidth: 10000` 限制 — 这一版砍掉, 容器自适应; 业务自己用 CSS 控

---

## 6. 场景示例 (Seller Center 真实用例)

### 6.1 普通 3 层路径 — Order Detail
```tsx
<Breadcrumb>
  <Breadcrumb.Item href="/">Home</Breadcrumb.Item>
  <Breadcrumb.Item href="/orders">Orders</Breadcrumb.Item>
  <Breadcrumb.Item>Order #SP240601001</Breadcrumb.Item>
</Breadcrumb>
```

### 6.2 4 层 — Product Edit
```tsx
<Breadcrumb>
  <Breadcrumb.Item href="/">Home</Breadcrumb.Item>
  <Breadcrumb.Item href="/products">Products</Breadcrumb.Item>
  <Breadcrumb.Item href="/products/cat">Electronics</Breadcrumb.Item>
  <Breadcrumb.Item>Edit</Breadcrumb.Item>
</Breadcrumb>
```

### 6.3 深路径 (8 层) — 自动折叠
```tsx
<Breadcrumb maxItems={4} itemsAfterCollapse={2}>
  <Breadcrumb.Item href="/">Home</Breadcrumb.Item>
  <Breadcrumb.Item href="/p">Products</Breadcrumb.Item>
  <Breadcrumb.Item href="/p/e">Electronics</Breadcrumb.Item>
  <Breadcrumb.Item href="/p/e/m">Mobile</Breadcrumb.Item>
  <Breadcrumb.Item href="/p/e/m/b">Brand</Breadcrumb.Item>
  <Breadcrumb.Item href="/p/e/m/b/s">SKU</Breadcrumb.Item>
  <Breadcrumb.Item href="/p/e/m/b/s/v">Variant</Breadcrumb.Item>
  <Breadcrumb.Item>Edit Listing</Breadcrumb.Item>
</Breadcrumb>
// → Home > ··· > Variant > Edit Listing
```

### 6.4 自定义 Separator
```tsx
<Breadcrumb separator="/">
  <Breadcrumb.Item href="/">Home</Breadcrumb.Item>
  <Breadcrumb.Item>Settings</Breadcrumb.Item>
</Breadcrumb>
```

### 6.5 业务自己控制 Ellipsis (挂 popover)
```tsx
import { useState } from 'react';
import { Popover } from '@shopee/design-system';

function PathWithPopover() {
  const [open, setOpen] = useState(false);
  return (
    <Breadcrumb>
      <Breadcrumb.Item href="/">Home</Breadcrumb.Item>
      <Popover open={open} content={<HiddenItemsList />}>
        <Breadcrumb.Ellipsis onClick={() => setOpen(!open)} />
      </Popover>
      <Breadcrumb.Item href="/4">Fourth level</Breadcrumb.Item>
      <Breadcrumb.Item>Fifth level</Breadcrumb.Item>
    </Breadcrumb>
  );
}
```

### 6.6 Item 内带 Icon (Tier 3 自由组合)
```tsx
<Breadcrumb>
  <Breadcrumb.Item href="/">
    <span style={{ display: 'inline-flex', alignItems: 'center', gap: 4 }}>
      <Icon name="anchor" size={14} />
      Home
    </span>
  </Breadcrumb.Item>
  <Breadcrumb.Item>Current</Breadcrumb.Item>
</Breadcrumb>
```

---

## 7. 组合模式 (Breadcrumb × 其它组件)

- **Breadcrumb 在 Page Header 内**：通常包在带阴影的 Header Bar 里 (旧 Guidelines 场景示例), 跟 user/menu icons 同一行
- **Breadcrumb + Tabs**：很多页面 Breadcrumb 之下紧跟 Tabs (Order Detail 等), Breadcrumb 用来定位"我在哪里", Tabs 用来切换"看哪一面"
- **Breadcrumb + Page Title**：Breadcrumb 在上面一行, Page Title (h1) 在下面一行 (更突出当前页)

---

## 8. 反例

| ❌ 错误 | 原因 | ✅ 正确 |
|---|---|---|
| `<Breadcrumb.Item current>Home</Breadcrumb.Item>` 在第一位 | current 应该只用在末位 | 末位自动 current, 不要手动加 |
| `<Breadcrumb><div>Home</div>...</Breadcrumb>` | 必须是 `Breadcrumb.Item`, 其他 child 会被过滤 | 用 `<Breadcrumb.Item>` |
| 自己用 svg 画 `>` 当 separator | 违反铁律 #8 不画 svg | 用 `<Icon name="arrow-right" />` |
| Breadcrumb 当成主要导航用 | Shopee 用 Breadcrumb 是辅助/补充导航 (旧 Guidelines), 主导航用 Sidebar | 主导航用 Sidebar Nav |
| 单独使用 `<Breadcrumb.Separator />` 在两个 Item 之间 | 根组件自动插, 重复了 | 只放 `Breadcrumb.Item`, 自动插 Separator |
| 写中文 demo `<Breadcrumb.Item>首页</Breadcrumb.Item>` | 组件库是 i18n-neutral, demo 一律英文 | `<Breadcrumb.Item>Home</Breadcrumb.Item>` |

---

## 9. a11y 要点

- 根元素 `<nav aria-label="Breadcrumb">` — 屏幕阅读器会读 "Breadcrumb navigation"
- 末位 Item: `<span aria-current="page">` — 告知用户这是当前页
- Separator: `aria-hidden="true"` — 屏幕阅读器不读 `>`
- `Breadcrumb.Item` 链接形态: `<a>` 自带键盘聚焦 + Enter 跳转
- `Breadcrumb.Item` :focus-visible: 2px controlOutline 描边, 键盘聚焦可见
- `Breadcrumb.Ellipsis`: `role="button"` + `tabIndex={0}` + Enter/Space 触发 onClick

---

## 10. 与 Figma 对应

| Figma 节点 | React 组件 | State / Type prop |
|---|---|---|
| ComponentSet `Breadcrumb Link` (924:21) | `<Breadcrumb.Item>` | State: CSS 伪类 (:hover/:active/:focus-visible) + `current` prop |
| ComponentSet `Breadcrumb Separator` (925:14) | `<Breadcrumb.Separator>` | 单 variant, 可 children 覆盖 |
| ComponentSet `Breadcrumb Ellipsis` (925:21) | `<Breadcrumb.Ellipsis>` | State: CSS 伪类 (:hover/:active) + `aria-expanded` |
| ComponentSet `Breadcrumb` (926:50) | `<Breadcrumb>` | Type=Basic / WithEllipsis (代码用 `maxItems` 控制) |

Code Connect 已写好 4 个映射 (`Breadcrumb.figma.tsx`), 在 Figma Dev Mode 选中任一 ComponentSet 可看对应代码片段。
