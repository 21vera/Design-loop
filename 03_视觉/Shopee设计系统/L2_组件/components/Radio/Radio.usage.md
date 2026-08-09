# Radio 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注，禁止脑补）：
> - **主**：旧 Shopee Guidelines [GP-Radio 节点 40:47426](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=40-47426) —— 5 状态规格 + 业务变体清单
> - **辅**：旧 Vue `Shopee前端组件源码/components/radio/` —— props 命名 + Group 行为
> - **System Test**：[Radio ComponentSet 节点 840:26](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=840-26) + [Display 排版 842:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=842-2) （7 个 State 变体，全部 Token 绑定）
>
> 跨组件惯例见 [`../../../L3_全局规范/全局规范.md`](../../../L3_全局规范/全局规范.md)。

---

## 0. 依据来源映射（防越界）

| Prop | 来源等级 | 证据 |
|---|---|---|
| `value` | ✅ Tier 2 旧 Vue | EdsRadio `value` prop |
| `checked` / `defaultChecked` | ✅ Tier 1 React 标准 | 受控/非受控双模式 |
| `onChange` | ✅ Tier 2 旧 Vue | `@change` 事件 |
| `disabled` | ✅ Tier 2 旧 Vue | EdsRadio `disabled` |
| `name` | ✅ Tier 2 旧 Vue + HTML | radio group 必需 |
| `children` (label) | ✅ Tier 2 旧 Vue | slot default |
| `description` | ✅ Tier 2 旧 Guidelines | 「单选带说明文案」明确变体 |
| `direction` | ✅ Tier 2 旧 Vue | `layout` (改名更贴 React 习惯) |
| `options` | ✅ Tier 2 数据驱动等价写法 | 与 children 共存, Seller Center 表单常用 |
| `enableArrowNav` | ⚠️ Tier 4 → 用户已签字 | 默认 false, opt-in 才开 |
| :hover / :focus-visible / :active / :disabled | ✅ Tier 3 状态补齐 | 旧规范明确 5 状态规格 |

**丢弃项**（来源不足或已 deprecated）：~~`size`~~ ~~`type=outline`~~ ~~`fixWidth`~~ ~~radio-button 按钮形态~~ ~~嵌 textarea 的二级操作~~。

---

## 1. 总览

- **组件名**：`Radio` + `RadioGroup`
- **用途**：在多个备选值中**只能选一个**（与 Checkbox 区别：多选用 Checkbox）
- **导入**：
  ```ts
  import { Radio, RadioGroup, type RadioProps, type RadioGroupProps, type RadioOption } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Radio`
- **Code Connect**：Radio.figma.tsx（占位映射，等设计师建组件后再绑 nodeId）

---

## 2. 决策树（AI 必读）

```
用户需要从一组备选项里选 1 个?

├─ 备选项 ≥ 2 个 → 用 RadioGroup 包住, 强制互斥
│    ├─ 选项是固定枚举 (语言/币种/支付方式...) → 用 options 数组
│    │    <RadioGroup options={[{label, value}]} value={x} onChange={setX} />
│    └─ 选项需要自定义渲染 (混入 icon / 自定义副文本结构) → 用 children
│         <RadioGroup value={x} onChange={setX}>
│           <Radio value="a">A</Radio>
│           <Radio value="b" description="副说明">B</Radio>
│         </RadioGroup>
│
└─ 只有 1 个 boolean 开关 → 用 Switch / Checkbox, 不用 Radio

横排 vs 竖排?
├─ 选项 ≤ 4 个 + label 短 → direction="horizontal" (24px 间距, 默认)
└─ 选项 ≥ 5 个 或 任一带 description → direction="vertical" (16px 间距, 易扫读)

需要副文本?
├─ 是 → description prop (12px, 副字色)
└─ 否 → 只传 children

需要键盘方向键导航?
├─ 是 → enableArrowNav (opt-in, ARIA radiogroup 标准)
└─ 默认关 → 原生 Tab 行为
```

---

## 3. Props 完整签名

### `Radio`

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `value` | `string \| number` | — (必填) | 选项值, 与 Group value 比对判定 checked |
| `checked` | `boolean` | — | 受控模式. 嵌 Group 时由 Group 控制, 不需要传 |
| `defaultChecked` | `boolean` | `false` | 非受控初始值 |
| `onChange` | `(e: ChangeEvent) => void` | — | 变化回调 |
| `disabled` | `boolean` | `false` | 禁用. Group disabled 与此取或 |
| `children` | `ReactNode` | — | label 主文本 |
| `description` | `ReactNode` | — | 副文本 (12px, 副字色) |
| `name` | `string` | — | 嵌 Group 时由 Group 注入 |

### `RadioGroup`

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `value` | `string \| number` | — | 受控当前值 |
| `defaultValue` | `string \| number` | — | 非受控初始值 |
| `onChange` | `(value, e) => void` | — | 选项变化回调 |
| `options` | `RadioOption[]` | — | 数据写法 (与 children 互斥) |
| `name` | `string` | auto | 共享 name (HTML radio group 必需), 不传自动生成 |
| `disabled` | `boolean` | `false` | 整组禁用 |
| `direction` | `'horizontal' \| 'vertical'` | `'horizontal'` | 排版方向 |
| `enableArrowNav` | `boolean` | `false` | 方向键导航 (ARIA radiogroup) |
| `children` | `ReactNode` | — | 一组 `<Radio/>` |

### `RadioOption`

```ts
interface RadioOption {
  value: string | number;
  label: ReactNode;
  description?: ReactNode;
  disabled?: boolean;
}
```

---

## 4. 视觉规格速查（旧 Guidelines 1:1）

| 项 | 值 | Token |
|---|---|---|
| 指示器 (圆框) | 16 × 16 px | `--Radio-indicatorSize` |
| 中心点 | 6 × 6 px | `--Radio-dotSize` |
| label 与 indicator 间距 | 8 px | `--Radio-labelGap` |
| label 字号 | 14 px | `--Radio-labelFontSize` |
| description 字号 | 12 px | `--Radio-descriptionFontSize` |
| RadioGroup 横排间距 | 24 px | `--Radio-groupGapHorizontal` |
| RadioGroup 竖排间距 | 16 px | `--Radio-groupGapVertical` |
| 边框宽度 | 1 px | `--Radio-borderWidth` |

### 5 状态色

| 状态 | bg | border | dot | 备注 |
|---|---|---|---|---|
| Normal | `colorBg` | `colorBorder` | hidden | — |
| Hover | `colorBg` | `colorBorderHover` (primary) | hidden | 仅未禁用未选 |
| Selected | `colorBgChecked` (primary) | `colorBorderChecked` | `colorDot` (白) | — |
| Disabled Unselected | `colorBgDisabled` | `colorBorderDisabled` | hidden | — |
| Disabled Selected | `colorBgCheckedDisabled` | 同 bg | 白 | + CSS opacity 0.5 |
| Focus-visible | 不变 | 不变 | 不变 | box-shadow 0 0 0 2px `colorOutlineFocus` |

---

## 5. Shopee 特有规则（旧 Guidelines 提取）

> 这些是从旧规范里**仍然适用**的业务智慧，不是凭空发明。

1. **横排间距 24px / 竖排间距 16px** —— 旧规范明确写在 `$radio-margin-horizontal` / `$radio-margin-vertical`，不要自己改
2. **label 字号 14px** —— 与 Body Regular 对齐，不要拍脑袋改 16px
3. **选项数量 ≥ 5 必须竖排** —— 旧规范"场景应用"里所有 ≥ 5 项的例子都竖排
4. **disabled + selected 用 50% opacity** —— 不是另起一个灰色变体，而是直接叠半透明（旧规范 Disabled Selected 项明确）
5. **focus 用 box-shadow 而不是 outline** —— 圆形 outline 在 Safari 会变方框，旧规范的做法用 box-shadow 0 0 0 2px primary

---

## 6. 场景示例

### 6.1 简单互斥选择（语言切换）

```tsx
const [lang, setLang] = useState<'en' | 'zh' | 'th'>('en');
<RadioGroup
  value={lang}
  onChange={(v) => setLang(v as 'en' | 'zh' | 'th')}
  options={[
    { value: 'en', label: 'English' },
    { value: 'zh', label: '中文' },
    { value: 'th', label: 'ภาษาไทย' },
  ]}
/>
```

### 6.2 支付方式（竖排 + 副文本）

```tsx
<RadioGroup
  direction="vertical"
  value={method}
  onChange={setMethod}
  options={[
    { value: 'card', label: 'Credit / Debit card', description: 'Visa, Mastercard, JCB' },
    { value: 'paypal', label: 'PayPal', description: 'Pay via PayPal account' },
    { value: 'wallet', label: 'ShopeePay', description: '1% cashback' },
    { value: 'cod', label: 'Cash on delivery', description: 'Pay when receiving', disabled: true },
  ]}
/>
```

### 6.3 单 Radio 独立使用（不放 Group）

```tsx
// 受控
<Radio value="agree" checked={agreed} onChange={(e) => setAgreed(e.target.checked)}>
  I agree to the terms
</Radio>

// 非受控
<Radio value="agree" defaultChecked>
  I agree to the terms
</Radio>
```

### 6.4 启用方向键导航（a11y 强化场景）

```tsx
<RadioGroup
  enableArrowNav   // 显式 opt-in
  value={x}
  onChange={setX}
  options={[...]}
/>
// 用法: Tab 进入 → ← → 或 ↑ ↓ 切换选项 (横排用 ←→, 竖排用 ↑↓)
```

### 6.5 整组禁用

```tsx
<RadioGroup disabled value={x} options={[...]} />
// 子 Radio 的 disabled 与此取或, 不需要每个再加 disabled
```

---

## 7. 组合模式

| 搭配组件 | 用法 |
|---|---|
| **Form.Item** | RadioGroup 作为 Form 字段, 提供 label / 校验信息 |
| **Card** | 卡片内的设置项常用 RadioGroup direction="vertical" |
| **Modal** | "选择类型"类弹窗用 RadioGroup options |
| **Tooltip** | 单个 Radio 加 Tooltip 解释（不要塞进 description）|

---

## 8. 反例（不要这么写）

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `<Radio>` 不放在 Group 里却需要互斥 | 多个 Radio 放进 `<RadioGroup/>` | 原生 radio 互斥需要共享 name |
| `<Radio disabled defaultChecked />` 写成普通灰色 | 用 token, 自动 50% opacity 主色 | 旧规范明确 Disabled+Selected 用半透明主色 |
| `<RadioGroup options={...}>` 又塞 children | 二选一 | 同时传时 options 优先, children 被忽略, 易困惑 |
| 给单个 Radio 加 `name` 想互斥 | 用 RadioGroup, 不要手动管 name | name 应由 Group 注入, 避免命名冲突 |
| 选项 8 个还横排 | direction="vertical" | 横排难扫读, 旧规范 ≥ 5 项都竖排 |
| description 写中文 (业务接入)  | demo 用英文, 业务用 i18n key | 组件库底层 i18n-neutral |
| `<RadioGroup>` 内混 `<Radio/>` 和 `<Checkbox/>` | 互斥用 Radio, 多选用 Checkbox | 语义错位, 用户预期被破坏 |

---

## 9. 与 Checkbox 的区别

| 维度 | Radio | Checkbox |
|---|---|---|
| 选中数量 | 单选 (1 个) | 多选 (0+ 个) |
| 视觉 | 圆形 | 方形 |
| 互斥 | 是 (同 name 内) | 否 |
| 必选 | 通常默认选中一个 | 通常默认全不选 |

---

## 10. 已知限制 / 后续 TODO

- ❌ 暂不支持**单选带二级操作**（嵌 textarea/input 的复杂变体, Phase 2.5 Tier 4 跳过, 等明确需求再加）
- ❌ 暂不支持 **radio-button 按钮风格**（用户 Phase 0 选择只做 Radio + Group）
- ✅ **System Test Figma ComponentSet 已建**（节点 840:26，7 个 State 变体），Code Connect 已绑定实际 nodeId
