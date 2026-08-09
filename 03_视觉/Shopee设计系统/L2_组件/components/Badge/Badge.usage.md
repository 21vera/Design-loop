# Badge 组件用法（AI 调用指南）

> 写给 AI（Claude / Cursor / Codex）的"按这个调用就对了"的说明书。
>
> **依据来源**（Phase 2.5 Scope 契约逐项标注）：
> - **主**：旧 Shopee Guidelines [GP-Badges 节点 40:23859](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=40-23859) — 3 业务类型 + 视觉规格
> - **辅**：旧 Vue `Shopee前端组件源码/components/badge/` — `type / value / max / hidden`
> - **旧库精确数值**：[节点 4131:712](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/?node-id=4131-712) — 数字 / 文案 / Pulse 精确尺寸 + Roboto 字体
> - **System Test**：[ComponentSet 874:19](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=874-19) + [Display 875:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=875-2) — 8 变体（含 Pulse 静止帧）

---

## 0. 依据来源映射（防越界）

| Prop | 来源等级 | 证据 |
|---|---|---|
| `type: 'dot' \| 'pulse' \| 'new' \| 'hot' \| 'beta'` | ✅ Tier 2 旧 Vue 5 type | — |
| `count: number` (代替旧 `value`，React 风格) | ✅ Tier 2 旧 Vue + Tier 1 旧 Guidelines 数字徽标 | — |
| `max: number` (默认 99) | ✅ Tier 2 旧 Vue | — |
| `showZero: boolean` | ✅ Tier 3 状态补齐 (旧 Vue 默认隐藏 0，新增 prop 显式控制) | — |
| `hidden: boolean` | ✅ Tier 2 旧 Vue | — |
| `children: ReactNode` (anchor 锚点) | ✅ Tier 2 旧 Vue slot | — |
| Pulse CSS animation | ✅ Tier 2 旧 Vue keyframes | — |

**Figma 处理**：
- ✅ 8 个 variant 全部画了静止帧（含 Pulse 的"双圈"静止帧）
- ❌ 不画 Pulse 动画过程（动画交给 CSS @keyframes 1s ease-in-out infinite）

---

## 1. 总览

- **组件名**：`Badge`
- **用途**：醒目的提示标识，用于内容/功能的新增或变化提醒
- **导入**：
  ```ts
  import { Badge, type BadgeProps, type BadgeType } from '@shopee/design-system';
  ```
- **Storybook**：`Components/Badge`
- **Code Connect**：Badge.figma.tsx（8 个 variant mappings）

---

## 2. 决策树（AI 必读）

```
用户需要在某元素上提示有新内容/状态?
├─ 仅"有"或"无", 不显示数量 → type="dot" (小红点)
├─ 强提醒, 需要呼吸动画吸引注意 → type="pulse"
├─ 显示数量 (消息/订单/购物车) → count={n}
│    ├─ 普通: <Badge count={5}/>
│    └─ 超 99 显示 99+: <Badge count={150}/> (max 默认 99)
├─ 引导新功能 → type="new" / "hot" / "beta"
└─ standalone (不挂任何 anchor) → 不传 children

需要挂在 Icon / Avatar / Tab 上?
├─ 是 → 把 anchor 元素作为 children, Badge 自动定位右上角
└─ 否 → 不传 children, 徽标独立显示

count=0 时?
├─ 默认隐藏 (与旧 Vue 一致)
└─ 显式显示 → showZero={true}
```

---

## 3. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `type` | `'dot' \| 'pulse' \| 'new' \| 'hot' \| 'beta'` | `'dot'` | 徽标类型 |
| `count` | `number` | — | 数字 (传了即切到数字模式, 除 pulse/new/hot/beta 外) |
| `max` | `number` | `99` | count 上限 |
| `showZero` | `boolean` | `false` | count=0 时是否显示 |
| `hidden` | `boolean` | `false` | 显式隐藏 (anchor 仍渲染) |
| `children` | `ReactNode` | — | 锚点 (slot)；不传则 standalone |

**type 与 count 的关系**：
- `type='pulse'/'new'/'hot'/'beta'` 优先，count 被忽略
- `type='dot'` + 传 `count` → 显示数字
- `type='dot'` + 不传 `count` → 显示红点

---

## 4. 视觉规格速查（旧库 1:1）

| 类型 | 尺寸 | 字体 | 圆角 | 边框 |
|---|---|---|---|---|
| **dot** | 8×8 + 1px 白边 OUTSIDE → 视觉 10×10 | — | 50% | 1px white OUTSIDE |
| **pulse** | 16×16 (外圈 + 6×6 内点居中) | — | 50% | — |
| **count 1-digit** | 18×18 + 1px 白边 OUTSIDE | Roboto Regular **12px** | 9px (full pill) | 1px white OUTSIDE |
| **count 2-digit** | 22×18 | 同上 | 同上 | 同上 |
| **count overflow (99+)** | ~30×20 | 同上 | 10px | 同上 |
| **text (new/hot/beta)** | 28×16 | **Roboto Medium 10px** | tl/bl/br=9px, **tr=2px** | **无边框** |

### 颜色（全部 Token）

| 用途 | Token |
|---|---|
| Dot/Count 背景 | `--Badge-colorBg` (→ colorPrimary 橙) |
| 边框 (Dot/Count) | `--Badge-colorBorder` (→ colorBgContainer 白) |
| 文字 | `--Badge-colorText` (→ 白) |
| 文案徽标渐变起 | `--Badge-colorTextBadgeBgStart` (→ orange-5) |
| 文案徽标渐变止 | `--Badge-colorTextBadgeBgEnd` (→ colorPrimary) |
| Pulse 内点 | `--Badge-colorPulseInner` (→ colorPrimary) |
| Pulse 外圈 | `--Badge-colorPulseOuter` (→ colorPrimary, opacity 10%) |

---

## 5. Shopee 特有规则

1. **文案徽标圆角不对称** — `tl/bl/br = 9px, tr = 2px`（梯形效果，旧 Guidelines 明确）
2. **文案徽标用渐变** — `216deg, orange-5 → colorPrimary`（旧 Vue SCSS 一致）
3. **文案徽标无白边** — 与 Dot/Count 不同，Phase 4 用户手动确认
4. **Dot/Count 用 1px 白边 OUTSIDE** — `box-sizing: content-box`，让视觉尺寸 = token 尺寸 + 2px
5. **Pulse 外圈 opacity 10%** — `--Badge-pulseOuterOpacity: 0.1`
6. **Pulse 动画规格** — scale 1→2.6 + opacity 0.1→0 循环 1s ease-in-out infinite（旧 Vue keyframes 一致）

---

## 6. 场景示例

### 6.1 Header 通知中心（dot + count + pulse 混合）

```tsx
<header>
  <Badge type="dot">
    <Icon name="bell" size={24} />
  </Badge>
  <Badge count={messageCount}>
    <Icon name="message" size={24} />
  </Badge>
  <Badge count={orderCount} max={999}>
    <Icon name="order" size={24} />
  </Badge>
  <Badge type="pulse">
    <Icon name="alert" size={24} />  {/* 紧急告警, 呼吸吸引注意 */}
  </Badge>
</header>
```

### 6.2 Tab 引导新功能（type="new/hot/beta"）

```tsx
<TabList>
  <Tab>
    Marketing
    <Badge type="new" />  {/* 新功能 */}
  </Tab>
  <Tab>
    Discount Center
    <Badge type="hot" />  {/* 热门活动 */}
  </Tab>
  <Tab>
    AI Assistant
    <Badge type="beta" />  {/* 公测 */}
  </Tab>
</TabList>
```

### 6.3 Avatar 在线状态（dot 独立色或 pulse）

```tsx
<Badge type="dot">
  <Avatar src={user.avatar} />
</Badge>
```

### 6.4 购物车（count 0 时隐藏）

```tsx
<Badge count={cartItemCount}>  {/* count=0 自动隐藏 */}
  <Icon name="cart" />
</Badge>
```

### 6.5 显式控制隐藏（hidden）

```tsx
<Badge type="dot" hidden={!hasUnread}>
  <Icon name="bell" />
</Badge>
```

### 6.6 Standalone 独立徽标（不挂 anchor）

```tsx
{/* 表格行内显示状态 */}
<td>
  <Badge type="new" />  {/* 新条目 */}
</td>
<td>{order.id}</td>
```

---

## 7. 组合模式

| 搭配组件 | 用法 |
|---|---|
| **Icon** | Header 通知图标 + dot/count/pulse |
| **Avatar** | 在线状态点 / 未读数 |
| **Tab** | 新功能 / 热门 / Beta 引导 |
| **Tag** | Tag 内 standalone 文字 badge (强组合) |
| **Button** | Button 上挂 dot (不推荐, 视觉冲突) ⚠️ |

---

## 8. 反例（不要这么写）

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `<Badge count={0}>` 期望显示 0 | 加 `showZero` | 与旧 Vue + Ant Design 一致, 默认隐藏 0 |
| `<Badge type="new" count={5}>` 期望同时显示 New + 数字 | 选一种或拆成两个 Badge | type 优先, count 会被忽略 |
| 给 `<Button>` 挂 dot 形成"待办按钮" | 用 isLoading prop 或单独 Toast | 视觉冲突 |
| 用 dot 表示"重要" + dot 表示"未读" | dot 仅 1 个语义, 用 pulse 表"紧急" | 语义混淆 |
| `<Badge count={9999} max={9999}>` 显示完整 9999 | 用 max=999 + 实际值 | 大数字视觉占用太大 |
| 用 `<Badge type="hot">` 当 Tag 用 | 用 Tag 组件 | Badge 只是"提示标识", Tag 是"信息组件" |
| Pulse 动画在表格里 100 行 | 用 dot, 别用 pulse | 100 个动画严重影响性能 |

---

## 9. 与 Tag 的区别

| 维度 | Badge | Tag |
|---|---|---|
| 用途 | **提示标识** (有/无内容变化) | **信息组件** (分类/状态等元数据) |
| 形状 | 小红点 / 数字 / 短文案 (固定) | 大方形 (自由内容) |
| 内容 | dot / 1-3 位数 / "New"/"Hot"/"Beta" | 任意 ReactNode |
| 位置 | 通常挂 anchor 右上角 | 行内显示, 与文本同流 |
| 颜色 | 单一主色 (橙) | 多色 (10+ 业务态) |

---

## 10. 已知限制 / 后续 TODO

- ❌ 不支持 `color` / `status` prop（与 Ant Design 不同，Shopee Badge 只用主色橙）
- ❌ 不支持自定义文案 (只能 New/Hot/Beta，避免业务自由扩展导致风格不统一)
- ⚠️ Pulse 动画在大列表场景下需谨慎使用（每个 pulse = 一个 infinite animation）
- ✅ Phase 4 用户手动调整：Dot 边框 OUTSIDE / Text 无边框 / tr=2px，已同步到 Token CSS
