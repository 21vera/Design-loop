# DatePicker

> 日期选择器 — 复合 4 层组件 (Trigger 复用 Input + cell 原子 + panel 面板 + popup 弹层)

## 0. 依据来源 (Phase 2.5 Scope 契约)

所有 props 来源映射 (无 Tier 4 凭空创造):

| Prop | 来源 | Tier |
|---|---|---|
| `type` / `size` / `disabled` / `clearable` / `format` / `shortcuts` / `showOverflowDate` / `fixed` / `rangeSeparator` / `startOfWeek` / `disabledDate` / `iconPlacement` | 旧 Vue `@eds-vue/date-picker` `types/index.d.ts` | T1/T2 |
| cell 状态 (hover/today/selected/in-range/disabled/out-of-month) | 旧 Vue `date-table.vue` + 旧库 Figma 353:20214 | T1 |
| `showFooter` (Confirm/Reset) | 旧库 3784:3427 | T2 |

**Scope** (用户签字): 7 type — `date` / `week` / `month` / `daterange` / `datetime` / `monthrange` / `yearrange` + 快捷侧栏 + Footer。**已降级删除**: `year` 单选、`datetimerange`、`size=small`(类型保留但旧库无独立 URL)。

## 1. 总览

- **用途**: 表单/筛选中选择单日、范围、月、年、日期+时间。
- **导入**: `import { DatePicker } from '@shopee/design-system'`
- **Storybook**: `Components/DatePicker`
- **Figma**: [System Test — DatePicker (1645:6671)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1645-6671)
- **Token**: `Components/DatePicker/*` (35 个) → `src/tokens/components/datepicker.tokens.css`

```tsx
<DatePicker type="date" onChange={(v) => console.log(v)} />
```

## 2. 嵌套架构 (4 层)

```
DatePicker (root)
 ├─ Trigger        ← 复用 Input 组件 (calendar prefix + value + clear)
 └─ Popup          ← 统一一层阴影
     ├─ ShortcutSidebar?   ← 快捷侧栏 (shortcuts)
     ├─ Panel(s)           ← DatePanel / MonthPanel / YearPanel
     │   ├─ Header         ← « ‹ Label › » (双箭头快速翻页)
     │   ├─ WeekdayRow
     │   └─ Grid → DayCell / MonthYearCell (原子, 9/7 状态)
     ├─ TimeColumn?        ← datetime: HH : MM 滚动
     └─ Footer?            ← Confirm / Reset (复用 Button)
```

## 3. 决策树 (AI 必读)

- 选**一天** → `type="date"`
- 选**一周** → `type="week"`
- 选**月份** → `type="month"`
- 选**日期+时间** → `type="datetime"` (自动带 Footer)
- 选**日期范围** → `type="daterange"` (双历, 连续淡橙带)
- 选**月份范围** → `type="monthrange"`
- 选**年份范围** → `type="yearrange"`
- 需要"最近 7 天"等快捷 → 传 `shortcuts`
- 需要禁用部分日期 → 传 `disabledDate={(d) => ...}`
- 受控 → 传 `value` + `onChange`; 非受控 → `defaultValue`

## 4. Props 完整签名

| Prop | 类型 | 默认 | 说明 |
|---|---|---|---|
| `type` | `DatePickerType` | `'date'` | 7 type, 见决策树 |
| `value` | `Date \| RangeDate \| null` | — | 受控值 (range 时为 `{startDate,endDate}`) |
| `defaultValue` | `Date \| RangeDate \| null` | `null` | 非受控初始值 |
| `onChange` | `(v) => void` | — | 变化回调 |
| `size` | `'small'\|'normal'\|'large'` | `'normal'` | 输入框尺寸 |
| `disabled` | `boolean` | `false` | 禁用 |
| `clearable` | `boolean` | `true` | hover 显示清空 |
| `format` | `string` | 按 type 推断 | 显示格式 (`DD/MM/YYYY` 等) |
| `placeholder` | `string` | = format | 占位符 |
| `shortcuts` | `DateShortcut[]` | — | 快捷侧栏 |
| `showOverflowDate` | `boolean` | `false` | 显示上/下月溢出日期 |
| `fixed` | `'start'\|'end'\|false` | `false` | 锁定范围一端 (range) |
| `startOfWeek` | `number` | `0` | 周起始 (0=日) |
| `disabledDate` | `(d:Date)=>boolean` | — | 禁用某天 |
| `iconPlacement` | `'prefix'\|'suffix'` | `'prefix'` | calendar icon 位置 |
| `showFooter` | `boolean` | datetime=`true` | 底部 Confirm/Reset |
| `appendToBody` | `boolean` | `true` | 弹层 portal 到 body |

```ts
interface RangeDate { startDate: Date | null; endDate: Date | null; }
interface DateShortcut { text: string; value: Date | RangeDate | (() => Date | RangeDate); }
```

## 5. 场景示例 (Seller Center)

```tsx
// 5.1 订单创建日期
<DatePicker type="date" placeholder="Select date" />

// 5.2 数据报表日期范围 + 快捷
<DatePicker
  type="daterange"
  shortcuts={[
    { text: 'Today', value: () => new Date() },
    { text: 'Last 7 Days', value: () => ({ startDate: minus(6), endDate: new Date() }) },
  ]}
/>

// 5.3 活动开始时间 (日期+时间)
<DatePicker type="datetime" />

// 5.4 财务对账月份范围
<DatePicker type="monthrange" />

// 5.5 受控 + 禁用未来日期
const [v, setV] = useState<Date | null>(null);
<DatePicker type="date" value={v} onChange={setV} disabledDate={(d) => d > new Date()} />

// 5.6 禁用态
<DatePicker type="date" disabled />
```

## 6. 视觉规格 (1:1 Figma · 旧库精确扒值)

| 项 | 值 | Token |
|---|---|---|
| 面板宽 | 272px | `--DatePicker-panelWidth` |
| 日 cell | 24×24, r4 | `--DatePicker-cellSize` / `cellRadius` |
| 月/年 cell | 72×24 | `--DatePicker-monthCellWidth` |
| Header 高 | 48px, 标题 16 Roboto Medium | `--DatePicker-headerHeight` |
| 面板阴影 | `0 8 16 .04` + `0 0 16 .10` (2 层) | `--DatePicker-panelShadow` |
| 选中底 | `#EE4D2D` 白字 | `--DatePicker-colorCellSelectedBg` |
| 今天 | 主橙字 + 橙点 | `--DatePicker-colorCellTodayText` |
| 区间带 | `colorPrimaryBg` (连续, 起止 solid 橙) | `--DatePicker-colorCellInRangeBg` |
| 非本月 | `#666` | `--DatePicker-colorTextOutOfMonth` |
| 禁用 | `colorTextDisabled` | `--DatePicker-colorCellDisabledText` |
| 导航箭头 | `#999`, hover `#333` | `--DatePicker-colorNavIcon` |

复用 (铁律 #8): Trigger=`<Input>` 视觉 · 翻页/calendar/clear=`<Icon>` · Footer=`<Button>`。

## 7. 组合模式

- **筛选栏**: 多个 DatePicker + `Filter` 组件组合。
- **表单字段**: 配 `label` + 校验; range 配合后端起止字段。
- **快速翻页**: header `«` `»` 跳年/十年, `‹` `›` 跳月。

## 8. 反例 (AI 不能这样做)

| ❌ | 原因 |
|---|---|
| 自画日历 cell / 输入框 | 必须复用 DayCell 结构 + Input 视觉 (铁律 #8) |
| range 用两个独立 DatePicker 拼 | 用 `type="daterange"` 单组件, 自带连续带逻辑 |
| 区间带做成独立圆角块 | 必须连续 (cell 无 gap + 满格底色), 起止才 solid 圆角 |
| datetime 时间用三列 HH MM SS | 旧库是 `HH : MM` 两列带冒号 |
| 给 `year` 单选 / `datetimerange` | 不在 scope (无旧库 URL, 已降级) |
| demo 字符串用中文 | 组件库 i18n-neutral, demo 一律英文 |

## 9. 历史变更

- **2026-06-10** v1 导入完成。Phase 1-6 全流程。35 token + 6 文件 + 4 ComponentSet (DayCell 9 / MonthYearCell 7 / Trigger 4 / DatePicker 7 type) + 3 Display。
  - 用户 review 修改: 快速翻页 `«»` icon (旧库 3784:1166)、范围连续淡橙带、Trigger 状态组件化、时间 HH:MM、下箭头去描边、合并弹层去接缝阴影。
