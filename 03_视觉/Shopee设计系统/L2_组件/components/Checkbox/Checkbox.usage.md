# Checkbox 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注，禁止脑补）：
> - **主**：旧 Shopee Guidelines [GP-Checkbox 节点 40:16118](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=40-16118) —— 9 状态规格 (含 Indeterminate) + 业务变体
> - **辅**：旧 Vue `Shopee前端组件源码/components/checkbox/` —— `indeterminate` prop + Group 行为
> - **旧库 vector**：勾号 path 抄自 [353:19797](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/?node-id=353-19793)，半选横杠 path 抄自 [353:19782](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/?node-id=353-19782)
> - **System Test**：[Checkbox ComponentSet 节点 850:34](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=850-34) + [Display 排版 851:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=851-2) — 9 个 State 变体，全部 Token 绑定

---

## 0. 依据来源映射（防越界）

| Prop | 来源等级 | 证据 |
|---|---|---|
| `value` | ✅ Tier 2 旧 Vue | EdsCheckbox `value` |
| `checked` / `defaultChecked` | ✅ Tier 1 React 标准 | 受控/非受控 |
| `indeterminate` | ✅ **Tier 1 双重证据** | 旧 Guidelines 明确画了 Indeterminate 状态 + 旧 Vue 有 `indeterminate` prop。**自动做，不让用户选。** |
| `onChange` | ✅ Tier 2 旧 Vue `@change` | — |
| `disabled` | ✅ Tier 2 旧 Vue | — |
| `name` | ✅ Tier 2 + HTML 标准 | — |
| `children` | ✅ Tier 2 旧 Vue slot | — |
| `description` | ✅ Tier 2 旧 Guidelines | — |
| `direction` | ✅ Tier 2 旧 Vue `layout` | — |
| `options` | ✅ Tier 2 数据驱动等价写法 | Radio 已批准同写法 |
| 5 状态 CSS（hover/focus/active/disabled）| ✅ Tier 3 状态补齐 | 旧规范明确 |

**丢弃项**（来源不足或 deprecated）：~~`acturalValue`~~ ~~`size`~~ ~~`type=outline`~~ ~~`fixWidth`~~ ~~enableArrowNav~~（用户明确不要）。

---

## 1. 总览

- **组件名**：`Checkbox` + `CheckboxGroup`
- **用途**：在多个备选项里**任意选 0+ 个**（与 Radio 区别：单选用 Radio）
- **关键区别于 Radio**：**方形** (圆角 2px) + 中心**勾号 / 横杠** + 支持 **indeterminate** 半选态
- **导入**：
  ```ts
  import { Checkbox, CheckboxGroup, type CheckboxProps, type CheckboxGroupProps, type CheckboxOption } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Checkbox`
- **Code Connect**：Checkbox.figma.tsx

---

## 2. 决策树（AI 必读）

```
用户需要从一组备选项里选 0+ 个?

├─ 是 → 用 Checkbox / CheckboxGroup
│    ├─ 选项是固定枚举 → options 数组
│    └─ 选项需要自定义 → children
│
├─ 只能选 1 个 → 用 Radio
└─ Boolean 开关 → 用 Switch

需要 indeterminate (半选) ?
├─ 是 (典型: 父子级"全选/全不选/部分选"; Table 表头多选)
│    → <Checkbox indeterminate={someButNotAll}/>
│    ⚠️ indeterminate 不替代 checked, 两者独立: 父项点击切换的是 checked, 视觉是 indeterminate
└─ 否 → 普通 Checkbox

横排 vs 竖排?
├─ 选项 ≤ 4 个 + label 短 → direction="horizontal" (24px 间距, 默认)
└─ 选项 ≥ 5 个 或 任一带 description → direction="vertical" (16px 间距)
```

---

## 3. Props 完整签名

### `Checkbox`

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `value` | `string \| number` | — | 选项值, Group 中用于匹配 value 数组 |
| `checked` | `boolean` | — | 受控. 嵌 Group 时由 Group 控制 |
| `defaultChecked` | `boolean` | `false` | 非受控初始值 |
| `indeterminate` | `boolean` | `false` | 半选态 (视觉, 不影响 checked) |
| `onChange` | `(e: ChangeEvent) => void` | — | 变化回调 |
| `disabled` | `boolean` | `false` | 禁用. Group disabled 与此取或 |
| `children` | `ReactNode` | — | label 主文本 |
| `description` | `ReactNode` | — | 副文本 (12px) |
| `name` | `string` | — | 嵌 Group 时由 Group 注入 |

### `CheckboxGroup`

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `value` | `(string \| number)[]` | — | 受控当前值数组 |
| `defaultValue` | `(string \| number)[]` | `[]` | 非受控初始值数组 |
| `onChange` | `(value, e) => void` | — | 选项变化回调 |
| `options` | `CheckboxOption[]` | — | 数据写法 (与 children 互斥) |
| `name` | `string` | auto | 共享 name |
| `disabled` | `boolean` | `false` | 整组禁用 |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | 排版方向 |
| `children` | `ReactNode` | — | 一组 `<Checkbox/>` |

### `CheckboxOption`

```ts
interface CheckboxOption {
  value: string | number;
  label: ReactNode;
  description?: ReactNode;
  disabled?: boolean;
}
```

---

## 4. 视觉规格速查（Figma 1:1）

| 项 | 值 | Token |
|---|---|---|
| 指示器 (方框) | 16 × 16 px | `--Checkbox-indicatorSize` |
| **圆角** | **2 px** ⭐ 区别 Radio 圆形 | `--Checkbox-borderRadius` |
| 中心勾号 / 横杠 | 12 × ~7.4 px / 10 × 2 px | `--Checkbox-checkmarkSize` |
| label 与 indicator 间距 | 8 px | `--Checkbox-labelGap` |
| label 字号 | 14 px | `--Checkbox-labelFontSize` |
| description 字号 | 12 px | `--Checkbox-descriptionFontSize` |
| Group 横排间距 | 24 px | `--Checkbox-groupGapHorizontal` |
| Group 竖排间距 | 16 px | `--Checkbox-groupGapVertical` |
| 边框宽度 | 1 px | `--Checkbox-borderWidth` |

### 9 状态色

| 状态 | bg | border | mark |
|---|---|---|---|
| Normal | `colorBg` | `colorBorder` | hidden |
| Hover | `colorBg` | `colorBorderHover` (primary) | hidden |
| Selected | `colorBgChecked` (primary) | `colorBorderChecked` | check vector |
| Selected Hover | `colorBgChecked` | `colorBorderHover` | check |
| **Indeterminate** | `colorBgChecked` | `colorBorderChecked` | **horizontal bar vector** |
| Disabled Unselected | `colorBgDisabled` | `colorBorderDisabled` | hidden |
| Disabled Selected | `colorBgCheckedDisabled` | 同 bg | check + **opacity 0.5** |
| Disabled Indeterminate | `colorBgCheckedDisabled` | 同 bg | bar + opacity 0.5 |
| Focus-visible | 不变 | 不变 | box-shadow 0 0 0 2px `colorOutlineFocus` |

---

## 5. Shopee 特有规则（旧 Guidelines 提取）

1. **横排 24px / 竖排 16px** —— 与 Radio 一致
2. **label 字号 14px** —— 与 Body Regular 对齐
3. **Indeterminate 不替代 Checked** —— 视觉表达"部分选中"，调用方点击后决定 checked 走向
4. **disabled + selected/indeterminate 用 50% opacity** —— 旧规范 Disabled Selected 项明确，**不要换成另一个灰色 token**
5. **方形圆角 2px** —— 与 Radio 圆形是关键区分

---

## 6. 场景示例

### 6.1 简单多选（Hobbies）

```tsx
const [checked, setChecked] = useState<string[]>(['reading']);
<CheckboxGroup
  value={checked}
  onChange={(v) => setChecked(v as string[])}
  options={[
    { value: 'watching-tv', label: 'Watching TV' },
    { value: 'reading', label: 'Reading' },
    { value: 'swimming', label: 'Swimming' },
    { value: 'singing', label: 'Singing' },
  ]}
/>
```

### 6.2 父子级 全选 / 半选 / 全不选 ⭐ Indeterminate 关键场景

```tsx
const all = ['watching-tv', 'reading', 'swimming', 'singing'];
const [checked, setChecked] = useState<string[]>(['watching-tv', 'reading']);

const allChecked = checked.length === all.length;
const someChecked = checked.length > 0 && !allChecked;

<>
  <Checkbox
    value="all"
    checked={allChecked}
    indeterminate={someChecked}
    onChange={(e) => setChecked(e.target.checked ? all : [])}
  >
    All hobbies
  </Checkbox>
  <div style={{ paddingLeft: 24 }}>
    <CheckboxGroup direction="vertical" value={checked} onChange={(v) => setChecked(v as string[])}>
      <Checkbox value="watching-tv">Watching TV</Checkbox>
      <Checkbox value="reading">Reading</Checkbox>
      <Checkbox value="swimming">Swimming</Checkbox>
      <Checkbox value="singing">Singing</Checkbox>
    </CheckboxGroup>
  </div>
</>
```

### 6.3 通知设置（竖排 + 副文本）

```tsx
<CheckboxGroup direction="vertical" value={prefs} onChange={setPrefs} options={[
  { value: 'email', label: 'Email notifications', description: 'Get product updates and tips' },
  { value: 'sms', label: 'SMS notifications', description: 'Receive shipping updates' },
  { value: 'push', label: 'Push notifications', description: 'In-app alerts' },
  { value: 'marketing', label: 'Marketing emails', description: 'Special offers', disabled: true },
]} />
```

### 6.4 单 Checkbox 独立使用

```tsx
// 用户协议同意
<Checkbox value="terms" checked={agreed} onChange={(e) => setAgreed(e.target.checked)}>
  I agree to the terms and conditions
</Checkbox>
```

### 6.5 Table 表头多选 (典型 indeterminate 场景)

```tsx
const total = rows.length;
const selectedCount = selectedIds.length;
const headerIndeterminate = selectedCount > 0 && selectedCount < total;
const headerChecked = selectedCount === total;

<th>
  <Checkbox
    value="all"
    checked={headerChecked}
    indeterminate={headerIndeterminate}
    onChange={(e) => setSelectedIds(e.target.checked ? rows.map(r => r.id) : [])}
    aria-label="Select all rows"
  />
</th>
```

---

## 7. 组合模式

| 搭配组件 | 用法 |
|---|---|
| **Form.Item** | CheckboxGroup 作为字段 |
| **Table** | 行选 / 表头多选 (用 indeterminate) |
| **Card** | 设置项内 CheckboxGroup direction="vertical" |
| **Tree** | 树形多选 (每节点用 indeterminate 表达"子节点部分选中") |

---

## 8. 反例（不要这么写）

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 多选用 `Radio` | 用 `Checkbox` | 语义错位 |
| 单选用 `Checkbox` 多选只允许 1 个 | 用 `Radio` | 互斥应该用 radio 原生 |
| `indeterminate` 当成 checked 的第三态 | 同时设 `checked` + `indeterminate` 各管各 | 它们是独立 prop |
| `<Checkbox indeterminate disabled defaultChecked />` 期望灰色横杠 | 用 token 自动处理 50% opacity | 旧规范明确 |
| 给单个 Checkbox 加 `name` 想互斥 | 用 Radio | Checkbox 不互斥 |
| 选项 8 个还横排 | direction="vertical" | 难扫读 |
| description 写中文 (业务接入)  | demo 英文, 业务用 i18n key | 组件库底层 i18n-neutral |

---

## 9. 与 Radio 的区别

| 维度 | Checkbox | Radio |
|---|---|---|
| 选中数量 | 0+ 个 (任意) | 1 个 |
| 视觉 | **方形 圆角 2px** | 圆形 |
| 中心标记 | **勾号 / 横杠 (SVG vector)** | 圆点 |
| 半选态 | ✅ 支持 `indeterminate` | ❌ 不支持 |
| 互斥 | 不互斥 | 同 name 内互斥 |
| Value 类型 | `string \| number`, Group 是数组 | `string \| number`, Group 是单值 |

---

## 10. 已知限制 / 后续 TODO

- ❌ 暂不支持**多选带二级操作**（嵌 textarea, Phase 2.5 Tier 4 跳过）
- ❌ 暂不支持 **CheckboxGroup `enableArrowNav`**（用户 Phase 0 不需要）
- ✅ **System Test Figma ComponentSet 已建** (节点 850:34, 9 状态), Code Connect 已绑实际 nodeId
