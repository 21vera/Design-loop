# Header

> 页面头部 — Seller Center 顶部导航容器。**双层 Compound Component**, 严格按旧 Guidelines「类型汇总」做 2 种 Type, 内部全部 instance 现有组件 (Button / Icon / Badge / Avatar / Breadcrumb)。

---

## 1. 总览

- **组件名**: `Header`
- **用途**: 提供 Seller Center 页面的顶部导航壳, 56px 高 + 固定顶部 + 左右两簇布局
- **导入**:
  ```ts
  import {
    Header,
    type HeaderProps,
    type HeaderBrandProps,
    type HeaderIconButtonProps,
    type HeaderUserProps,
    type HeaderDividerProps,
  } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Header`
- **Figma**: [Header (Layer 2)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1020-611) · [Display](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1023-503)
- **Code Connect**: ✅ 已映射 (5 个 ComponentSet, 见 `Header.figma.tsx`)

**依据来源**:
- Tier 2 (大头): 旧 Guidelines `NG-Header` (25:10565)「类型汇总」+「视觉样式」+「场景示例」
- Tier 3: hover / active / focus-visible CSS 状态补齐
- 旧 Vue **没有** Header 组件 → 没有 Tier 1, 所有 props 都是按旧 Guidelines + 现代规范定的
- 复用现有组件 (按 AI操作手册铁律 #8): Button / Icon / Badge / Avatar / Breadcrumb

---

## 2. 决策树 (AI 必读)

```
当前页面属于哪种结构?
├─ 顶层 / 左侧导航场景 (主页 / 列表页 / 仪表盘)
│    → 用「基础页面头部」: <Header.Brand logo title subtitle />
│
└─ 子层级页面 (订单详情 / 商品编辑 / 子流程)
     → 用「面包屑页面头部」: <Header.Brand mini /> + <Breadcrumb> ... </Breadcrumb>

需要哪些右侧操作?
├─ 用户菜单 (头像 + 用户名) → <Header.User name avatar onClick />
├─ 通知中心 (铃铛 + 未读数) → <Header.IconButton icon="notification" badge={n} aria-label="Notifications" />
├─ 应用切换器 (9-dot 网格) → <Header.IconButton icon="menu" aria-label="App switcher" />
├─ 教育中心入口 (Education Hub) → <Button icon="education">Education Hub</Button>  (不是 Header.IconButton!)
└─ 视觉分组 → 在 User 和 Icon 组之间放 <Header.Divider />

需要固定在顶部吗?
├─ 是 (绝大多数情况) → 不传 fixed, 默认 true
└─ 否 (用在 Storybook / 文档预览 / 测试) → fixed={false}
```

---

## 3. Props 完整签名

### `<Header>` (Layer 2 根容器)

| 名称 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `children` | `ReactNode` | — | Compound 子节点。Brand / Breadcrumb → 左簇, 其它 → 右簇, 自动 flex space-between |
| `fixed` | `boolean` | `true` | 是否固定在视口顶部 (旧 Guidelines「Header 只会 Fixed」) |
| (HTML attrs) | `HTMLAttributes<HTMLElement>` | — | 标准 HTML 透传 |

### `<Header.Brand>` (Layer 1)

| 名称 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `logo` | `ReactNode` | — | logo 节点 (img/svg)。Full 模式建议 97×30, Mini 模式 28×28 |
| `mini` | `boolean` | `false` | true → 只渲染 mini logo, 不显示 title/subtitle (面包屑模式专用) |
| `title` | `string` | — | 平台主标题, 18px Roboto Medium。`mini=false` 才显示 |
| `subtitle` | `string` | — | 辅助文案, 14px Roboto Regular 灰色。`mini=false` 才显示 |
| `href` | `string` | — | 整块作为链接跳转。不传 → `<span>` 不可点击 |

### `<Header.IconButton>` (Layer 1)

| 名称 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `icon` | `IconName \| ReactNode` | — | 用 `<Icon name>` 渲染。**禁止自画 svg** (铁律 #8) |
| `badge` | `number \| ReactNode` | — | 右上角徽标。number → 内部用 `<Badge count={n}>` |
| `aria-label` | `string` | — | **必填** — icon 无语义, 屏幕阅读器需要文字 |
| `onClick` | `MouseEventHandler` | — | 点击回调 |

### `<Header.User>` (Layer 1)

| 名称 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | — | 用户名 (Medium 14px) |
| `avatar` | `ReactNode \| string` | — | string → 内部 `<Avatar size="small" type="user" src>`; ReactNode → 直接渲染; 不传 → 默认 user icon Avatar |
| `open` | `boolean` | `false` | dropdown 是否展开, 控制 caret 翻转 + 选中态 bg |
| `onClick` | `MouseEventHandler` | — | 点击触发 dropdown (业务自己挂展开逻辑) |

### `<Header.Divider>` (Layer 1)

| 名称 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| (无业务 prop, 纯 1×32 视觉分隔线) | | | |

---

## 4. 场景示例 (Seller Center 真实用例)

```tsx
// === 场景 1: 基础页面头部 — 主页 / 列表页 ===
<Header>
  <Header.Brand
    logo={<ShopeeLogo />}
    title="Seller Center"
    subtitle="ID: SP24081288 · MY"
  />
  <Header.User name="Mona Chen" avatar={userAvatarSrc} onClick={openUserMenu} />
  <Header.Divider />
  <Header.IconButton icon="menu" aria-label="App switcher" onClick={openAppSwitcher} />
  <Header.IconButton icon="notification" badge={12} aria-label="Notifications" onClick={openInbox} />
  <Button icon="education">Education Hub</Button>
</Header>

// === 场景 2: 面包屑页面头部 — 订单详情页 ===
<Header>
  <Header.Brand mini logo={<ShopeeLogo size="mini" />} />
  <Breadcrumb>
    <Breadcrumb.Item href="/">Home</Breadcrumb.Item>
    <Breadcrumb.Item href="/orders">Orders</Breadcrumb.Item>
    <Breadcrumb.Item href="/orders/all">All Orders</Breadcrumb.Item>
    <Breadcrumb.Item>Order #SP240601001</Breadcrumb.Item>
  </Breadcrumb>
  <Header.User name="Mona" />
  <Header.Divider />
  <Header.IconButton icon="notification" badge={3} aria-label="Notifications" />
  <Button icon="education">Education Hub</Button>
</Header>

// === 场景 3: 用户 dropdown 受控展开 ===
const [open, setOpen] = useState(false);
<Header>
  <Header.Brand logo={<ShopeeLogo />} title="Seller Center" />
  <Header.User
    name="Mona"
    open={open}
    onClick={() => setOpen(!open)}
  />
</Header>

// === 场景 4: 无副标题的极简头部 ===
<Header>
  <Header.Brand logo={<ShopeeLogo />} title="Seller Center" />
  <Header.User name="Mona" />
  <Header.IconButton icon="notification" badge={1} aria-label="Notifications" />
</Header>

// === 场景 5: 不固定头部 (Storybook / 文档展示) ===
<Header fixed={false}>
  ...
</Header>
```

---

## 5. 组合模式

| 模式 | Header 角色 | 配合组件 |
|------|------------|---------|
| **完整 Seller Center 页面壳** | 顶部导航 (56px) | `<Sidebar>` 左侧 + `<main>` 右侧主区 |
| **面包屑页面头部** | 顶部导航 (Brand mini + Breadcrumb) | `<Breadcrumb>` (Breadcrumb 组件已建好, Header 直接接受作为 child) |
| **通知中心入口** | `<Header.IconButton icon="notification" badge>` | `<Badge>` (内部自动 instance) |
| **用户身份区** | `<Header.User>` | `<Avatar>` (内部自动 instance) + 业务侧的 `<Popover>` / `<Menu>` (业务自管) |
| **教育中心入口** | 仅承载位置 | `<Button variant="default" icon="education">` 直接放进 Header (不是 Header.Action) |

**关键约束**: Header 只负责"56px 横排容器 + 左右簇分布"。任何**自定义文字按钮**(如 Education Hub) 一律用 `<Button>` 不要包成 Header 子组件 — 这样可以拿 Button 所有 5 维变体 (Size / Type / State 等) 而不需要在 Header 里重新实现。

---

## 6. 反例 (AI 绝不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---------|---------|------|
| `<Header.IconButton icon={<svg>...</svg>}>` (内联 SVG) | `<Header.IconButton icon="notification">` | 铁律 #8: 必须 instance Icon 库, 不准自画。inline svg 颜色不能跟着 token 走 |
| 在 Header 内自己写 `<button>Education Hub</button>` | `<Button icon="education">Education Hub</Button>` | Button 已经实现了 5 维变体 (size/state/danger/loading), 自己写一份会跟 Design Token 脱节 |
| `<Header.User name="X">` (不传 aria-label 给 IconButton) | `<Header.IconButton icon="menu" aria-label="App switcher">` | icon 无语义, 屏幕阅读器读不到名称, a11y 违规 |
| `<Header.Brand mini title="Seller Center">` | `<Header.Brand mini />` (面包屑模式) 或 `<Header.Brand logo title subtitle />` (基础模式) | mini 模式专为面包屑场景设计, 不显示 title/subtitle。混用会被 CSS 忽略, 误导后续开发者 |
| Header 内放 `<div>` / 任意非 Header.* 子组件做布局 | 用 `<Header.Divider>` 或保持 Compound 子集 | Header 根据 child type 自动分左/右簇, 非识别类型会被推到右簇但分组语义丢失 |
| 用 `fixed={false}` 但不在 Storybook / 测试 | 默认 `fixed=true` | 旧 Guidelines 明确「Header 只会 Fixed」, 业务页面不应让 Header 滚动 |
| `<Header.IconButton badge>` 不传 number 也不传 ReactNode | `<Header.IconButton badge={3}>` 或 `<Header.IconButton badge={<Badge type="hot" />}>` | badge 必须有数字或具体节点, `true` 不会渲染任何 Badge |

---

## 7. Token 主题化

| 需求 | 改哪个 token |
|------|-------------|
| Header 整体高度 | `--Header-heightBase` (默认 56px) |
| 左右内边距 | `--Header-paddingInline` (默认 16px) |
| IconButton 尺寸 | `--Header-iconButtonSize` (默认 32px) |
| User 容器高度 | `--Header-userHeight` (默认 44px) |
| Brand 主标题字号 | `--Header-brandTitleFontSize` (默认 18px) |
| Brand 副标题字号 | `--Header-brandSubtitleFontSize` (默认 14px) |
| Header 背景色 | `--Header-colorBg` (默认 colorBgContainer 白) |
| 底部分隔线色 | `--Header-colorBorderBottom` (默认 colorBorderSecondary) |
| Icon 默认色 | `--Header-colorIcon` (默认 colorTextSecondary gray-8) |
| Icon hover 加深 | `--Header-colorIconHover` (默认 colorText gray-9) |
| IconButton hover 背景 | `--Header-colorBgHover` (默认 colorBgTextHover) |
| Header.Divider 颜色 | `--Header-colorDivider` (默认 colorBorderSecondary) |

20 个 token 完整清单见 `src/tokens/components/header.tokens.css`。

---

## 8. 无障碍 (a11y)

- **focus 态**: IconButton / User 都用 `:focus-visible` (键盘 Tab 到才触发), 加 2px 描边 (`box-shadow: 0 0 0 2px var(--Header-colorIconHover)`)。鼠标点击不触发 focus 环, 避免视觉噪音。
- **键盘**: Tab 顺序为左到右、Brand → 左侧 Breadcrumb → 右侧 User → Divider → IconButton ×N → Button。Enter / Space 触发 onClick。
- **屏幕阅读器**:
  - Header 根容器是 `<header>` landmark, 自动被识别为页面头部 region。
  - `<Header.IconButton>` 必填 `aria-label` (icon 无文字, 没有 label 等于无语义元素)。
  - `<Header.User>` 内部加了 `aria-haspopup="menu"` + `aria-expanded={open}`, 屏幕阅读器会朗读"已折叠/已展开 菜单"。
  - `<Header.Divider>` 是 `aria-hidden="true"` 纯视觉, 不进入朗读流。
- **对比度**: 默认色组合 `colorIcon (gray-8) on colorBg (white)` ≈ 8.5:1 (远超 WCAG AAA 7:1)。hover 态 `colorIconHover (gray-9) on colorBgTextHover` ≈ 10:1。

---

## 文档维护

- 2026-06-03 创建 (Phase 6) — 写完 8 节 + Code Connect + Excel 已更新。
