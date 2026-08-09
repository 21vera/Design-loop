# Modal

> 模态对话框 — Seller Center 标准 dialog 容器。**单层组件 + slot 模式**，复用 `<Button>` + `<Icon>`，严格按旧 Vue + 旧组件库 5 个 visual pattern 实现。

---

## 1. 总览

- **组件名**: `Modal`
- **用途**: 阻塞用户当前操作，要求做一次决策（确认/取消/告知）或承载一个独立任务（小型表单）
- **导入**:
  ```ts
  import { Modal, type ModalProps, type ModalSize, type ModalStatus } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Modal`
- **Figma**: [Modal ComponentSet (1139:442)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1139-442) · [Display](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1140-94)
- **Code Connect**: ✅ 已映射，见 `Modal.figma.tsx`

**依据来源**:
- Tier 2 (大头): 旧 Vue `EdsModal` 全部 props + 旧组件库 5 个 visual symbol
- Tier 3: focus trap / body scroll lock / Esc 关闭 / Portal / 状态补齐
- 复用 (铁律 #8): `<Button>` for footer buttons, `<Icon>` for close + 4 status icons (`close` / `success-s` / `error-s` / `notice-triangle-s` / `information-s`)
- T4 全部不加 (`hasBack` / `appendToBody` / `closeOnHashChange` / 命令式 API `Modal.confirm()`) — 业务有需求再说

---

## 2. 决策树 (AI 必读)

```
用户要什么交互?
├─ 单纯告知 (操作已完成 / 信息提示) — 不需要用户决策
│    → showCancel={false}  (单 OK 按钮的 Alert 模式)
│    → confirmText 可省 (自动 "OK")
│    └─ 配 status="success" | "info" 加 48px 图标 + 居中
│
├─ 需要二次确认 (删除 / 不可逆操作 / 离开未保存)
│    → showCancel + showConfirm (默认两个按钮)
│    → 危险操作: confirmText="Delete" + onConfirm 处理
│    └─ 配 status="warning" 加黄色三角图标 + 居中加强警示
│
├─ 操作失败 / 错误提示
│    → status="error" + showCancel={false} (单 OK)
│
└─ 录入数据 (小型表单, ≤ 5 字段)
     → 不传 status, 默认左对齐
     → children 放 <input>/<Select>/... 等
     → 复杂表单 (> 5 字段) 用 size="medium" 或 "large"
     → 真正复杂的整页表单 → 不要用 Modal, 用 Drawer 或单独路由页

需要多大?
├─ 一行字提示 / 单按钮 Alert → size="normal" (400, 默认)
├─ 含 2-3 字段表单 → size="medium" (500)
├─ 含 4-5 字段 / 表格预览 → size="large" (600)
└─ 含多列 / 多步流程 → size="x-large" (800, min-height 400)

需要关闭逃生路径吗?
├─ 关键操作不可误关 → closeOnEsc=false, closeOnClickMask=false (默认)
└─ 轻量提示/无后果 → closeOnEsc, closeOnClickMask 都开
```

---

## 3. Props 完整签名

| 名称 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| **控制** | | | |
| `open` | `boolean` | — | **必填** — 是否打开 |
| `onClose` | `() => void` | — | close icon / Esc / mask 触发 |
| `onConfirm` | `() => void \| Promise<unknown>` | — | 主按钮 Confirm 回调。返 Promise 时业务需配 `confirmLoading` |
| `onCancel` | `() => void` | 同 `onClose` | 次按钮 Cancel 回调 |
| **视觉** | | | |
| `title` | `ReactNode` | — | 标题 20px Roboto Medium |
| `subtitle` | `ReactNode` | — | 副标题 14px Roboto Regular gray-8 |
| `children` | `ReactNode` | — | Body 内容 |
| `status` | `'success' \| 'error' \| 'warning' \| 'info'` | — | 加顶部 48px 状态图标 + 内容居中 + body 字色变浅 |
| **尺寸** | | | |
| `size` | `'normal' \| 'medium' \| 'large' \| 'x-large'` | `'normal'` | 预设宽度 400/500/600/800 |
| `width` | `number` | — | 自定义宽度 (覆盖 size) |
| **Footer 按钮** | | | |
| `showClose` | `boolean` | `true` | 右上 X icon |
| `showCancel` | `boolean` | `true` | Cancel 按钮 |
| `showConfirm` | `boolean` | `true` | Confirm 按钮 |
| `confirmText` | `ReactNode` | `'Confirm'` (单按钮时 `'OK'`) | Confirm 文案 |
| `cancelText` | `ReactNode` | `'Cancel'` | Cancel 文案 |
| `confirmLoading` | `boolean` | `false` | Confirm 加载态 |
| `cancelLoading` | `boolean` | `false` | Cancel 加载态 |
| `confirmDisabled` | `boolean` | `false` | Confirm 禁用 |
| `cancelDisabled` | `boolean` | `false` | Cancel 禁用 |
| `footerAssist` | `ReactNode` | — | Footer 左侧辅助槽 (link/text) |
| `footer` | `ReactNode` | — | 整个 footer 覆盖 (传了之后 show*/confirmText 全部失效) |
| **交互** | | | |
| `closeOnEsc` | `boolean` | `false` | Esc 关闭 |
| `closeOnClickMask` | `boolean` | `false` | 点 mask 关闭 |
| `center` | `boolean` | `status` 存在时 `true` | 强制内容居中 |

> 💡 透传 HTML 属性: 任何 `HTMLAttributes<HTMLDivElement>` 都会传到内部 `.box` 元素（`id` / `aria-*` 等）。

---

## 4. 场景示例 (Seller Center 真实用例)

```tsx
// === 场景 1: 删除订单 (危险操作 + 二次确认) ===
const [open, setOpen] = useState(false);
<Button variant="primary" isDanger onClick={() => setOpen(true)}>Delete Order</Button>
<Modal
  open={open}
  onClose={() => setOpen(false)}
  onConfirm={async () => {
    await deleteOrder(orderId);
    setOpen(false);
  }}
  title="Delete this order?"
  confirmText="Delete"
>
  Order #SP240601001 will be permanently removed. This action cannot be undone.
</Modal>

// === 场景 2: 操作成功提示 (单按钮 Alert + status) ===
<Modal
  open={successOpen}
  onClose={() => setSuccessOpen(false)}
  onConfirm={() => setSuccessOpen(false)}
  status="success"
  showCancel={false}
  title="Successfully"
>
  You have successfully generated 10 pickup codes, now you can download these labels.
</Modal>

// === 场景 3: 操作失败 (error + 单按钮) ===
<Modal
  open={errorOpen}
  onClose={() => setErrorOpen(false)}
  onConfirm={() => setErrorOpen(false)}
  status="error"
  showCancel={false}
  title="Operation Failed"
>
  We could not generate the pickup codes. Please check your network and try again.
</Modal>

// === 场景 4: 离开未保存的提示 (warning) ===
<Modal
  open={leaveOpen}
  onClose={() => setLeaveOpen(false)}
  onConfirm={confirmLeave}
  onCancel={() => setLeaveOpen(false)}
  status="warning"
  title="Discard unsaved changes?"
  confirmText="Discard"
>
  Your account has unsaved drafts. Leaving now will discard them.
</Modal>

// === 场景 5: 新建地址表单 (medium size + form children) ===
<Modal
  open={addrOpen}
  onClose={() => setAddrOpen(false)}
  onConfirm={async () => {
    await saveAddress(form);
    setAddrOpen(false);
  }}
  size="medium"
  title="Add a New Address"
  confirmText="Save"
  confirmDisabled={!form.isValid}
>
  <form>
    <Input label="Address" placeholder="City / Country" />
    <Input label="Phone Number" placeholder="Number" />
    <Input label="Name" placeholder="Name" />
  </form>
</Modal>

// === 场景 6: 异步 confirm + loading ===
const [loading, setLoading] = useState(false);
<Modal
  open={open}
  onClose={() => !loading && setOpen(false)}
  onConfirm={async () => {
    setLoading(true);
    await submit();
    setLoading(false);
    setOpen(false);
  }}
  confirmLoading={loading}
  cancelDisabled={loading}
  title="Submit changes?"
>
  Submitting may take a few seconds.
</Modal>

// === 场景 7: 含辅助链接 (footer-assist) ===
<Modal
  open={open}
  onClose={() => setOpen(false)}
  onConfirm={() => setOpen(false)}
  title="Confirm payment"
  footerAssist={<a href="/help/payments" target="_blank">Need help?</a>}
>
  Total amount: $128.50 will be charged from your saved card.
</Modal>
```

---

## 5. 组合模式

| 模式 | Modal 角色 | 配合组件 |
|------|-----------|---------|
| **二次确认 + 主操作** | 中心容器 | `<Button isDanger>` 触发 + Modal 显示 + `<Button>` 内嵌 footer |
| **状态反馈** (success/error) | 状态容器 | `status` prop + `<Icon>` 自动 instance |
| **小型表单** | 表单容器 | `<Input>` / `<Select>` / `<Checkbox>` 等 form 字段嵌入 children |
| **多步流程** | 单步容器 | 配 `<Steps>` 横排顶部 + 业务侧控制 step 状态 + Modal 切 step content |
| **异步提交** | 处理容器 | `confirmLoading` + Promise-based `onConfirm` |

**关键约束**:
- Modal 不嵌 Modal (层级冲突 + a11y 灾难)。多步流程用 Steps 或 wizard 模式
- Modal 内不放 Drawer / Popover 等覆盖层 (会被 mask 遮蔽)
- 整页表单 (10+ 字段) **不应该用 Modal**，用独立 route 页面

---

## 6. 反例 (AI 绝不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---------|---------|------|
| 自己在 children 里写 `<button>Cancel</button>` | 用 `showCancel + cancelText="Cancel" + onCancel` | Modal 已有标准 footer 按钮组件 + 间距 + 顺序 + a11y, 自画的按钮跟 design token 脱节 |
| 用 `<svg>` 写状态图标 | 用 `status="success"` 自动 instance `<Icon name="success-s">` | 铁律 #8: 必须 instance 现有 icon, svg 颜色不会跟 token |
| Modal 嵌 Modal | 改用 wizard / Steps + 单 Modal 切内容 | 嵌套 Modal 导致 mask z-index 冲突 + focus trap 失效 + Esc 关错弹窗 |
| 关键操作 (删除) 设 `closeOnClickMask` | 默认 false 不开 | 用户点外面误操作 → 数据丢失。关键操作必须主动确认 |
| 把整页表单 (10+ 字段) 塞进 Modal | 改用独立 route 页面 | Modal 是"阻塞决策"，长表单不是决策、是录入，用 Modal 会破坏 a11y + scroll + 移动端体验 |
| `onConfirm` 不 await Promise 直接关 Modal | `await onConfirm()` 或自己设 `confirmLoading={true}` | 用户看不到加载态以为没响应；网络失败时业务无法回滚 UI |
| `size="x-large"` 但内容只有 1 行字 | 用 `size="normal"` | XLarge 设置了 min-height 400，单行内容会出现大片留白 |
| status 和 showClose 都开 | status + `showClose=false` (status modal 通常不给关) | 状态反馈完成时用户点 OK 才算确认收到信息；提供 X 反而暗示可忽略 |

---

## 7. Token 主题化

| 需求 | 改哪个 token |
|------|-------------|
| 4 个 size 宽度 | `--Modal-normalWidth` / `--Modal-mediumWidth` / `--Modal-largeWidth` / `--Modal-xLargeWidth` |
| Modal 上下/左右内边距 | `--Modal-paddingBlock` / `--Modal-paddingInline` (默认 24) |
| header → body 间距 | `--Modal-headerGap` (16) |
| body → footer 间距 | `--Modal-footerGap` (24) |
| Title 字号/行高 | `--Modal-titleFontSize` (20) / `--Modal-titleLineHeight` (28) |
| 圆角 | `--Modal-borderRadius` (4，旧 Vue 3，已升到现代 4) |
| 状态图标大小 | `--Modal-statusIconSize` (48，旧库实测) |
| Close icon 偏移 | `--Modal-closeIconOffset` (24，旧库实测) |
| 按钮间距 | `--Modal-buttonsGap` (8) |
| 弹窗背景 | `--Modal-colorBg` (`colorBgElevated`，白) |
| 蒙层颜色 | `--Modal-colorBgMask` (`colorBgMask`，黑 0.45) |
| Title 文字色 | `--Modal-colorTextTitle` (`colorTextHeading`，gray-10) |
| 4 个状态色 | `--Modal-colorStatusSuccess` / `Error` / `Warning` / `Info` |
| 阴影 | `--Modal-boxShadow` (旧库 2-layer: ambient + key) |

34 个 token 完整清单见 `src/tokens/components/modal.tokens.css`

---

## 8. 无障碍 (a11y)

- **role 与语义**:
  - `.box` 容器 `role="dialog" + aria-modal="true"`
  - title 自动 `id="modal-title"`，`.box` 上 `aria-labelledby="modal-title"`
  - close button `aria-label="Close"`
  - status icon `aria-hidden="true"` (装饰性)

- **键盘**:
  - 打开时自动 focus 到第一个可聚焦元素 (Cancel / Confirm / first input)
  - Esc 关闭 (需 `closeOnEsc=true`)
  - Tab 顺序: 内容 → footerAssist → Cancel → Confirm → close

- **焦点管理**:
  - 弹窗打开期间 body scroll lock (`overflow: hidden`)
  - 关闭后焦点应回到触发按钮 (业务侧用 `useRef` + `focus()` 实现)

- **对比度**:
  - title `colorTextHeading` (gray-10) on `colorBgElevated` (白) → 13:1 (AAA)
  - body `colorText` (gray-9) on 白 → 11:1 (AAA)
  - status colors (success/error/warning/info) 在白底上均 > 4.5:1 (AA)

- **Reduced motion**:
  - mask fade-in + box slide-down 各约 200ms
  - 用户 `prefers-reduced-motion` 时可在 .module.css 加 `@media` 关掉 (TODO)

---

## 文档维护

- 2026-06-03 创建 (Phase 6) — 写完 8 节 + Code Connect + Excel 已更新。
- 历史教训写进 [`AI操作手册/导入新组件的完整流程.md`](../../../_建设参考/导入新组件的完整流程.md) 铁律 #6a + #6b: 建 ComponentSet 前必扒旧库 effects/colors/labels；Figma 现有 icon 必须用 ID + getNodeByIdAsync 查 (孤儿 master parent=null findAll 找不到)。
