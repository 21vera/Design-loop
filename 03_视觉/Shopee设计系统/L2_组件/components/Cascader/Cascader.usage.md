# Cascader

> 级联选择菜单 — Trigger (Input-style) + Portal 多列 popup, 支持任意嵌套深度的 option tree.

## 1. 总览

- **组件名**: `Cascader`
- **用途**: 多级嵌套选项 — 国家/省/市, 类目/子类目/SKU, 文件夹层级等
- **导入**:
  ```ts
  import { Cascader, type CascaderOption } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Cascader`
- **Figma** (4 ComponentSet):
  - [CascaderItem (1293:35)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1293-35) — 8 variants (State 4 × HasArrow 2)
  - [CascaderMenu (1295:55)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1295-55) — 1 base (3 列 popup)
  - [CascaderTrigger (1304:166)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1304-166) — 12 variants (Status 3 × HasValue 2 × IsOpen 2)
  - [Cascader 组合 (1307:178)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1307-178) — trigger + menu 合一
- **Code Connect**: ✅ (`Cascader.figma.tsx`)

**依据来源**:
- Tier 1: System Test 4 个 ComponentSet (用户确认)
- Tier 2: 旧规范 40:13827 — 4 使用场景 + 视觉样式全规格
- 旧库 4131:171 — 旧库 design context 精确扒值 (padding 7/12, gap 8, LH 18)

---

## 2. 4 个 Item 状态 (核心要先记住)

| State | 视觉 | 业务示例 |
|---|---|---|
| `default` | 白底, 文字 `#333` | 普通可选项 |
| `hover` | 灰底 `#F5F5F5`, 文字 `#333` | 鼠标悬浮 (CSS 自动) |
| `selected` | 文字 + 箭头都橙 `#EE4D2D`, **字重 Medium** | 当前已选路径上的节点 |
| `disabled` | 文字灰 `#999`, 不可点 | 权限不足/暂不可用 |

**Branch (有子级)**: 右侧显示 `>` 箭头, 点击展开下一列
**Leaf (无子级)**: 无箭头, 点击 commit value + 关闭

---

## 3. 决策树 (AI 必读)

```
要让用户从多级嵌套选项里选?
├─ 2-3 层固定深度, 每层选项 ≤ 10 → Cascader (本组件)
├─ 任意深度, 树状大数据 → TreeSelect (待建)
├─ 单层选项 (扁平 list) → Dropdown (短列表) 或 Select (待建, 长列表)

数据组织?
├─ 提前知道完整树结构 → options prop 直接传完整树
└─ 远程懒加载 → 暂未支持, 等 v2

触发方式?
├─ 严格只在点击 (默认, 防误触) → expandTrigger="click"
└─ Hover 自动展开 (常见于导航 / 后台快选) → expandTrigger="hover"
```

---

## 4. Props 完整签名

### Cascader

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `options` | `CascaderOption[]` | — | **必填**, 嵌套树 |
| `value` | `string[]` | — | **受控** 当前选中 path (例如 `['sg', 'central', 'orchard']`) |
| `defaultValue` | `string[]` | `[]` | 非受控初始 path |
| `onChange` | `(value, path) => void` | — | 选择回调, path = CascaderOption[] |
| `expandTrigger` | `'click' \| 'hover'` | `'click'` | 子级展开触发 |
| `placement` | `'bottom-start' \| ...` | `'bottom-start'` | 4 位置 |
| `placeholder` | `string` | `'Please select'` | 占位符 |
| `disabled` | `boolean` | `false` | 禁用 trigger |
| `clearable` | `boolean` | `false` | 已选时右侧显示清空按钮 |
| `displaySeparator` | `string` | `' / '` | trigger 显示 path 时的分隔 |
| `className` | `string` | — | trigger 外层 |
| `triggerClassName` | `string` | — | trigger 自身 |
| `menuClassName` | `string` | — | menu 弹层 |
| `minWidth` | `number \| string` | — | menu 最小宽度覆盖 |

### CascaderOption

| Prop | 类型 | 说明 |
|---|---|---|
| `value` | `string` | **必填**, 同层 unique |
| `label` | `ReactNode` | **必填**, 显示内容 |
| `children` | `CascaderOption[]` | 子节点 (有则为 branch, 无则为 leaf) |
| `disabled` | `boolean` | 禁用此项 |

---

## 5. 场景示例

### 5.1 基础 — 国家/省/市
```tsx
const regions: CascaderOption[] = [
  { value: 'sg', label: 'Singapore', children: [
    { value: 'central', label: 'Central Region', children: [
      { value: 'orchard', label: 'Orchard' },
      { value: 'marina',  label: 'Marina Bay' },
    ]},
  ]},
];

<Cascader options={regions} placeholder="Select region" clearable />
```

### 5.2 受控
```tsx
const [region, setRegion] = useState<string[]>([]);

<Cascader
  options={regions}
  value={region}
  onChange={(value, path) => {
    setRegion(value);
    console.log('Selected:', path.map(o => o.label).join(' / '));
  }}
/>
```

### 5.3 Hover 触发 (快速选)
```tsx
<Cascader options={categoryTree} expandTrigger="hover" />
```

### 5.4 表单字段
```tsx
<form>
  <label>Shipping Region <span style={{ color: 'red' }}>*</span></label>
  <Cascader
    options={regions}
    value={form.region}
    onChange={(v) => setForm({ ...form, region: v })}
    placeholder="Select region"
  />
</form>
```

### 5.5 Disabled
```tsx
<Cascader
  options={regions}
  defaultValue={['sg', 'central']}
  disabled
/>
```

### 5.6 自定义分隔
```tsx
<Cascader options={tree} defaultValue={['a','b','c']} displaySeparator=" > " />
// → "A > B > C"
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| Trigger 高 | 32px | `--Cascader-triggerHeight` |
| Trigger padding | 7px 12px | `--Cascader-triggerPaddingBlock/Inline` |
| Trigger gap (text↔chevron) | 12px | `--Cascader-triggerGap` |
| Trigger border-radius | 4px | `--Cascader-triggerBorderRadius` |
| Trigger border default | `#E5E5E5` | `--Cascader-colorTriggerBorder` |
| Trigger border focus | `#EE4D2D` (橙) | `--Cascader-colorTriggerBorderFocus` |
| Trigger placeholder | `#B7B7B7` | `--Cascader-colorTriggerPlaceholder` |
| Trigger value | `#333333` | `--Cascader-colorText` |
| Trigger disabled bg | `#F6F6F6` | `--Cascader-colorTriggerBgDisabled` |
| Item 高 | 32px | `--Cascader-itemHeight` |
| Item padding | 7px 12px (旧库扒) | `--Cascader-itemPaddingBlock/Inline` |
| Item gap (text↔arrow) | 8px | `--Cascader-itemGap` |
| Item font / LH | 14px / 18px | `--Cascader-itemFontSize/LineHeight` |
| Item hover bg | `#F5F5F5` (4% 黑) | `--Cascader-colorBgHover` |
| Item selected color | `#EE4D2D` + Medium | `--Cascader-colorTextSelected` |
| Column 宽 / 最小宽 | 180 / 120 px | `--Cascader-columnWidth/MinWidth` |
| Column padding-block | 8px | `--Cascader-columnPaddingBlock` |
| Column 分隔线 | 1px `#E5E5E5` | (CSS 内联) |
| Menu border-radius | 4px | `--Cascader-menuBorderRadius` |
| Menu shadow (旧库 Effect radius 16) | 2 层 | `--Cascader-menuShadow` |
| Icon size (arrow-right / arrow-down) | 16px | `--Cascader-iconSize` |

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `options` 每渲染都新引用 | `useMemo` 包装 | 否则位置/列重算频繁 |
| `value` 传 string (单值) | 必须 `string[]` (path) | Cascader 本质是路径选择 |
| 没传 onChange 又用 `value` 受控 | 加 `onChange` 或改用 `defaultValue` | 受控不更新 = bug |
| Branch leaf 混乱 (有 children=[] 当 branch) | `children` 为 `undefined` 或缺省时才是 leaf | 空数组也会被当 branch 显示 `>` |
| 嵌套 5+ 层 | 限 3-4 层, 否则改用 Tree | 多列横向滚动体验差 |
| `displaySeparator` 设过长 | 默认 ' / ' 简短 | 占空间, trigger 容易溢出 |
| 用 Cascader 选择单层 | 用 Dropdown / Select | Cascader 设计为多级 |
| 把 disabled 设在 leaf 上但 parent 不 disable | 整条 path disable 或分组 grayout | 半禁用状态用户混淆 |
| 自画 arrow / chevron / clear icon | 用 `<Icon name="arrow-right" />` 等 | 铁律 #8 |

---

## 8. Accessibility

- Trigger: `role="combobox"`, `aria-expanded`, `tabIndex` 0 (disabled=-1)
- Menu: `role="listbox"`
- Column: `role="group"`
- Item: `role="option"`, `aria-selected`, `disabled` 同步 HTML
- 键盘:
  - Tab 进入 trigger
  - Enter / Space 打开 menu
  - Esc 关闭
  - Tab 在 item 间走焦点
  - Enter 选中 (button 默认)

未来增强 (TODO):
- 上下方向键导航 + 自动 focus 第一项
- 左右方向键切换列
- 输入字母快速跳到对应 item (typeahead)
- 远程懒加载 (loadData prop)
- search 模式 (filter options)

---

## 9. 历史变更

- **2026-06-05 v1** — Phase 5 首版
  - 4 ComponentSet (Item 8 + Menu 1 + Trigger 12 + 组合 1)
  - React Cascader 完整: trigger + Portal popup + 多列动态计算
  - resolvePath + computeColumns 内部算法
  - 4 placement (含 viewport clamping)
  - click / hover expand trigger 双 mode
  - 受控 + 非受控
  - Esc + click-outside 关闭
  - 19 Token 全绑定 (12 Component + 7 Global) + Trigger 9 token 新增
  - 严格旧库 design context 扒值 (padding 7/12, gap 8, LH 18, Medium for selected)
