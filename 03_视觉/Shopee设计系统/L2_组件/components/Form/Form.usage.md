# Form 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**：
> - **主**：新 System Test Form / FormItem ComponentSet（[Form 1703:517](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1703-517) · [FormItem 1701:628](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1701-628)）
> - **辅**：旧 Shopee Guidelines GP-Form（[42:56883](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=42-56883)）— 提取「类型汇总」「组件元素三层」「视觉样式」等 Shopee 规则
> - **数值**：旧 Vue `EdsForm` / `EdsFormItem` 源码 SCSS（label 144 / gap 16 / 行距 24 等）
>
> 跨组件惯例见 [`../../../L3_全局规范/全局规范.md`](../../../L3_全局规范/全局规范.md)。

---

## 1. 总览

- **组件名**：`Form` + `FormItem`（复合组件）
- **用途**：组织一组输入控件，统一布局、标签、校验、提交。Form 是容器，FormItem 是字段项。
- **组成**：`<Form>`（标题层由业务自填）→ 多个 `<FormItem>`（label + 控件 slot + 错误信息 / 额外提示）→ 操作区（Button）。
- **导入**：`import { Form, FormItem, type FormRef } from '@shopee/design-system';`
- **Storybook**：`Components/Form`
- **Code Connect**：FormItem → 1701:628；Form → 1703:517

**Props 来源映射**（Phase 2.5 Scope 契约，无 Tier4 自创）：

| Prop | 来源 |
|------|------|
| `layout` / `labelPosition` / `size` / `showMessage` / `validateTrigger` / `labelWidth` | 旧 Vue `EdsForm` |
| `name`(prop) / `label` / `required` / `rules` / `span` / `extra` / `inlineLabel` | 旧 Vue `EdsFormItem` |
| `validate()` / `validateFields()` / `clearValidate()` / `clearValidateFields()` | 旧 Vue `EdsForm` methods（ref API） |

---

## 2. 决策树（AI 必读）

```
要排布一组输入控件？
│
├─ 常规页面表单（详情页 / 编辑页）?
│    → layout="horizontal"（默认, label 右对齐居左, label↔控件 16px）
│
├─ 在弹窗里 / 页面横向空间有限 / 需要左右对齐?
│    → layout="vertical"（label 在控件上方）
│
├─ 筛选条件 / 紧凑布局（一行多个字段）?
│    → layout="inline"（一行排布, 建议 ≤ 3 列, 单行→按钮水平 / 多行→按钮垂直）
│
└─ 需要多列对齐的复杂表单?
     → layout="grid" + 每个 FormItem 设 span（24 列栅格）

单个字段：
├─ 必填? → <FormItem required>（label 前红 *）
├─ 要校验? → 给 Form rules={{ field: [...] }} 或 FormItem rules={[...]}
├─ 要灰色帮助提示? → <FormItem extra="...">（错误信息下方）
└─ label 想贴在输入框边框上(搜索/筛选)? → <FormItem inlineLabel>（联结标签, Shopee 特有）
```

---

## 3. Props 完整签名

### Form

| Prop | 类型 | 默认 | 说明 |
|------|------|------|------|
| `model` | `Record<string, unknown>` | — | 表单数据对象（校验时读取） |
| `rules` | `FormRules` | — | 表单级校验规则，key = 字段 name |
| `layout` | `'horizontal' \| 'vertical' \| 'inline' \| 'grid'` | `'horizontal'` | 布局类型 |
| `labelPosition` | `'right' \| 'left' \| 'top'` | `'right'` | 标签位置（horizontal 生效） |
| `size` | `'small' \| 'normal' \| 'large'` | `'normal'` | 控件尺寸（24/32/40px） |
| `labelWidth` | `number \| string` | `144` | label 列宽 |
| `showMessage` | `boolean` | `true` | 是否显示错误信息 |
| `validateTrigger` | `'change' \| 'blur' \| ''` | `''` | 默认校验触发时机 |
| `gutter` | `number` | `16` | grid 列间距 |
| `onSubmit` | `(e) => void` | — | 提交回调（已 preventDefault） |
| `ref` | `FormRef` | — | 命令式 API（见下） |

**FormRef 命令式 API**：`validate()` / `validateFields(names)` / `clearValidate()` / `clearValidateFields(names)`，均返回 `Promise<{ valid, invalidFields }>`（清除类无返回）。

### FormItem

| Prop | 类型 | 默认 | 说明 |
|------|------|------|------|
| `name` | `string` | — | 字段 key（校验用，对应 model 键，支持 `a.b`） |
| `label` | `ReactNode` | — | 标签内容 |
| `required` | `boolean` | `false` | 必填（显示红 *） |
| `rules` | `FormRule \| FormRule[]` | — | 字段级规则，优先级高于 Form |
| `size` | `FormSize` | 继承 Form | 覆盖尺寸 |
| `labelPosition` | `FormLabelPosition` | 继承 Form | 覆盖标签位置 |
| `inlineLabel` | `boolean` | `false` | 联结标签（label 贴控件边框，Shopee 特有） |
| `span` | `number` | `24` | grid 列宽（1-24） |
| `extra` | `ReactNode` | — | 灰色帮助提示（错误信息下方） |
| `validateStatus` | `'default' \| 'error'` | — | 手动控制校验状态（不走内部校验时用） |
| `help` | `ReactNode` | — | 手动错误信息（配合 `validateStatus='error'`） |
| `showMessage` | `boolean` | 继承 Form | 是否显示该项错误信息 |

**FormRule**：`{ required?, message?, validator?(value, parentValue, model), trigger?, pattern?, min?, max? }`。`validator` 返回 `true` 通过，返回 `string` 作为错误信息。

---

## 4. 视觉规格速查

| 项 | 值 | Token |
|----|----|-------|
| label 列宽 / 最大宽 | 144 / 200px | `--Form-labelWidth` / `--Form-labelMaxWidth` |
| label ↔ 控件间距 | 16px | `--Form-labelGap` |
| 字段行距（margin-bottom） | 24px | `--Form-itemSpacing` |
| inline 组间 / 行间 | 24 / 16px | `--Form-inlineItemGap` / `--Form-inlineRowGap` |
| grid 列间距 | 16px | `--Form-gridGutter` |
| 控件行高 small/normal/large | 24 / 32 / 40px | `--Form-itemMinHeight*` |
| 必填 * | 红 12px, 右距 3px | `--Form-colorRequired` / `--Form-requiredFontSize` |
| 错误信息 | 红 12px, 上距 4px | `--Form-colorErrorMessage` / `--Form-messageFontSize` |
| extra 帮助 | 灰 12px, 上距 4px | `--Form-colorExtra` / `--Form-extraFontSize` |
| 联结标签 | 边框 + 左圆角 4, padding 12 | `--Form-colorJointBorder` / `--Form-jointBorderRadius` |

---

## 5. Shopee 特有规则（⭐ 从旧 Guidelines 提取）

1. **三层结构**：表单 = 标题层（标题文案 / 面包屑）+ 内容层（区域标题 / label / 控件）+ 操作层（主 + 次按钮）。
2. **一个表单尽量只有一个主操作按钮**（Submit/Save 用 `variant="primary"`，Cancel 用 `variant="default"`）—— 视觉焦点唯一。
3. **label 最大宽 200px**：超长 label 自动换行并保持右对齐，不要让 label 撑破布局。
4. **控件在 32px 行高内垂直居中**：文本 / 开关 / 单选 / 复选 / 单行文本在表单中统一行高 32px。
5. **行内表单**：默认左对齐；输入项**建议 ≤ 3 列**；一行 n 列时按钮水平排布，n 行 n 列时按钮垂直排布。
6. **垂直分布**用于：弹窗内表单、页面横向空间有限、需要左右对齐的场景。
7. **联结标签（inlineLabel）** 仅用于带边框的控件（Input / Select / DatePicker），不用于 textarea。

---

## 6. 场景示例（Seller Center 真实用例）

```tsx
// 1) 商品编辑页 — 水平表单 + 校验
const ref = useRef<FormRef>(null);
<Form ref={ref} model={data} rules={{ name:[{required:true,message:'Product name is required'}] }} labelPosition="right">
  <FormItem name="name" label="Product Name" required>
    <Input value={data.name} onChange={v => setData(s => ({...s, name:v}))} placeholder="Set product name" />
  </FormItem>
  <FormItem name="price" label="Price" extra="The price must be more than 0.00">
    <Input value={data.price} onChange={v => setData(s => ({...s, price:v}))} prefix="$" placeholder="0.00" />
  </FormItem>
</Form>

// 2) 弹窗内表单 — 垂直分布
<Form layout="vertical">
  <FormItem name="addr" label="Address" required><Input /></FormItem>
</Form>

// 3) 列表筛选 — 行内表单
<Form layout="inline">
  <FormItem name="keyword" label="Keyword"><Input placeholder="Search" /></FormItem>
  <FormItem name="category" label="Category"><Input placeholder="Default" /></FormItem>
  <Button variant="primary">Submit</Button>
</Form>

// 4) 复杂表单 — 24 列栅格, 两列布局
<Form layout="grid" gutter={16}>
  <FormItem name="a" label="Field A" span={12} labelPosition="top"><Input /></FormItem>
  <FormItem name="b" label="Field B" span={12} labelPosition="top"><Input /></FormItem>
</Form>

// 5) 提交校验
const { valid, invalidFields } = await ref.current!.validate();
if (valid) submit(); else focusFirst(invalidFields);
```

---

## 7. 组合模式

- `Form × Input / Select / Cascader / DatePicker`：标准字段控件，直接作为 FormItem 的 children。
- `Form × Radio / Checkbox / Switch`：选项类控件，label 右对齐，控件在 32px 行高内居中。
- `Form × Button`：操作区，主按钮 `primary` + 次按钮 `default`，水平表单下按钮缩进对齐控件列（`paddingLeft = labelWidth + labelGap = 160`）。
- `Modal × Form(layout="vertical")`：弹窗内默认用垂直分布表单。

---

## 8. 反例（不要这样做）

| ❌ 错误 | 原因 | ✅ 正确 |
|--------|------|--------|
| 一个表单放 2 个 primary 按钮 | 视觉焦点不唯一 | 仅 1 个 primary，其余 default/outline |
| 行内表单排 5+ 列 | 太挤，可读性差 | 建议 ≤ 3 列，超出换 grid/horizontal |
| 自己写 `<label>` + `<input>` 拼字段 | 不走 Token / 校验 / 对齐 | 用 `<FormItem><Input/></FormItem>` |
| 用 `style={{color:'red'}}` 标必填 | 魔法值 | 用 `required`（自动绑 `--Form-colorRequired`） |
| textarea 用 `inlineLabel` | 联结标签只适配单行边框控件 | textarea 用普通 label |
| 错误信息自己画红字 | 与校验状态不同步 | 走 `rules` / `validateStatus` + `help` |
| label 写中文 demo | 组件库 i18n-neutral，demo 一律英文 | demo 用英文，业务层再 i18n |
