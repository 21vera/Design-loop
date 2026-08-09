# Tabs

> 页签切换 — **7 种视觉风格** × Count 2-6 × 受控/非受控双模式。Compound 组件 (Tabs + Tabs.TabPane)。

## 1. 总览

- **组件名**: `Tabs` / `Tabs.TabPane`
- **用途**: 将关联但分属不同类别的内容分隔展示，单页面内容切换
- **导入**:
  ```ts
  import { Tabs, type TabsType, type TabsProps, type TabPaneProps } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Tabs`
- **Figma**:
  - [Tabs ComponentSet (1241:675)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1241-675) — 35 variants (Type 7 × Count 5)
  - [TabItem ComponentSet (1240:773)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1240-773) — 30 variants (Type 5 × State 3 × HasIcon 2)
  - [ModuleTab ComponentSet (1225:317)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1225-317) — 24 variants (Type 2 × State 3 × Position 4)
  - [SlideArrow ComponentSet (1219:34)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1219-34) — 2 variants
- **Code Connect**: ✅ (`Tabs.figma.tsx`)

**依据来源**:
- Tier 1: System Test ComponentSets (Phase 4 重做后)
- Tier 2: 旧库 4121:422 (Tabs 类型汇总 + 组合规格 1:1 扒值)
- 旧 Vue (`tabMargin`/`activeIndicatorHeight`/`outline-button-group` 等惯例)

---

## 2. 7 种 Type (核心要先记住)

| Type | 视觉 | 场景 | 业务示例 |
|---|---|---|---|
| `default` | 纯文字 + 橙下划线 | 最常见的页签 | Overview / Orders / Products |
| `digital` | 文字 + inline 数字 | 列表分类带数量 | Pending (18) / Shipped (56) |
| `icon` | 前置 icon + 文字 | 强语义图标分类 | + Add / × Close / → Next |
| `tooltip` | 文字 + 后置 ? 提示 | 需补充说明的页签 | Performance ?/ Returns ? |
| `card` | 折叠纸样式 (灰底 → 白底 Active) | 类似文件夹 tab 多文档切换 | Doc 1 / Doc 2 / Doc 3 |
| `module` | Outline 按钮组 | 紧凑的时间/筛选切换 | Daily / Weekly / Monthly |
| `digital-module` | 按钮组 + inline 数字 | 紧凑分类带数量 | All (120) / Live (45) |

**决策树 (AI 必读)**:
```
要切换页签?
├─ 主导航 / 顶级分类 (页面切换)? — 用 `default` (最常见)
├─ 分类带"数量徽标"? — 列表场景用 `digital`, 紧凑场景用 `digital-module`
├─ 分类有强语义图标? — `icon` (前置), 复用 <Icon /> 库
├─ 分类需要 hover 解释? — `tooltip` (后置 ?)
├─ 类似文件夹的多文档/多面板切换? — `card`
└─ 紧凑筛选 / 时间维度切换? — `module` (outline 按钮组)
```

---

## 3. Props 完整签名

### Tabs

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `type` | `TabsType` | `'default'` | 视觉风格 7 选 1 |
| `activeKey` | `string` | — | **受控** active key (传 → 受控模式) |
| `defaultActiveKey` | `string` | 第 1 个 TabPane.tabKey | **非受控** 初始 active key |
| `onChange` | `(key: string) => void` | — | Tab 切换回调 |
| `children` | `ReactNode` | — | TabPane 子节点 |
| `className` | `string` | — | 透传到根 |
| `renderContent` | `(activeKey: string) => ReactNode` | — | 自定义内容渲染 (覆盖默认 = active TabPane.children) |

### Tabs.TabPane

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `tabKey` | `string` | — | **必填**, 唯一标识 |
| `title` | `ReactNode` | — | **必填**, tab 标签 |
| `count` | `number \| string` | — | Digital/Digital-Module 用, inline 数字 ("18", "99+") |
| `icon` | `ReactNode` | — | Icon 用, 前置 icon (传 `<Icon name="..." size={16} />`) |
| `tooltip` | `ReactNode` | — | Tooltip 用, ? icon hover 内容 |
| `disabled` | `boolean` | `false` | 禁用 |
| `children` | `ReactNode` | — | tab 内容 (Tabs 默认渲染 active 的内容) |

---

## 4. 场景示例

### 4.1 非受控 (常用)
```tsx
<Tabs type="default" defaultActiveKey="overview">
  <Tabs.TabPane tabKey="overview" title="Overview">Overview content</Tabs.TabPane>
  <Tabs.TabPane tabKey="orders"   title="Orders">Orders content</Tabs.TabPane>
  <Tabs.TabPane tabKey="products" title="Products">Products content</Tabs.TabPane>
</Tabs>
```

### 4.2 受控 (与全局状态/路由联动)
```tsx
const [tab, setTab] = useState('overview');

<Tabs type="default" activeKey={tab} onChange={setTab}>
  <Tabs.TabPane tabKey="overview" title="Overview">…</Tabs.TabPane>
  <Tabs.TabPane tabKey="orders"   title="Orders">…</Tabs.TabPane>
</Tabs>
```

### 4.3 Digital — 订单状态分类
```tsx
<Tabs type="digital" defaultActiveKey="pending">
  <Tabs.TabPane tabKey="pending"   title="Pending"   count={18}>…</Tabs.TabPane>
  <Tabs.TabPane tabKey="shipped"   title="Shipped"   count={56}>…</Tabs.TabPane>
  <Tabs.TabPane tabKey="delivered" title="Delivered" count="99+">…</Tabs.TabPane>
  <Tabs.TabPane tabKey="cancelled" title="Cancelled" count={0}>…</Tabs.TabPane>
</Tabs>
```

### 4.4 Icon — 引用 Icon 库
```tsx
import { Icon } from '@shopee/design-system';

<Tabs type="icon" defaultActiveKey="add">
  <Tabs.TabPane tabKey="add"   title="Add"   icon={<Icon name="add" size={16} />}>…</Tabs.TabPane>
  <Tabs.TabPane tabKey="close" title="Close" icon={<Icon name="close" size={16} />}>…</Tabs.TabPane>
</Tabs>
```

### 4.5 Module — 时间维度切换 (button group)
```tsx
<Tabs type="module" defaultActiveKey="daily">
  <Tabs.TabPane tabKey="daily"   title="Daily">…</Tabs.TabPane>
  <Tabs.TabPane tabKey="weekly"  title="Weekly">…</Tabs.TabPane>
  <Tabs.TabPane tabKey="monthly" title="Monthly">…</Tabs.TabPane>
  <Tabs.TabPane tabKey="yearly"  title="Yearly">…</Tabs.TabPane>
</Tabs>
```

### 4.6 自定义内容渲染 (复杂内容懒加载/路由)
```tsx
<Tabs type="default" activeKey={tab} onChange={setTab}
  renderContent={(key) => {
    if (key === 'orders') return <OrdersPage />;
    if (key === 'products') return <ProductsPage />;
    return null;
  }}>
  <Tabs.TabPane tabKey="orders"   title="Orders" />
  <Tabs.TabPane tabKey="products" title="Products" />
</Tabs>
```

---

## 5. 视觉规格 (1:1 Figma, 旧库 4121:422)

| 项 | Line family (default/digital/icon/tooltip) | Card | Module / Digital-Module |
|---|---|---|---|
| 高 | 56 (pad 19 + text 18 + pad 19) | 40 (pad 11×2 + text 18) | 32 (pad 7×2 + text 18) |
| Padding inline | 16 | 16 | 16 |
| 圆角 | 0 | top-only 4 | Position 决定 (Solo=4/Left=左4/Middle=0/Right=右4) |
| Border | 无 (active 仅底部 ink 3px) | 1px #E8E8E8 全围 | 1px outline (Active 时 4 边橙色) |
| Active 字色 | #EE4D2D + Medium | #EE4D2D + Medium | #EE4D2D + Medium |
| Active 视觉 | 橙下划线 3px | 白底 + 橙字 (灰底 → 白底) | 橙 outline 4 边 |
| Gap (组合时) | 24 | 4 | 0 (border 共享 + Active 时 -1px margin 重叠) |

### 关键 Token

```css
--Tabs-lineTabHeight: 56px;
--Tabs-cardTabHeight: 40px;
--Tabs-moduleTabHeight: 32px;
--Tabs-paddingBlockLine: 19px;
--Tabs-paddingBlockCard: 11px;
--Tabs-paddingBlockModule: 7px;
--Tabs-paddingInline: 16px;
--Tabs-activeIndicatorHeight: 3px;
--Tabs-tabGap: 24px;            /* Line family */
--Tabs-digitalGap: 4px;         /* Card gap + Digital inline */
--Tabs-moduleBorderRadius: 4px;
--Tabs-cardBorderRadius: 0;     /* top-only via CSS */
--Tabs-colorText: #333333;
--Tabs-colorTextActive: var(--colorPrimary);  /* #EE4D2D */
--Tabs-colorTextDisabled: #999999;
--Tabs-cardNormalBg: #F6F6F6;
--Tabs-cardActiveBg: #FFFFFF;
--Tabs-cardBorder: #E8E8E8;
--Tabs-moduleNormalBorder: #E5E5E5;
--Tabs-moduleActiveBorder: var(--colorPrimary);
```

---

## 6. Module Position 机制 (核心实现细节)

ModuleTab/Digital-Module 是 outline button group。多个 cell 拼接时:

```
[Active Left] [Normal Middle] [Normal Middle] [Normal Right]
   ┌────┐      ┌────┐          ┌────┐          ┌────┐
   │    │      │    │          │    │          │    │
   └────┘      └────┘          └────┘          └────┘
   左圆角      无圆角           无圆角           右圆角
   全 border   无左 border      无左 border      无左 border
   (左邻 right border 当左 border)
```

**Position 自动计算** (Tabs root 帮你算):
- 单 cell → `solo` (4 圆角全 border)
- 多 cell 首位 → `left` (左圆角, 全 border)
- 多 cell 中间 → `middle` (无圆角, 无左 border)
- 多 cell 末位 → `right` (右圆角, 无左 border)

**Active 特殊处理**: 当 Middle/Right 位置变 Active, 左 border 自动恢复成橙色 (`margin-left: -1px` 防止位移)。
所以 Active cell **永远 4 边都是橙色 outline**, 不管它在组内哪个位置。

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 用 `default` 类型 + `count` prop | 改用 `digital` type | count 仅 digital/digital-module 显示 |
| 用 `module` 类型放 `icon` prop | icon 仅 `type='icon'` 渲染 | Module 类型不显示 icon (设计未定义) |
| Tabs 里塞非 TabPane 的子节点 | 只能放 `Tabs.TabPane` | 其他子节点会被过滤丢弃 |
| 6 个以上 tab | ≤ 6 个 (Count 轴 2-6) | 超过 6 视觉太挤, 建议改用 Select 或分层导航 |
| `<Tabs.TabPane key="a">` (用 React key 当 tabKey) | `<Tabs.TabPane tabKey="a" key="a">` | React key 和 tabKey 分开, tabKey 是业务 ID |
| 把 TabPane 的内容塞到 `title` | 内容放 `children`, 标签放 `title` | title 只渲染在 tab bar, children 渲染在 content |
| `icon`/`tooltip` 类型不传 `icon`/`tooltip` prop | 必须传 (Icon 类型必传 icon, Tooltip 类型可不传) | 否则视觉不完整 |
| 自定义画 + (add) 图标 | 用 `<Icon name="add" size={16} />` | 铁律 #8: 禁止重画 Icon |
| 受控模式只传 `onChange` 不传 `activeKey` | 传 `activeKey` 进入受控 | 只 `onChange` 没 `activeKey` 仍是非受控 |

---

## 8. Accessibility

- Tabs 容器: `role="tablist"`
- 每个 TabItem: `role="tab"` + `aria-selected={isActive}` + `aria-disabled` (disabled 时)
- 内容区: `role="tabpanel"`
- 键盘: Tab/Shift+Tab 切焦点, Enter/Space 激活 (button 默认行为)
- Disabled tab: `tabindex={-1}`, 不可聚焦

未来增强 (TODO):
- 左右方向键切换 active tab
- Home/End 跳首末
- SlideArrow 溢出滚动 (当 tab 数超出容器宽度)

---

## 9. 历史变更

- **2026-06-05 v1** — Phase 5 首版
  - 7 type (default/digital/icon/tooltip/card/module/digital-module)
  - Compound 组件 (Tabs + Tabs.TabPane)
  - 受控 + 非受控
  - Module Position 自动计算 (solo/left/middle/right)
  - Active Middle/Right 4 边 outline 重建 (margin-left: -1px 防位移)
