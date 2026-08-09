# Card 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注）：
> - **主**：旧 Shopee Guidelines [GP-Card 节点 40:10723](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=40-10723) — 3 业务类型 + Secondary text
> - **辅**：旧 Vue `Shopee前端组件源码/components/card/` — 5 props (title/border/gray/hover/padding)
> - **旧库精确数值**：[节点 4032:5677](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/?node-id=4032-5677) — 288×160 标准, padding 24, Roboto 22/14
> - **System Test**：[ComponentSet 891:20](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=891-20) + [Display 892:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=892-2) — 6 变体

---

## 0. 依据来源映射（防越界）

| Prop | 来源 | 证据 |
|---|---|---|
| `variant: 'normal' \| 'gray' \| 'border'` | ✅ Tier 1 | 旧 Vue (border/gray boolean 合并) + 旧 Guidelines 3 类型 |
| `title` | ✅ Tier 2 旧 Vue | — |
| `description` | ✅ Tier 2 旧 Guidelines | "Secondary text" 明确变体 |
| `hoverable` | ✅ Tier 2 旧 Vue `hover` 改 React 命名 | — |
| `padding` | ✅ Tier 2 旧 Vue | 默认 24 |
| `children` | ✅ Tier 2 旧 Vue default slot | — |

无 Tier 4 项。

**与旧 Vue 关键差异**:
- 旧 Vue `border: boolean` + `gray: boolean` 两个 boolean 互斥（可能同时为 true 行为未定义）→ ✅ 合并为 `variant` enum
- 旧 Vue `hover: boolean` → React 风格 `hoverable`

---

## 1. 总览

- **组件名**：`Card`
- **用途**：通用信息容器, 包裹任意内容
- **导入**：
  ```ts
  import { Card, type CardProps, type CardVariant } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Card`
- **Code Connect**：Card.figma.tsx

---

## 2. 决策树（AI 必读）

```
需要一个内容容器?
├─ 是 → Card
│    ├─ 强调内容 (有阴影抓眼) → variant="normal"
│    ├─ 背景区分 (列表/设置项) → variant="gray"
│    └─ 网格内的卡片 (轻量边界) → variant="border"
│
└─ 否 → 直接 <div>, 不需要 Card

可点击吗?
├─ 是 (整卡跳转/选中) → hoverable={true}
└─ 否 → 普通展示

有标题吗?
├─ 是 → title prop
└─ 否 → 只用 children

有副标题吗?
├─ 是 → description prop (14px 灰字)
└─ 否 → 不传

需要自定义内边距?
├─ 是 → padding={n} (默认 24)
└─ 否 → 不传
```

---

## 3. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `variant` | `'normal' \| 'gray' \| 'border'` | `'normal'` | 类型 |
| `title` | `ReactNode` | — | 标题 (Roboto Medium 22px) |
| `description` | `ReactNode` | — | 副文本 (Roboto Regular 14px 灰字) |
| `hoverable` | `boolean` | `false` | hover 时叠加 alpha 4% 覆盖 |
| `padding` | `number` | `24` | 内边距 px |
| `children` | `ReactNode` | — | 正文 (在 title/description 下方) |

---

## 4. 视觉规格速查（旧库 + Figma 1:1）

| 项 | 值 | Token |
|---|---|---|
| 标准展示尺寸 | 288×160 | — |
| padding | 24 px | `--Card-padding` |
| 圆角 | **4 px** (统一) | `--Card-borderRadiusVariant` |
| 边框宽度 (Border) | 1 px | `--Card-lineWidth` |
| title 字号 | **18 px Roboto Medium** (旧库精确) | `--Card-titleFontSize` |
| title 行高 | 20 px | `--Card-titleLineHeight` |
| description 字号 | 14 px Roboto Regular | `--Card-descriptionFontSize` |
| title-description 间距 | 4 px | `--Card-gapTitleDescription` |

### 3 类型视觉差异

| 类型 | 背景 | 阴影 | 边框 |
|---|---|---|---|
| Normal | `colorBgContainer` (白) | `0 1px 4px 0 rgba(0,0,0,0.10)` | — |
| Gray | `colorBgLayout` (浅灰) | — | — |
| Border | `colorBgContainer` (白) | — | 1px `colorBorderSecondary` |

### Hover 覆盖

`hoverable=true` 时, hover 状态 `::before` 绝对定位覆盖整卡, bg `rgba(0,0,0,0.04)` (alpha 4% 黑)。旧 Vue SCSS 一致。

---

## 5. Shopee 特有规则

1. **Normal 必须带阴影** — 旧 Guidelines 明确 `0 1px 4px 0 rgba(0,0,0,0.10)`, 不要换成其他 box-shadow token
2. **Gray 不允许阴影** — 旧规范明确 "无阴影"，避免视觉重复
3. **Border 圆角 4px 与 Normal/Gray 一致** — 用户确认统一 4px
4. **title Roboto Medium (500)** — 不是 Bold (700), 不是 Regular (400)
5. **Hover 用 ::before alpha 4% 黑覆盖** — 不是改 bg, 也不是加 box-shadow

---

## 6. 场景示例

### 6.1 Dashboard 数据卡

```tsx
<div style={{ display: 'grid', gridTemplateColumns: 'repeat(4, 1fr)', gap: 16 }}>
  <Card variant="normal" title="$24,567" description="Today's revenue" />
  <Card variant="normal" title="1,234" description="New orders" />
  <Card variant="normal" title="89%" description="Customer satisfaction" />
  <Card variant="normal" title="56" description="Active campaigns" />
</div>
```

### 6.2 设置入口（Gray + Hoverable）

```tsx
<Card
  variant="gray"
  hoverable
  title="Shop profile"
  description="Manage your shop information and branding"
  onClick={() => navigate('/settings/shop')}
/>
```

### 6.3 商品网格（Border + Hoverable）

```tsx
<Card variant="border" hoverable>
  <img src={product.cover} alt={product.name} />
  <div>{product.name}</div>
  <div>${product.price}</div>
</Card>
```

### 6.4 包裹 Form

```tsx
<Card title="Account Settings" description="Update your basic info">
  <Form>...</Form>
</Card>
```

### 6.5 自定义 padding (紧凑/宽松)

```tsx
<Card padding={12} variant="gray">  {/* 紧凑 */}
  Quick info
</Card>

<Card padding={48} variant="normal" title="Featured">  {/* 宽松 */}
  Marketing content
</Card>
```

---

## 7. 组合模式

| 搭配组件 | 用法 |
|---|---|
| **Form** | Card 包 Form, title 作为表单标题 |
| **Table** | Border Card 包 Table, 作为数据面板 |
| **Tag** | Card 右上角放 Tag 显示状态 |
| **Button** | Card 底部放 Button 作为操作 |
| **Card** | Card 内嵌 Card 做嵌套布局 (但不推荐超过 1 层) |

---

## 8. 反例（不要这么写）

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 单独按钮外面再包 Card | 直接用 Button | Card 是容器, 不是装饰 |
| 整页面包一个大 Card | 用 Layout 组件 | Card 是局部容器 |
| 给 Normal Card 加深阴影 | 用 token 默认阴影 | 视觉一致性 |
| Border + Hover 不传 onClick | hoverable 要配合点击行为 | 否则用户误以为可点 |
| padding=0 | 至少 8px | 内容紧贴边缘视觉不好 |
| 嵌套 3 层 Card | 用 `<section>` 或边距 | 视觉混乱 |
| title 用 Bold (700) | Roboto Medium (500) | 旧 SCSS 一致 |

---

## 9. 与其他容器的区别

| 维度 | Card | Modal | Drawer |
|---|---|---|---|
| 位置 | 行内 / 行流 | 屏幕中央覆盖 | 屏幕侧滑入 |
| 关闭 | 不能关闭 | 必须可关 | 必须可关 |
| 用途 | 信息展示 | 强对话 | 详情 / 设置 |

---

## 10. 已知限制 / 后续 TODO

- ❌ 不支持 `extra` slot (右上角自定义) — 旧 Vue 没有, Phase 2.5 跳过
- ❌ 不支持 `cover` 图片头 — Tier 4, 等真实场景需求再加
- ❌ 不支持 `actions` 底部操作区 — 同上
- ✅ 用户确认全部 4px 圆角（不分 default/variant 两种）
