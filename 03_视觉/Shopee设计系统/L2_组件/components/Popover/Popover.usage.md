# Popover 组件用法（AI 调用指南）

> 写给 AI 的"按这个在 Figma 里调用就对了"的说明书。
>
> **依据来源**：
> - **主**：System Test 里的 Popover 组件（变体清晰、Token 完整）—— [Figma ComponentSet 1856:138](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1856-138)
> - **辅**：旧 Shopee Guidelines「FB-Popover」类型汇总 + 旧 Vue `EdsPopover` props（仅提取仍适用的 Shopee 规则）
> - **精确数值**：旧组件库 Figma `4131:964`（卡片/投影/箭头/字号全部从此扒取）
>
> 跨组件/页面级规则见 [../../../L3_全局规范/全局规范.md](../../../L3_全局规范/全局规范.md)。

## 1. 总览

- **Figma 组件名**：`Popover`（与 Figma 图层名完全一致，PascalCase）
- **node-id**：`1856:138`（Popover ComponentSet 根节点）
- **用途**：点击/悬停目标元素后弹出的**气泡卡片**，承载进一步解释、操作或图示。一句话区分：Popover 是**可承载操作/富内容**的浮层；纯文字短提示用 `Tooltip`（深色、无操作）；模态阻断式确认用 `Modal`。
- **变体维度**：`Type(4) × ArrowDirection(4)` = 16 变体
- **依赖的基础组件**：`Button`（344:144… 实为 104:4263，Action 类型的 Cancel/Confirm）· 图片槽（Image 类型，业务传入）
- **Display**：`Popover — Display`（1857:117）

## 2. 何时用 / 何时不用（When to use）

- ✅ 用 Popover：需要对目标元素**进一步解释/引导**（Basic/Link），需要**就地轻操作**（Action：确认/编辑），需要**图示说明**（Image）。
- ❌ 不要用 Popover，改用别的：
  - 纯文字、无操作的悬停提示 → 用 `Tooltip`（深色气泡，本组件只做 light 卡片）。
  - 需要阻断用户、必须响应的确认 → 用 `Modal`。
  - 选项列表/菜单 → 用 `Dropdown`。

## 3. 决策树（AI 必读）

```
要在目标元素旁弹出内容?
├─ 纯解释文字 → Type=Basic
├─ 文字 + 一个跳转/操作链接 → Type=Link
├─ 需要确认/取消等按钮操作 → Type=Action   （内置 Button: Cancel + Confirm）
└─ 需要配图说明 → Type=Image                （图 + 标题 + 文字）
气泡相对目标在哪个方向弹出(箭头指向目标)?
├─ 气泡在目标下方, 箭头朝上 → ArrowDirection=Top
├─ 气泡在目标上方, 箭头朝下 → ArrowDirection=Bottom   （最常用, baseline）
├─ 气泡在目标右侧, 箭头朝左 → ArrowDirection=Left
└─ 气泡在目标左侧, 箭头朝右 → ArrowDirection=Right
不需要箭头? → withArrow=No （prop）
气泡相对目标偏移对齐? → placement start/center/end （prop, 默认 center）
```

## 4. 变体属性契约（= Figma Component Properties，逐字对齐 Figma）

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `Type` | Variant | `Basic` / `Link` / `Action` / `Image` | Basic | 内容形态 |
| `ArrowDirection` | Variant | `Top` / `Bottom` / `Left` / `Right` | Bottom | 箭头所在边 + 指向（指向目标元素） |

> **prop（非变体）**：`withArrow`(yes/no，是否显示箭头)、`placement`(start/center/end 偏移对齐)、`content`(文本)。`theme` 固定 light（dark 深色气泡是 Tooltip 的职责）。

## 5. 视觉规格（全部引用 Token，不写死值）

| 维度 | 值 | Token |
|------|----|----|
| 卡片底色 | 白 | `Components/Popover/Global/colorBg` (→colorBgElevated) |
| 圆角 | 4 | `Components/Popover/Component/borderRadius` |
| 水平内边距 | 16 | `paddingInline` |
| 垂直内边距 | 12 | `paddingBlock` |
| 投影 | 2 层 `r16 y8 a.04` + `r16 y0 a.10` | （effect，按旧库；不绑 variable） |
| 箭头 | 12 × 6 白三角 | `arrowWidth` / `arrowHeight` |
| 正文 | 14 / 行高 20，#333 | `fontSize` / `lineHeight` / `colorText` |
| 标题 (Image) | 16 Medium，#333 | `titleFontSize` / `colorTitle` |
| 链接 (Link) | 蓝 | `colorLink` (→colorLink) |
| 宽度 Basic/Link | ≤280 (hug) | `maxWidth` |
| 宽度 Action/Image | 320 | `widthWide` |
| 图片高 (Image) | 140 | `imageHeight` |
| Action 文字-按钮间距 | 16 | `contentGapAction` |
| Image 图-文间距 | 8 | `contentGapImage` |

字体 Roboto Regular（标题 Medium）。

## 6. Shopee 特有规则（来自旧 Guidelines，⭐ 高价值）

- **气泡随页面滚动**：目标元素接近视口顶部时，气泡应翻转方向（flip）保持可见（旧 GP「场景示例」；运行时 Popper 行为）。
- 旧 GP 类型汇总只列 3 类（常规/嵌套操作/带图片）；旧库另补了 **LinkPopover**，本组件合并为 4 个 Type。
- 箭头**白色、无描边**，视觉上与卡片连为一体盖住投影接缝；不要给箭头单独加阴影或边框。
- Popover 是 **light 白卡**；深色短提示用 Tooltip，避免两者风格混用。
- Action 类型的按钮**靠右排列**，顺序 Cancel 在左、Confirm(Primary) 在右（与 Modal footer 一致）。

## 7. 组合模式

| 场景 | 本组件配置 | 配合组件 | 排布 |
|------|-----------|---------|------|
| 字段解释 | Type=Basic, ArrowDirection=Bottom | 触发：`Icon` question-mark / 文本 | 气泡在目标上方 |
| 引导跳转 | Type=Link | — | 文末蓝色 Link |
| 就地确认删除 | Type=Action | `Button` Cancel + Confirm | 按钮右对齐 |
| 图示说明 | Type=Image | 业务图片 | 图在上、标题+文在下 |

## 8. 反例（AI 绝不能这样做）

| ❌ 错误 | ✅ 正确 | 原因 |
|---------|---------|------|
| 给箭头加投影/描边 | 箭头纯白无 effect，卡片统一投影 | 箭头带阴影会出现"黑边"，破坏与卡片的连贯 |
| Action 里自画按钮 | instance `Button`(Type=Default/Primary, Size=Small) | 违反复用原则；自画按钮样式/状态不同步 |
| 用 Popover 做纯文字悬停提示 | 用 `Tooltip` | Popover 是承操作的 light 卡片，纯提示该用深色 Tooltip |
| 用 Popover 做必须响应的确认 | 用 `Modal` | Popover 非阻断，关键确认需模态 |
| 箭头方向与目标位置不符 | 箭头永远指向触发目标 | 箭头错向会让用户找不到来源元素 |
| 硬编码卡片颜色/圆角/间距 | 全部用 `Components/Popover/*` token | 破坏主题化与一致性 |

## 9. Token 主题化

| 需求 | 改哪个 Token |
|------|-------------|
| 改卡片圆角 | `Components/Popover/Component/borderRadius` |
| 改最大宽度 | `maxWidth` / `widthWide` |
| 改链接色 | `Components/Popover/Global/colorLink` |
| 改图片区高度 | `imageHeight` |

## 10.（选填）动效 / a11y

- 出现/消失淡入淡出、随滚动 flip 翻转、delay(200ms) 等运行时行为由业务实现（Popper），Figma 不画过渡帧。
- a11y：触发元素 `aria-haspopup`/`aria-expanded`，气泡 `role="dialog"`（Action 类）或 `role="tooltip"`（Basic），Esc 关闭。

## 文档维护历史
- 2026-06-21：首次导入完成。1 ComponentSet（16 变体：Type 4 × ArrowDirection 4）+ 17 token（13 Component + 4 Global）+ 1 Display。Light only；复用 Button（Action）；箭头无描边/无独立投影；严格按旧库 4131:964 数值。
