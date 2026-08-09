# Tag

> 状态标签 — **5 个语义状态** × Filled/Outline (Bordered)。设计系统只承载颜色语义，业务侧自由映射自己的业务词到 5 个语义之一。

## 1. 总览

- **组件名**: `Tag`
- **用途**: 行内状态/分类标识。商品、订单、活动、审核流等任何有"状态"语义的列表/卡片场景
- **导入**:
  ```ts
  import { Tag, type TagProps, type TagSemantic } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Tag`
- **Figma**:
  - [Tag ComponentSet (1181:41)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1181-41) — 10 variants (Semantic 5 × Bordered 2)
  - [Display (1182:21)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1182-21)
- **Code Connect**: ✅ 已映射 (`Tag.figma.tsx`)

**依据来源**:
- Tier 1: System Test ComponentSet `Tag` (1181:41) — 用户确认 5 语义维度
- Tier 2: 旧库 4131:670 (高 18px / padding 1×4 / borderRadius 2 精确还原)
- 旧 Vue 8 业务状态 (`unlisted` / `underReview` / ...) **已废弃** — 维度划分错: 8 个业务词实际只对应 5 个语义颜色 (Phase 2 错误重做)

---

## 2. 5 个语义状态 (核心要先记住)

| Semantic | 含义 | 颜色 | 业务示例 |
|---|---|---|---|
| `processing` | 进程中 / 进行中 | 蓝 `#2673DD` on `#E5EEFB` | Under Review · In Progress · In Transit |
| `approved` | 完成 / 激活 / 通过 | 绿 `#30B566` on `#EBF9EF` | Approved · Live · Delivered · Active |
| `pending` | 暂停 / 待处理 / 需用户操作 | 黄 `#EDA500` on `#FEF6F5` | Pending Submission · Awaiting Payment · Draft |
| `rejected` | 异常 / 拒绝 / 严重错误 | 红 `#FF4742` on `#FFE9E8` | Rejected · Failed · Suspended (违规) |
| `cancelled` | 进程结束 / 终止 / 归档 | 灰 `#666666` on `#EEEEEE` | Cancelled · Expired · Archived · Closed |

**核心心态**: 业务侧的具体词（unlisted / soldOut / upcoming / paused / banned ...）由业务**自己映射**到这 5 个语义之一。设计系统不内置业务词表。

---

## 3. 决策树 (AI 必读)

```
要标识一个状态?
├─ 这个状态是"还在进行中 / 等待结果"? — Under Review / In Transit / Processing
│    → semantic="processing" (蓝)
├─ 这个状态是"完成了 / 成功 / 激活"? — Approved / Delivered / Active
│    → semantic="approved" (绿)
├─ 这个状态是"需要用户操作 / 等待用户输入 / 草稿"? — Pending / Draft / Awaiting Payment
│    → semantic="pending" (黄)
├─ 这个状态是"被拒 / 严重错误 / 违规"? — Rejected / Failed / Banned
│    → semantic="rejected" (红)
└─ 这个状态是"结束了 / 归档 / 取消 (正常或异常)"? — Cancelled / Expired / Archived
     → semantic="cancelled" (灰)

要边框还是实心?
├─ Filled (默认) — 业务列表里大多用这个, 视觉重
└─ Outline — 在深色/带 bg 的容器里, 用 bordered=true (白底 + 边)
```

---

## 4. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `semantic` | `'processing' \| 'approved' \| 'pending' \| 'rejected' \| 'cancelled'` | `'processing'` | 5 语义之一, 决定颜色 |
| `bordered` | `boolean` | `false` | true = Outline (白底+同色边), false = Filled (浅色底+深色字) |
| `icon` | `ReactNode` | — | 可选前置图标 (如 `<Icon name="time" size={12} />`) |
| `children` | `ReactNode` | 语义默认词 ("Processing" 等) | 业务自定义文字 — **优先于默认词** |

---

## 5. 场景示例 (3 类业务映射)

```tsx
// === 5.1 订单生命周期 ===
function OrderStatusTag({ order }: { order: Order }) {
  switch (order.state) {
    case 'in_transit':       return <Tag semantic="processing">In Transit</Tag>;
    case 'delivered':        return <Tag semantic="approved">Delivered</Tag>;
    case 'awaiting_payment': return <Tag semantic="pending">Awaiting Payment</Tag>;
    case 'failed':           return <Tag semantic="rejected">Failed</Tag>;
    case 'cancelled':        return <Tag semantic="cancelled">Cancelled</Tag>;
  }
}

// === 5.2 商品 listing ===
function ProductStatusTag({ product }: { product: Product }) {
  switch (product.state) {
    case 'reviewing': return <Tag semantic="processing">Under Review</Tag>;
    case 'live':      return <Tag semantic="approved">Live</Tag>;
    case 'draft':     return <Tag semantic="pending">Draft</Tag>;
    case 'suspended': return <Tag semantic="rejected">Suspended</Tag>;
    case 'archived':  return <Tag semantic="cancelled">Archived</Tag>;
  }
}

// === 5.3 营销活动 ===
function CampaignStatusTag({ campaign }: { campaign: Campaign }) {
  switch (campaign.state) {
    case 'upcoming':   return <Tag semantic="processing">Upcoming</Tag>;
    case 'active':     return <Tag semantic="approved">Active</Tag>;
    case 'needsAction':return <Tag semantic="pending">Pending Approval</Tag>;
    case 'rejected':   return <Tag semantic="rejected">Rejected</Tag>;
    case 'expired':    return <Tag semantic="cancelled">Expired</Tag>;
  }
}

// === 5.4 配合 Icon ===
<Tag semantic="approved" icon={<Icon name="success" size={12} />}>
  Approved
</Tag>

// === 5.5 Outline 模式 (深色容器内) ===
<div style={{ background: '#1B1B1F', padding: 16 }}>
  <Tag semantic="processing" bordered>Under Review</Tag>
</div>
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| 高 | 18px | (padding 1 + line-height 16 + padding 1) |
| Padding | 1px / 4px | `--Tag-paddingBlock`, `--Tag-paddingInline` |
| Icon-text 间距 | 4px | `--Tag-marginInline` |
| 字号 / 字重 | 12px Roboto Medium | `--Tag-fontSize` |
| 圆角 | 2px | `--Tag-borderRadius` |
| 边框 | 1px (仅 Bordered=true) | `--Tag-lineWidth` |

### 5 Semantic 色对

| Semantic | Filled bg | text/border |
|---|---|---|
| `processing` | `var(--Tag-processingBg)` → blue-1 | `var(--Tag-processingColor)` → blue-6 |
| `approved` | `var(--Tag-approvedBg)` → green-1 | `var(--Tag-approvedColor)` → green-7 |
| `pending` | `var(--Tag-pendingBg)` → orange-1 | `var(--Tag-pendingColor)` → yellow-7 |
| `rejected` | `var(--Tag-rejectedBg)` → red-1 | `var(--Tag-rejectedColor)` → red-6 |
| `cancelled` | `var(--Tag-cancelledBg)` → neutral-4 | `var(--Tag-cancelledColor)` → neutral-8 |

### Filled vs Outline

- **Filled** (`bordered={false}`): `bg = {semantic}Bg` (浅色), `text = {semantic}Color` (深色), 无 border
- **Outline** (`bordered={true}`): `bg = white`, `stroke = {semantic}Color`, `text = {semantic}Color` (描边和字同色)

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `<Tag semantic="new" />` | `<Badge type="new" />` | Tag 5 语义里没 "new"，Badge 才是徽标 |
| `<Tag>Active</Tag>` 不传 semantic | 必须传 semantic, 颜色才有意义 | semantic 决定视觉色, children 只是文字 |
| 在组件库内置 `unlisted` / `soldOut` 这种业务词 | 业务侧自己 switch 业务状态 → semantic | 设计系统不承载业务知识 |
| Outline 用别的颜色边 | 边色和字色必须同色 (semantic 决定) | Figma 强约束 |
| 一行放 5 个不同 Tag | 同区域 Tag ≤ 2 个 | 视觉噪音 |
| `<Tag semantic="approved" />` 表"成功消息" | 用 `<Toast>` / `<Alert>` 表通知 | Tag 是状态标记, 不是通知 |
| 自定义颜色 (style 改 bg) | 选最接近的 5 个语义之一 | 5 个语义已覆盖所有业务场景, 自定义打破一致性 |

---

## 8. 业务映射建议 (业务侧维护，不在设计系统)

业务 layer 自己定一个 `mapBusinessStatusToSemantic()` helper:

```ts
// business/order/statusMap.ts
import type { TagSemantic } from '@shopee/design-system';

export function orderStatusToSemantic(state: OrderState): TagSemantic {
  if (['in_transit', 'shipped', 'processing'].includes(state)) return 'processing';
  if (['delivered', 'paid'].includes(state))                    return 'approved';
  if (['awaiting_payment', 'awaiting_pickup'].includes(state))  return 'pending';
  if (['failed', 'rejected', 'returned'].includes(state))       return 'rejected';
  if (['cancelled', 'expired', 'archived'].includes(state))     return 'cancelled';
  return 'processing'; // fallback
}
```

每条业务线 (Order / Product / Campaign / Ad / User / ...) 自己维护一份映射表。

---

## 9. 历史变更

- **2026-06-03 v2** — **维度重做**: 从 8 业务状态 (unlisted/underReview/...) 重构为 5 语义状态 (processing/approved/pending/rejected/cancelled)。原因: 8 个业务词实际只对应 5 个语义颜色, Phase 2 维度划分错误。Property × Value Matrix 思路实战首例。
- **v1** (已废弃) — 8 业务 status 维度
