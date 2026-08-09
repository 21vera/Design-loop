# Filter

> 筛选器 — 页面级 filter 工具栏, 2 mode + 自适应宽 + slot 子组件.

## 1. 总览

- **组件名**: `Filter`
- **用途**: 列表页 / 表格页顶部的筛选区域 — 多个 dropdown / input / datepicker 组合
- **导入**:
  ```ts
  import { Filter } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Filter`
- **Figma**: [Filter (1500:164)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1500-164) — 6 variants (Mode 2 × Count 3)
- **Code Connect**: ✅

**依据**: 设计规范 [4871:21314](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/-New-Enterprise-Guideline?node-id=4871-21314) (规范不全, 经细扒拼出全貌)

---

## 2. 2 Mode

| Mode | 触发条件 | 交互 | 视觉 |
|---|---|---|---|
| `realtime` (默认) | filter ≤ 3 | 改 filter 立刻触发 query, **无 Apply/Reset 按钮** | 等宽 1/2 (count=1, 占 1/2) / 1/2 + 1/2 (count=2) / 1/3 × 3 (count=3) |
| `manual` | filter > 3 | 点 Apply 触发 query, Reset 一键还原 | 收起态: 3 filter + Apply/Reset 同行; 展开态: filter wrap 3 列等宽 + 下方右对齐 actions |

---

## 3. 自适应宽规则 (用户重点要求)

- 根容器 `width: 100%` (FILL 父容器)
- 内部 grid `grid-template-columns: 1fr 1fr ...` → **每列等宽自动分配**
- 容器 200px / 800px / 1400px 任意宽都正确等分
- columns prop 影响 Realtime 的列数 (1/2/3)
- Manual mode 始终 3 列 wrap

---

## 4. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `mode` | `'realtime' \| 'manual'` | `'realtime'` | 2 mode |
| `children` | `ReactNode` | — | filter slot 节点 (业务方传 `<Dropdown/>` / `<Input/>` 等) |
| `columns` | `1 \| 2 \| 3` | `3` | 每行列数 (仅 realtime 模式) |
| `collapsed` | `boolean` | `false` | Manual 收起态 (仅 mode='manual') |
| `onToggleCollapsed` | `(c: boolean) => void` | — | 切换收起态 |
| `onApply` | `() => void` | — | Apply 点击 (仅 manual) |
| `onReset` | `() => void` | — | Reset 点击 (仅 manual) |
| `applyText` | `ReactNode` | `'Apply'` | Apply 文案 |
| `resetText` | `ReactNode` | `'Reset'` | Reset 文案 |
| `className` | `string` | — | 自定义 |
| `actionsClassName` | `string` | — | actions 行 class |

---

## 5. 场景示例

### 5.1 Realtime 实时筛选 (3 个 filter, 默认列宽)
```tsx
<Filter mode="realtime" columns={3}>
  <Dropdown trigger={<button>Category</button>} items={cats} />
  <Dropdown trigger={<button>Status</button>} items={statuses} />
  <Input placeholder="Search…" value={q} onChange={setQ} />
</Filter>
```

### 5.2 Realtime 1 filter (占 1/2 宽)
```tsx
<Filter mode="realtime" columns={1}>
  <Dropdown trigger={<button>Status</button>} items={statuses} />
</Filter>
```

### 5.3 Manual 复杂筛选 + 收起/展开
```tsx
const [collapsed, setCollapsed] = useState(true);

<Filter
  mode="manual"
  collapsed={collapsed}
  onToggleCollapsed={setCollapsed}
  onApply={() => refetch()}
  onReset={() => resetState()}
>
  <Dropdown ... /> {/* 6+ filter */}
  <Dropdown ... />
  ...
</Filter>
```

### 5.4 自定义 Apply/Reset 文案
```tsx
<Filter
  mode="manual"
  applyText="Search"
  resetText="Clear"
  onApply={handleSearch}
  onReset={handleClear}
>
  ...
</Filter>
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| 容器上下 padding | 16 | `--Filter-paddingBlock` |
| 同行 filter 间距 | 16 | `--Filter-columnGap` |
| 换行行间距 | 16 | `--Filter-rowGap` |
| filter ↔ actions 间距 | 24 | `--Filter-actionGap` |
| Apply ↔ Reset 间距 | 8 | `--Filter-buttonGap` |
| 每行最大列数 | 3 | `--Filter-maxColumns` |
| Apply Button | primary default | (Button 复用) |
| Reset Button | default default | (Button 复用) |

---

## 7. 反例

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 自画 Apply/Reset 按钮 | 用 `<Button variant="primary">` / `<Button variant="default">` | 铁律 #8 |
| filter slot 写死宽度 (px) | 让 grid `1fr` 等分 | 容器宽变化时不自适应 |
| mode='realtime' 加 Apply 按钮 | 该模式无 Apply (实时筛选) | 设计规范明确 |
| filter ≤ 3 用 mode='manual' | 用 'realtime' (无需 Apply) | 简化交互 |
| filter > 3 用 mode='realtime' | 用 'manual' (一次 query) | 减少 query 频次 |
| collapsed + mode='realtime' | collapsed 只在 manual 生效 | mode 决定 |

---

## 8. Accessibility

- Root: `role="region"` + `aria-label="Filters"`
- Apply / Reset: native `<button>` (来自 Button)
- Filter slots: 业务方传的 children 自带 a11y

---

## 9. 历史变更

- **2026-06-08 v1** — Phase 5 首版
  - 1 ComponentSet (Filter 6 variants: Mode 2 × Count 3)
  - React Filter: slot children + mode 自适应 layout
  - 6 token (paddingBlock/columnGap/rowGap/actionGap/buttonGap/maxColumns)
  - Storybook: Playground / RealtimeAllCounts / ManualToggle / RealWorld
  - 复用: `<Button>` (Apply primary + Reset default) — 铁律 #8
  - 自适应宽: CSS Grid `1fr` 等分 (容器多宽都自适应)
