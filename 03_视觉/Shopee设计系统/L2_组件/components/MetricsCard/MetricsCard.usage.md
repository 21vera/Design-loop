# MetricsCard

> 指标卡 / 数据卡 — Layer 1 atom · 4 axes × 16 variants

## 1. 总览

- **组件名**: `MetricsCard`
- **用途**: Dashboard / 报表页面顶部 KPI 卡 — 显示一个数值指标 (GMV / Sales / Orders / Visitors 等), 含可选 ⓘ 解释 / 环比变化 / 选中态
- **导入**: `import { MetricsCard } from '@shopee/design-system';`
- **Storybook**: `Components/MetricsCard`
- **Figma ComponentSet**: [MetricsCard (1577:171)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1577-171) — 16 variants
- **Figma Display**: [MetricsCard — Display (1588:175)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1588-175)
- **Code Connect**: ✅
- **来源**:
  - 设计规范 [Metrics Card 指标卡 (848:5591)](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/-New-Enterprise-Guideline?node-id=848-5591)
  - System Test 参考 [1522:11033](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1522-11033) (含 ⓘ 解释 icon + 顶部 4px 装饰色 bar)

---

## 2. 4 Axes × 16 Variants

| Axis | Values | 说明 |
|---|---|---|
| **Size** | `large` / `small` | 大: padding 16, value 22px / 小: padding 12, value 18px |
| **Selectable** | `no` / `yes` | yes 时顶部 4px 灰 bar; 已选中变彩 |
| **HasComparison** | `no` / `yes` | yes 时显示 `Vs Previous 30 Days: ▲ X%` (绿/红) |
| **HasExplanationIcon** | `no` / `yes` | yes 时 title 后跟 ⓘ help icon |

2 × 2 × 2 × 2 = **16 variants** (无 invalid)

---

## 3. Props 完整签名

| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `title` | `ReactNode` | — | 指标名称 (必填) |
| `value` | `ReactNode` | — | 数值 (必填) |
| `size` | `'large' \| 'small'` | `'large'` | 尺寸 |
| `explanation` | `ReactNode \| boolean` | — | ⓘ 解释 icon; 传字符串作 tooltip 文案 |
| `comparisonLabel` | `ReactNode` | — | 对比时间 e.g. "Vs Previous 30 Days:" |
| `changeValue` | `number` | — | 变化率 (e.g. 20.34 → ▲20.34% 绿, -19.73 → ▼19.73% 红) |
| `changeText` | `ReactNode` | — | 自定义 change 文案 (覆盖 changeValue) |
| `selectable` | `boolean` | `false` | 可选中 (顶部 bar + 点击交互) |
| `onClick` | `() => void` | — | 卡片点击 (selectable=true 时) |
| `isSelected` | `boolean` | `false` | 已选中态 (顶部 bar 变彩色) |
| `indicatorColor` | `string` | — | 选中时顶 bar 颜色 (默认橙 `colorPrimary`) |
| `onExplanationClick` | `() => void` | — | ⓘ icon 点击 (用于 tooltip 展开) |
| `className` | `string` | — | 自定义 |

---

## 4. 场景示例

### 4.1 基础单指标卡
```tsx
<MetricsCard title="GMV" value="$99,999.99" />
```

### 4.2 带环比变化
```tsx
<MetricsCard
  title="Orders"
  value="89,405"
  comparisonLabel="Vs Previous 30 Days:"
  changeValue={20.34}     // 正 → ▲ 绿
/>
```

### 4.3 带 ⓘ 解释 icon
```tsx
<MetricsCard
  title="GMV"
  value="$99,999.99"
  explanation="Gross Merchandise Volume in 30 days"
/>
```

### 4.4 可选中 (4 张卡组)
```tsx
const [selected, setSelected] = useState('sales');

const metrics = [
  { key: 'sales',    title: 'Sales',    value: '$31,085', change:  4.23, color: '#EE4D2D' },
  { key: 'orders',   title: 'Orders',   value: '89,405',  change:  0.73, color: '#FF6B35' },
  { key: 'visitors', title: 'Visitors', value: '30,059',  change:  3.22, color: '#3B7CC3' },
  { key: 'addon',    title: 'Add-on',   value: '6,726',   change: -1.5,  color: '#55CC77' },
];

<div style={{ display: 'flex', gap: 16 }}>
  {metrics.map(m => (
    <MetricsCard
      key={m.key}
      title={m.title}
      value={m.value}
      comparisonLabel="Vs Previous 30 Days:"
      changeValue={m.change}
      selectable
      isSelected={selected === m.key}
      onClick={() => setSelected(m.key)}
      indicatorColor={m.color}
    />
  ))}
</div>
```

### 4.5 小尺寸
```tsx
<MetricsCard size="small" title="ROI" value="3.5x" explanation="Return on Investment" />
```

---

## 5. 视觉规格 (1:1 Figma)

| 项 | 大尺寸 (large) | 小尺寸 (small) | Token |
|---|---|---|---|
| padding | 16px | 12px | `--MetricsCard-padding-{large/small}` |
| min-width | 200px | 160px | `--MetricsCard-minWidth-{large/small}` |
| title font-size | 14px Medium #333 | 14px Regular #999 | `--MetricsCard-titleFontWeight-{large/small}` / `titleColor-{large/small}` |
| value font-size | 22px Medium #333 | 18px Medium #333 | `--MetricsCard-valueFontSize-{large/small}` |
| corner-radius | 8px | 8px | `--MetricsCard-cornerRadius` |
| border | 1px #E5E5E5 | 1px #E5E5E5 | `--MetricsCard-border*` |
| top bar 高 | 4px (Selectable=yes) | 4px | `--MetricsCard-topBarHeight` |
| 未选中 bar | 灰 #B7B7B7 (neutral-6) | 同 | `--MetricsCard-topBarColorUnselected` |
| 已选中 bar | 橙 colorPrimary (业务可覆盖) | 同 | `--MetricsCard-topBarColorSelected` |
| ⓘ icon | 16×16 | 16×16 | `--MetricsCard-explanationIconSize` |
| ▲/▼ icon | 10×10 | 10×10 | `--MetricsCard-changeIconSize` |
| 上升色 | #30B566 (green-7 spec 精准) | 同 | `--MetricsCard-changeColorUp` |
| 下降色 | colorError (≈ #FF4742) | 同 | `--MetricsCard-changeColorDown` |

---

## 6. Icon 引用 (铁律 #8 + #10)

不自画, 全引用现有库:

| 用途 | React | Figma master |
|---|---|---|
| ⓘ 解释 | `<Icon name="question-mark" size={16} />` | 旧库 475:552 |
| ▲ 环比上升 | `<Icon name="index-up" size={10} />` | 旧库 475:590 (实心绿三角) |
| ▼ 环比下降 | `<Icon name="index-down" size={10} />` | 旧库 536:1562 (实心红三角) |

---

## 7. 反例

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 自画 close icon 标记可选中 | 用 topBar 灰/彩 区分 | 设计规范明示 (1522:11033 参考) |
| 用 arrow-up-s/arrow-down-s 当环比 icon | 用 index-up/index-down 实心三角 | 规范用实心三角, 描边箭头是"方向", 非"涨跌" |
| Selectable=yes + 没传 onClick | 同时传 | 用户期待点击切换 |
| selected 态用绿色 bar | 用 colorPrimary / 业务 indicatorColor | 一致性 |

---

## 8. Accessibility

- Card root: `role="button"` + `tabIndex={0}` + `aria-pressed` (selectable=true 时)
- ⓘ icon: `<button aria-label>` + title (作 tooltip)
- ▲/▼ icon: 装饰性 (含义在文字), 不影响 a11y

---

## 9. 历史变更

- **2026-06-09 v1**:
  - 首版 — Phase 0 → 6 全流程
  - **重做记录**: v0 (48 variants, Size×Sparkline×Comparison×Selectable×State) → v1 (16 variants, Size×Selectable×HasComparison×HasExplanationIcon)
  - 原因: v0 我自行加 Sparkline / blurred / 4-state 都没经用户确认, 违反铁律 #16 (Inventory 表逐格 URL 才能进 Phase 3)。重做后严格按用户 4-axis 矩阵
  - **Selectable 重做**: 旧版用 × close 标记可选中, 新版按用户规范用顶部 4px 灰/彩 bar (1522:11033 参考)
  - Icon 全部 instance 现有库 (475:552 question-mark, 475:590 index-up, 536:1562 index-down), 不自画
