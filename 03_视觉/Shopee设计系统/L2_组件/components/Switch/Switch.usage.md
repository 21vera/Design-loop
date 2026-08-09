# Switch 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注）：
> - **主**：旧 Shopee Guidelines [GP-Switch 节点 40:53157](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=40-53157) — 2 类型 + 4 状态规格
> - **辅**：旧 Vue `Shopee前端组件源码/components/switch/` — `loading` / `activeText` 等 prop
> - **旧库精确数值**：[节点 4131:326](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/?node-id=4131-326) — 带文字开关 "on"/"off" 12px Roboto 精确位置
> - **System Test**：[ComponentSet 864:51](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=864-51) + [Display 865:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=865-2) — 21 变体，全部 Token

---

## 0. 依据来源映射（防越界）

| Prop | 来源等级 | 证据 |
|---|---|---|
| `checked` / `defaultChecked` / `onChange` | ✅ Tier 1 React 标准 | 受控/非受控 |
| `disabled` | ✅ Tier 2 旧 Vue + 旧 Guidelines | — |
| `loading` | ✅ Tier 2 旧 Vue | EdsSwitch `loading` prop |
| `size` (`default` / `small`) | ✅ Tier 2 旧 Vue + 旧 Guidelines | — |
| `checkedChildren` / `uncheckedChildren` | ✅ Tier 2 旧 Vue `activeText` / `inactiveText` 改 React 风格命名 | — |
| hover / focus-visible CSS | ✅ Tier 3 状态补齐 | — |

**丢弃项**：~~`size=large` / `x-large`~~（旧 Vue README + 旧 Guidelines 都已 deprecated）

**Figma 故意不画**：
- ❌ Loading variant — 运行时动效，Figma 是静态画板画不出旋转
- ❌ Small × WithText 变体组合 — 16px 高放不下文字，与旧库一致（笛卡尔积故意留空洞）

---

## 1. 总览

- **组件名**：`Switch`
- **用途**：二态切换（开/关），用于**立即生效**的设置开关
- **导入**：
  ```ts
  import { Switch, type SwitchProps } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Switch`
- **Code Connect**：Switch.figma.tsx

---

## 2. 决策树（AI 必读）

```
用户需要一个二态切换控件?
├─ 是 → Switch
│    ├─ 操作立即生效 (无需 Save 按钮) → Switch ✅
│    └─ 需要 Save / Confirm 二次确认 → 用 Checkbox + Save button (不要用 Switch)
│
├─ 在多个互斥选项中选一个 → Radio, 不是 Switch
├─ 多选, 0 或多个 → Checkbox, 不是 Switch
└─ 选项 ≥ 4 个 → 一组 Radio / 单选 Select, 不是一组 Switch

需要异步保存反馈?
├─ 是 → loading prop, 同时 disable 交互
└─ 否 → 普通 onChange

要不要开关内文字 "on"/"off"?
├─ 是 → size="default" + checkedChildren="on" + uncheckedChildren="off"
│    ⚠️ size="small" 不支持文字 (放不下)
└─ 否 → 不传 children

尺寸怎么选?
├─ 普通页面/设置 → size="default" (48×24, 默认)
└─ 表格行内/密集 UI → size="small" (32×16)
```

---

## 3. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `checked` | `boolean` | — | 受控模式 |
| `defaultChecked` | `boolean` | `false` | 非受控初始值 |
| `onChange` | `(checked, event) => void` | — | 变化回调，**第一个参数是 boolean** (与 React `<input>` onChange 区分) |
| `disabled` | `boolean` | `false` | 禁用 |
| `loading` | `boolean` | `false` | 加载中（自动禁用 + spinner 替换 dot） |
| `size` | `'default' \| 'small'` | `'default'` | 尺寸 |
| `checkedChildren` | `ReactNode` | — | 开 (checked) 时开关内显示的文字。**仅 default size 生效** |
| `uncheckedChildren` | `ReactNode` | — | 关时开关内显示的文字。**仅 default size 生效** |
| `aria-label` | `string` | — | 推荐传（无外部 label 时） |

---

## 4. 视觉规格速查（Figma 1:1）

| 项 | Default | Small | Token |
|---|---|---|---|
| 宽 × 高 | 48 × 24 | 32 × 16 | `--Switch-{size}Width/Height` |
| Dot 尺寸 | 20 | 12 | `--Switch-{size}DotSize` |
| Dot Padding | 2 | 2 | `--Switch-{size}DotPadding` |
| 内文字号 | 12 | — | `--Switch-{size}InnerLabelFontSize` |
| 内文位置 (On) | x=7 y=4 | — | (硬编码自旧库) |
| 内文位置 (Off) | x=25 y=5 | — | (硬编码自旧库) |
| 圆角 | height/2 | height/2 | (full-pill) |

### 颜色状态

| 状态 | bg | dot | Token |
|---|---|---|---|
| Off (Normal) | `colorTextQuaternary` (浅灰) | 白 | `--Switch-colorBgOff` |
| Off Hover | `colorTextTertiary` (深灰) | 白 | `--Switch-colorBgOffHover` |
| **On** | `colorSuccess` (绿) | 白 | `--Switch-colorBgOn` ⭐ |
| On Hover | `colorSuccessHover` | 白 | `--Switch-colorBgOnHover` |
| Disabled (任意) | 不变 + opacity 0.5 | 不变 | (旧规范明确) |
| Focus-visible | 不变 | 不变 | box-shadow 0 0 0 2px `colorOutlineFocus` |
| Loading | 不变 + opacity 0.5 | spinner (CSS animation 替换 dot) | — |

---

## 5. Shopee 特有规则

1. **⭐ 使用 `colorSuccess` 绿色而不是 `colorPrimary` 橙色**：Shopee Switch 一直用绿色 = "ON 表示已激活/同意"，与 Radio/Checkbox 选中态橙色截然不同。**不要替换成 primary！**
2. **小写文字** "on" / "off"（与旧库 4EgWXbFDmKLRpU0hdZeDh4 一致），不是大写
3. **Roboto Regular 12px** 字体（不是 Inter，硬编码）
4. **Small 不能带文字** —— 旧库根本没建这个变体，不要强加
5. **disabled 用 opacity 0.5** —— 旧规范明确，不换灰色 token
6. **Loading 转圈** —— 不画 Figma variant，代码 CSS `@keyframes` 实现

---

## 6. 场景示例

### 6.1 立即生效的设置项

```tsx
const [pushOn, setPushOn] = useState(true);
<Switch checked={pushOn} onChange={setPushOn} aria-label="Push notifications" />
```

### 6.2 异步保存（loading）

```tsx
const [enabled, setEnabled] = useState(false);
const [saving, setSaving] = useState(false);
const handleChange = async (next: boolean) => {
  setSaving(true);
  try {
    await api.updatePref({ enabled: next });
    setEnabled(next);
  } finally {
    setSaving(false);
  }
};
<Switch checked={enabled} loading={saving} onChange={handleChange} />
```

### 6.3 带文字开关（强引导）

```tsx
<Switch
  checked={mode === 'auto'}
  onChange={(next) => setMode(next ? 'auto' : 'manual')}
  checkedChildren="on"
  uncheckedChildren="off"
/>
```

### 6.4 密集 UI（表格行内 Small）

```tsx
<td>
  <Switch
    size="small"
    checked={row.enabled}
    onChange={(next) => updateRow(row.id, next)}
    aria-label={`Toggle ${row.name}`}
  />
</td>
```

### 6.5 整组禁用

```tsx
<>
  <Switch disabled checked />
  <Switch disabled />
</>
```

---

## 7. 组合模式

| 搭配组件 | 用法 |
|---|---|
| **Form** | Switch 作为 boolean 字段；表单不必有"Save"按钮，立即生效 |
| **Table** | size="small" 在行内做行级开关 |
| **Card** | Settings 卡片内多个 Switch 行（典型 Notification 偏好场景）|
| **Modal** | 在"高级选项"弹窗中用 |

---

## 8. 反例（不要这么写）

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `<Switch>` 后面跟 `<Button>Save</Button>` | 直接 `<Switch>`，立即生效 | Switch 语义就是"立即"；要 Save 用 Checkbox |
| `<Switch checkedChildren="开启" />` + `size="small"` | 去掉 children 或换 `size="default"` | Small 放不下文字 |
| `<Switch checked={loading ? prev : next} />` 用 loading 模拟 | `<Switch loading={true}>` 配合 prop | loading 自己会处理 disable + spinner |
| 把 Switch 当 Checkbox 用 (多选场景) | 用 Checkbox / CheckboxGroup | Switch 是二态，不是多选 |
| 4+ 个 Switch 表达互斥选项 (1 开 → 其他自动关) | 用 RadioGroup | 互斥逻辑会失控 |
| `<Switch size="large" />` | 用 `default` (砍了 large) | 旧 Vue README deprecated，新组件库不支持 |
| 给 children 传中文 (业务场景) | 用 i18n key，demo 用英文小写 "on"/"off" | 组件库 i18n-neutral |

---

## 9. 与 Checkbox / Radio 的区别

| 维度 | Switch | Checkbox | Radio |
|---|---|---|---|
| 选项数 | 二态 (开/关) | 0+ 多选 | 1 选 |
| 反馈时机 | **立即生效** | 通常配 Save 按钮 | 通常配 Save 按钮 |
| 主色 | **colorSuccess 绿** | colorPrimary 橙 | colorPrimary 橙 |
| 形状 | 椭圆胶囊 + 滑动 dot | 方形 圆角 2px | 圆形 |
| Loading | 内置 prop | 通常不需要 | 通常不需要 |

---

## 10. 已知限制 / 后续 TODO

- ❌ 不支持 `large` / `x-large` 尺寸（旧 Vue README + 旧 Guidelines 都标 deprecated）
- ❌ 不支持 `size="small"` + `checkedChildren` / `uncheckedChildren`（16px 高放不下，与旧库一致）
- ❌ checkedChildren / uncheckedChildren 只接受短文字（"on"/"off"/"yes"/"no"），不接受 ReactNode 内 SVG icon
