# Steps 组件用法（AI 调用指南）

> 写给 AI 的"按这个在 Figma 里调用就对了"的说明书。
>
> **依据来源**：
> - **主**：System Test 里的 Steps 组件 —— [Steps ComponentSet 1866:233](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1866-233) · [StepItem 1864:191](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1864-191)
> - **辅**：旧 Shopee Guidelines「NG-Step」类型汇总 + 旧 Vue `EdsSteps`/`EdsStep` props
> - **精确数值**：旧组件库 Figma `4121:570`（圈/点/线/字号/颜色全部从此扒取）
>
> 跨组件/页面级规则见 [../../../L3_全局规范/全局规范.md](../../../L3_全局规范/全局规范.md)。

## 1. 总览

- **Figma 组件名**：`Steps`（PascalCase）
- **node-id**：`1866:233`（Steps ComponentSet 根节点）
- **用途**：把一个任务拆成有序的若干步骤，展示**当前进度与各步状态**（已完成/进行中/等待）。一句话区分：Steps 表"线性流程进度"；`Tabs` 是平行切换、无先后；`Breadcrumb` 是层级位置、非进度。
- **变体维度**：`Type(Numbered/Dot/Icon) × Orientation(Horizontal/Vertical)` = 6 变体
- **复合层级（2 层，改下层 master 上层自动同步）**：
  - L1 原子 `StepItem`（[1864:191](https://www.figma.com/design/MHkEGIVKJpWrMK6peRHeN2/System-Test?node-id=1864-191)）= 指示器 + 标题 + 描述 + 尾部连接线
  - L2 `Steps`（1866:233）= 3 个 StepItem 拼成的进度条
- **依赖的基础组件**：`Icon`（Icon 类型用 shop/payment/shipping 等业务图标，24px）
- **Display**：`Steps — Display`（1873:594）· `StepItem — Display`（1875:517）

## 2. 何时用 / 何时不用

- ✅ 用 Steps：注册/下单/上架等**多步骤线性流程**的进度指示；横向用于页面顶部流程，竖向用于侧栏/详情时间线式流程。
- ❌ 不要用 Steps，改用别的：
  - 平行、无先后的内容切换 → 用 `Tabs`。
  - 表示页面层级位置 → 用 `Breadcrumb`。
  - 单纯的百分比/加载进度 → 用 `Progress`。

## 3. 决策树（AI 必读）

```
要展示线性流程进度?
├─ 指示器风格?
│  ├─ 带序号(1/2/3) → Type=Numbered
│  ├─ 仅圆点(轻量) → Type=Dot
│  └─ 业务图标(店铺/支付/物流) → Type=Icon  （instance Icon 库）
├─ 排列方向?
│  ├─ 顶部横向流程 → Orientation=Horizontal
│  └─ 侧栏/纵向流程 → Orientation=Vertical
每一步的状态(StepItem.Status)?
├─ 已完成 → Status=Finish   （橙实心指示器, 尾线橙）
├─ 进行中(当前) → Status=Process  （橙实心, 标题加粗 Medium, 尾线灰）
└─ 未开始 → Status=Wait     （灰描边/灰点, 灰字, 尾线灰）
每步要副说明? → StepItem Description = true
最后一步? → 隐藏其尾部连接线(isLast / connector.visible=false)
```

## 4. 变体属性契约（= Figma Component Properties，逐字对齐 Figma）

**Steps（根，1866:233）**

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `Type` | Variant | `Numbered` / `Dot` / `Icon` | Numbered | 指示器风格 |
| `Orientation` | Variant | `Horizontal` / `Vertical` | Horizontal | 排列方向 |

**StepItem（原子，1864:191）**

| 属性名 | 属性类型 | 可选值 | 默认 | 说明 |
|--------|---------|--------|------|------|
| `Type` | Variant | `Numbered` / `Dot` / `Icon` | Numbered | 指示器风格 |
| `Status` | Variant | `Finish` / `Process` / `Wait` | Process | 步骤状态 |
| `Orientation` | Variant | `Horizontal` / `Vertical` | Horizontal | 方向 |
| `Description` | Boolean | true / false | true | 是否显示副说明 |

> 末步连接线：在 Steps 里把最后一个 StepItem 实例的 `connector` 图层 `visible=false`（已在内置 6 变体中处理）。

## 5. 视觉规格（全部引用 Token）

| 维度 | 值 | Token |
|------|----|----|
| 数字圈 / 图标 | 24 | `Components/Steps/Component/indicatorSize` / `iconSize` |
| 圆点 | 10 | `dotSize` |
| 序号字号 | 14 Medium | `numberFontSize` |
| 标题字号 | 16（Process 用 Medium，余 Regular） | `titleFontSize` |
| 描述字号 | 14 | `descFontSize` |
| 连接线粗细 | 1 | `connectorThickness` |
| 连接线最小长 | 120 | `connectorMinLength` |
| 指示器-标题间距 | 8 | `itemGap` |
| 步骤间距 | 16 | `stepGap` |
| 激活色（Finish/Process 指示器 + 已完成线） | 橙 | `Global/colorActive` (→colorPrimary) |
| 序号白字 | 白 | `colorOnActive` (→colorTextLightSolid) |
| 标题色 | #333 | `colorTitle` (→colorText) |
| 等待色（Wait 指示器/字/未完成线） | #B7B7B7 | `colorWait` (→colorTextDisabled) |
| 描述色 | #666 | `colorDesc` (→colorTextSecondary) |

字体 Roboto（Process 标题 Medium，余 Regular）。

## 6. Shopee 特有规则（来自旧 Guidelines）

- **当前步（Process）标题加粗**（Medium），其余 Regular —— 强调"你在这一步"。
- **连接线颜色 = 前一步是否完成**：已完成步之后的线为橙，其余为灰（进度"填充"到当前）。
- **Numbered 的 Finish 与 Process 指示器同为橙底白字**（不显示对勾），区别只在标题粗细与后续连接线颜色（严格按旧库 4121:570）。
- **Icon 类型指示器用深灰/灰**（非橙）：Finish/Process 用 `colorTitle`，Wait 用 `colorWait`；图标必须 instance Icon 库，禁止自画。
- Vertical 适合步骤含较多说明文字的场景；Horizontal 适合顶部紧凑流程。

## 7. 组合模式

| 场景 | 本组件配置 | 配合组件 | 排布 |
|------|-----------|---------|------|
| 下单流程顶部 | Type=Numbered, Orientation=Horizontal | — | 页面内容上方通栏 |
| 物流进度 | Type=Icon, Orientation=Vertical | `Icon`(shipping 等) | 详情页侧栏 |
| 轻量引导 | Type=Dot, Orientation=Horizontal | — | 表单分段 |

## 8. 反例（AI 绝不能这样做）

| ❌ 错误 | ✅ 正确 | 原因 |
|---------|---------|------|
| 在 Steps 里裸画圆圈/线 | instance `StepItem` 原子 | 裸图形改 Token 不同步，破坏 2 层联动 |
| Icon 类型自画 SVG 图标 | instance Icon 库 master | 违反"不自创 icon"；尺寸/色不受 Token 管控 |
| 用对勾替换 Numbered 的 Finish 序号 | 保留橙底白序号 | 旧库 Numbered Finish 显示序号非对勾，要 1:1 |
| 所有步标题都加粗 | 仅 Process(当前)加粗 | 加粗用于标识"当前步"，全粗失去强调意义 |
| 连接线统一一种颜色 | 已完成段橙、未完成段灰 | 颜色表达进度填充，单色丢失进度信息 |
| 最后一步仍带尾部连接线 | 末步 connector 隐藏 | 末步后无下一步，留线视觉错误 |

## 9. Token 主题化

| 需求 | 改哪个 Token |
|------|-------------|
| 改激活/进度色 | `Components/Steps/Global/colorActive` |
| 改等待灰 | `colorWait` |
| 调指示器大小 | `indicatorSize` / `dotSize` |
| 调步骤间距 | `stepGap` |

## 10.（选填）动效 / a11y

- 步骤切换的高亮过渡由业务实现；Figma 不画过渡帧。
- a11y：用 `aria-current="step"` 标当前步，列表语义 `<ol>`，每步状态以文本/aria 暴露（非仅颜色）。

## 文档维护历史
- 2026-06-21：首次导入完成。2 ComponentSet（StepItem 18 = Type×Status×Orientation / Steps 6 = Type×Orientation）+ 15 token（10 Component + 5 Global）+ 2 Display。复用 Icon 库；连接线 done 橙/todo 灰、末步无线；Process 标题加粗；严格按旧库 4121:570 数值。
