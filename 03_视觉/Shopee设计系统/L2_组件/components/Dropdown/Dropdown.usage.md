# Dropdown

> 下拉菜单 — Trigger + 4 状态 Item + Portal 弹层. 支持 click/hover 触发, 6 placement, 受控/非受控双模式.

## 1. 总览

- **组件名**: `Dropdown`
- **用途**: 表格行操作 / 排序 / 筛选 / 用户菜单 / 任何「点开-选-关」场景
- **导入**:
  ```ts
  import { Dropdown, type DropdownItem } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Dropdown`
- **Figma**:
  - [DropdownItem ComponentSet (1289:35)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1289-35) — 8 variants (State 4 × HasIcon 2)
  - [DropdownMenu ComponentSet (1290:24)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1290-24) — 1 base
  - [DropdownItem Display (1291:19)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1291-19)
  - [DropdownMenu Display (1291:81)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1291-81)
- **Code Connect**: ✅ (`Dropdown.figma.tsx`)

**依据来源**:
- Tier 1: System Test ComponentSet DropdownItem (1289:35) — 用户确认 8 variants
- Tier 2: 旧规范 794:325 — 触发方式 / 位置 / shadow / 4 状态全规格
- 旧库 4131:107 — 视觉精确扒值 (border-radius 4 / padding 7/12 → 4-pt 规整化为 8/12)

---

## 2. 4 个 Item 状态 (核心要先记住)

| State | 视觉 | 业务示例 |
|---|---|---|
| `default` | bg 白, 文字 `#333` | 普通可选项 |
| `hover` | bg `#F5F5F5` (= 白 × 0.96, 4% 黑 overlay), 文字 `#333` | 鼠标悬浮 (CSS 自动, 不用手动设) |
| `selected` | 文字橙 `#EE4D2D`, 无对勾 icon | 当前已选/激活项 |
| `disabled` | 文字灰 `#999`, 不可点 | 权限不足/暂不可用 |

---

## 3. 决策树 (AI 必读)

```
要点击触发一组选项?
├─ 选项有强语义图标 (Edit / Delete / Settings)? → Dropdown items 用 icon prop
├─ 选项需要"当前已选"高亮? → selected prop
├─ 选项有禁用条件? → disabled prop
└─ 都没有? → 简单 Dropdown

触发方式选哪个?
├─ 显式点击触发 (主流, 默认)? → triggerOn="click"
├─ hover 自动展开 (常见于导航 / 工具栏)? → triggerOn="hover"

Menu 位置?
├─ 位置充足 → placement="bottom-start" (默认)
├─ Trigger 在右侧, 菜单容易超出 → "bottom-end"
├─ Trigger 在屏幕底部 → "top-start" / "top-end"
└─ 居中对齐 → "*-center"
```

---

## 4. Props 完整签名

### Dropdown

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `trigger` | `ReactNode` | — | **必填**, 触发元素 (任意 ReactNode, 通常 `<Button>`) |
| `items` | `DropdownItem[]` | — | **必填**, 菜单项数组 |
| `onSelect` | `(key, item) => void` | — | 选择回调 |
| `triggerOn` | `'click' \| 'hover'` | `'click'` | 触发方式 |
| `placement` | `DropdownPlacement` | `'bottom-start'` | 6 位置 (top/bottom × start/center/end) |
| `open` | `boolean` | — | 受控 open 状态 |
| `defaultOpen` | `boolean` | `false` | 非受控初始 open |
| `onOpenChange` | `(open) => void` | — | open 变化回调 |
| `closeOnSelect` | `boolean` | `true` | 选中后自动关闭 |
| `disabled` | `boolean` | `false` | 禁用整个 trigger |
| `minWidth` | `number \| string` | `140` | Menu 最小宽度 |
| `className` | `string` | — | trigger 外层 className |
| `menuClassName` | `string` | — | Menu 外层 className |

### DropdownItem (单项)

| Prop | 类型 | 说明 |
|---|---|---|
| `key` | `string` | **必填**, 唯一标识 |
| `label` | `ReactNode` | **必填**, 显示内容 |
| `icon` | `ReactNode` | 可选, 尾部 icon |
| `disabled` | `boolean` | 禁用此项 |
| `selected` | `boolean` | 标记此项已选 (文字变橙) |

---

## 5. 场景示例

### 5.1 基础 (非受控, 点击触发)
```tsx
<Dropdown
  trigger={<Button>Actions</Button>}
  items={[
    { key: 'edit',    label: 'Edit' },
    { key: 'archive', label: 'Archive' },
    { key: 'delete',  label: 'Delete' },
  ]}
  onSelect={(key) => console.log(key)}
/>
```

### 5.2 带 icon
```tsx
import { Icon } from '@shopee/design-system';

<Dropdown
  trigger={<Button>Manage</Button>}
  items={[
    { key: 'add',   label: 'Add new', icon: <Icon name="add" size={16} /> },
    { key: 'close', label: 'Close',   icon: <Icon name="close" size={16} /> },
  ]}
/>
```

### 5.3 已选项高亮 (selected)
```tsx
const [sortBy, setSortBy] = useState('name');

<Dropdown
  trigger={<Button>Sort: {sortBy}</Button>}
  items={[
    { key: 'name', label: 'Sort by name', selected: sortBy === 'name' },
    { key: 'date', label: 'Sort by date', selected: sortBy === 'date' },
  ]}
  onSelect={(key) => setSortBy(key)}
/>
```

### 5.4 受控 open
```tsx
const [open, setOpen] = useState(false);

<Dropdown
  trigger={<Button>Menu</Button>}
  items={defaultItems}
  open={open}
  onOpenChange={setOpen}
/>
<Button onClick={() => setOpen(true)}>Open externally</Button>
```

### 5.5 Hover 触发 (导航场景)
```tsx
<Dropdown
  trigger={<Button>Filter</Button>}
  items={filterOptions}
  triggerOn="hover"
/>
```

### 5.6 表格行操作 (placement bottom-end)
```tsx
<tr>
  <td>{product.name}</td>
  <td>{product.price}</td>
  <td>
    <Dropdown
      trigger={<Button size="small">⋯</Button>}
      placement="bottom-end"
      items={[
        { key: 'edit',    label: 'Edit' },
        { key: 'archive', label: 'Archive' },
        { key: 'delete',  label: 'Delete', disabled: !canDelete },
      ]}
      onSelect={(key) => handleAction(product.id, key)}
    />
  </td>
</tr>
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| Item 高 | 32px | `--Dropdown-itemHeight` |
| Item padding | 8px 12px (4-pt grid) | `--Dropdown-itemPaddingBlock/Inline` |
| Item 字号 | 14px | `--Dropdown-itemFontSize` |
| Item line-height | 16px (压缩) | `--Dropdown-itemLineHeight` |
| Item icon | 16px, gap 4px | `--Dropdown-iconSize/itemGap` |
| Menu border-radius | 4px | `--Dropdown-menuBorderRadius` |
| Menu min/max width | 140 / 600 px | `--Dropdown-menuMinWidth/MaxWidth` |
| Menu 2 层 shadow | `0 8px 16px rgba(0,0,0,0.12)` + `0 0 16px rgba(0,0,0,0.06)` | `--Dropdown-menuShadow` |
| Hover bg | `#F5F5F5` (4% 黑 overlay 预算) | `--Dropdown-colorBgHover` |
| Selected text | `#EE4D2D` (primary) | `--Dropdown-colorTextSelected` |
| Disabled text | `#999999` | `--Dropdown-colorTextDisabled` |

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 在 trigger 里用 Input 当触发元素 | 用 Button 当 trigger (或自定义 wrapping div) | Input 自带 focus 行为, 跟菜单 open 冲突 |
| 同时传 `open` 和 `defaultOpen` | 二选一 | `open` 优先, 但混用会让代码乱 |
| Item 50+ 项 | 改用 Select 组件 (待建) 或分组 / 搜索 | Dropdown 设计为短列表 (≤20 项), 长列表性能差 + 滚动体验差 |
| 用 Dropdown 当 modal 入口 | 用 Modal 触发 | Dropdown 只承载即时操作, 不承载多步流程 |
| items 数组每次渲染新引用 | 用 useMemo 包装 items | 否则 position 重算频繁, 性能差 |
| selected 多个 item | 只标 1 个 selected (单选) | Dropdown 是单选语义, 多选请用 Checkbox group |
| placement="top-*" 但 trigger 在屏幕上半部 | 用 bottom-* (系统会自动 viewport-clamp 但避免依赖) | 主动选位置最稳 |
| 自画 icon 替代 `<Icon />` | 用 Icon 库 instance (铁律 #8) | icon 在内置 component 改了不会自动同步 |

---

## 8. Accessibility

- Menu 容器: `role="menu"`
- 每项: `role="menuitem"` + `disabled` 同步 HTML disabled
- 键盘:
  - `Esc` 关闭菜单
  - Tab 在菜单项之间切换
  - Enter / Space 选中 (button 默认行为)
  - 焦点状态 `:focus-visible` 显示 hover bg

未来增强 (TODO):
- 上下方向键导航 + 第一项自动 focus
- Home/End 跳首末
- 输入字母快速跳到对应项 (typeahead)

---

## 9. 历史变更

- **2026-06-05 v1** — Phase 5 首版
  - 2 ComponentSet (DropdownItem 8 + DropdownMenu 1)
  - Compound API (trigger + items)
  - Portal menu + 6 placement (含 viewport clamping)
  - click/hover 两种触发, 受控/非受控双模式
  - Esc + click-outside 关闭, hover 模式延迟关
  - 21 Token 全绑定 (15 Component + 6 Global)
