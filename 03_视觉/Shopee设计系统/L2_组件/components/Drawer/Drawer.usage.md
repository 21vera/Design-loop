# Drawer

> 抽屉 — 触发命令后, 从屏幕边缘滑入的浮层面板. 承载中等复杂度的二级操作.

## 1. 总览

- **组件名**: `Drawer`
- **用途**: 详情拓展 (列表→详情) / 内容编辑 (长表单) / 多任务操作
- **导入**:
  ```ts
  import { Drawer } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Drawer`
- **Figma**: [Drawer (1369:26)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1369-26) — 6 variants (Size 3 × HasFooter 2)
- **Code Connect**: ✅ (`Drawer.figma.tsx`)

**依据来源**:
- Tier 1: 旧设计规范 [2911:16134](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/-New-Enterprise-Guideline?node-id=2911-16134) — 完整规格
- 旧组件库: 暂无 master (与 Search 同, 从规范从零搭)
- System Test 246:46 — 占位页, 由本流程填充

---

## 2. 3 个 Size (旧规范明确)

| Size | 宽度 | 业务示例 |
|---|---|---|
| `medium` | **600px** | 单 module 详情, 简单表单 |
| `large` | **800px** | 多 module 表单, 复杂详情 |
| `special` | **1000px** (max 1024) | 极宽场景: 表格 / 多列 |

**注意**: Special 是上限. 超过 1024px 应改用落地页 (Landing Page).

---

## 3. 决策树 (Drawer vs Modal vs Landing Page — 旧规范明确表)

```
内容复杂度 + 流程阻断强度 + 与主页面关联性?

├─ 内容简单 + 强阻断流程              → Modal
│   e.g. 确认 / 提示 / 简单增删改查
│
├─ 内容中等 + 非阻断 + 与主页强关联    → Drawer  ✅
│   e.g. 列表→详情, 长表单, 多模块编辑
│
└─ 内容复杂 + 独立流程 + 与主页弱关联  → Landing Page
    e.g. 商品工作台→创建商品页
```

**交互区分:**
- **详情型** Drawer: 点击 mask 即关 (`maskClosable=true`, 默认)
- **表单型** Drawer: 点击 mask 不关, 必须按按钮 (`maskClosable=false`)

**禁忌**: ⚠️ 不建议 drawer 套 drawer (除特殊业务诉求).

---

## 4. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `open` | `boolean` | — | **必填**, 是否打开 |
| `onClose` | `() => void` | — | **必填**, 关闭回调 |
| `title` | `ReactNode` | — | 标题 |
| `children` | `ReactNode` | — | 主体内容 |
| `size` | `'medium' \| 'large' \| 'special'` | `'medium'` | 尺寸 (600/800/1000) |
| `width` | `number \| string` | — | 自定义宽 (覆盖 size, 用于 right/left) |
| `height` | `number \| string` | — | 自定义高 (用于 top/bottom) |
| `placement` | `'top' \| 'right' \| 'bottom' \| 'left'` | `'right'` | 滑入方向 |
| `mask` | `boolean` | `true` | 显示蒙层 |
| `maskClosable` | `boolean` | `true` | mask 点击关闭 (表单型设 false) |
| `closeOnEsc` | `boolean` | `true` | Esc 关闭 |
| `showClose` | `boolean` | `true` | 显示右上角 close |
| `showFooter` | `boolean` | `false` | 显示 footer |
| `footer` | `ReactNode` | — | 自定义 footer (完全替换内置) |
| `footerText` | `ReactNode` | — | footer 左侧 14px 辅助文案 |
| `cancelText` | `ReactNode \| null` | `'Cancel'` | Cancel 文案 (null 不显示) |
| `confirmText` | `ReactNode \| null` | `'Confirm'` | Confirm 文案 (null 不显示) |
| `onCancel` | `() => void` | = `onClose` | Cancel 点击 |
| `onConfirm` | `() => void \| Promise` | — | Confirm 点击 (返 Promise 自动 loading) |
| `confirmLoading` | `boolean` | — | 受控 loading 状态 |
| `zIndex` | `number` | — | 自定义 z-index |
| `container` | `HTMLElement` | `document.body` | Portal 容器 |
| `className` / `panelClassName` / `maskClassName` | `string` | — | 三处自定义 class |

---

## 5. 场景示例

### 5.1 详情型 Drawer (mask 点击即关)
```tsx
const [open, setOpen] = useState(false);

<Drawer
  open={open}
  onClose={() => setOpen(false)}
  title="商品详情 — iPhone 15 Pro"
  size="medium"
>
  {/* 详情内容 */}
</Drawer>
```

### 5.2 表单型 Drawer (mask 不可关, Confirm Promise)
```tsx
<Drawer
  open={open}
  onClose={() => setOpen(false)}
  title="编辑商品"
  size="large"
  maskClosable={false}
  showFooter
  onConfirm={async () => {
    await api.saveProduct(form);
    toast.success('保存成功');
  }}
>
  {/* 长表单字段... */}
</Drawer>
```

### 5.3 带辅助文案的 footer
```tsx
<Drawer
  open={open}
  onClose={() => setOpen(false)}
  title="同步设置"
  footerText="保存后将自动同步到所有店铺"
  showFooter
>
  {/* content */}
</Drawer>
```

### 5.4 仅 Confirm 单按钮
```tsx
<Drawer
  open={open}
  onClose={() => setOpen(false)}
  cancelText={null}
  confirmText="知道了"
  showFooter
>
  {/* content */}
</Drawer>
```

### 5.5 从左 / 上 / 下滑入
```tsx
<Drawer open placement="left" size="medium" onClose={close}>侧边导航</Drawer>
<Drawer open placement="bottom" size="medium" onClose={close}>底部抽屉</Drawer>
<Drawer open placement="top" size="medium" onClose={close}>顶部通告</Drawer>
```

### 5.6 自定义 footer 完全替换
```tsx
<Drawer
  open={open}
  onClose={close}
  footer={
    <div style={{ display: 'flex', justifyContent: 'space-between', width: '100%' }}>
      <Button variant="text">导出</Button>
      <Button variant="primary">保存草稿</Button>
    </div>
  }
>
  {/* content */}
</Drawer>
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| Medium 宽 | 600px | `--Drawer-widthMedium` |
| Large 宽 | 800px | `--Drawer-widthLarge` |
| Special 宽 | 1000px (max 1024) | `--Drawer-widthSpecial` |
| Header padding | 24 | `--Drawer-headerPadding` |
| Body padding | 0 24 (上下 0, 左右 24) | `--Drawer-bodyPaddingInline` |
| Footer padding | 24 | `--Drawer-footerPadding` |
| Footer 按钮间距 | **24** (注意: 与 Modal 8 不同) | `--Drawer-footerGap` |
| Title 字号 | 20px | `--Drawer-titleFontSize` |
| Title 行高 | 24px (Modal 是 28) | `--Drawer-titleLineHeight` |
| Title 字色 | `#1d2129` (旧规范明确) | `--Drawer-colorTextTitle` |
| Title 字重 | Roboto Medium | — |
| Footer 辅助文案 | 14/20 `#333` | `--Drawer-footerTextFontSize` |
| Close icon size | 16px | `--Drawer-closeIconSize` |
| 背景 | `#FFFFFF` | `--Drawer-colorBg` |
| Mask | `rgba(0,0,0,0.45)` (同 Modal) | `--Drawer-colorBgMask` |
| 滑入动画 | `transform 0.25s ease` | (CSS 内置) |
| z-index | 1100 | (CSS 内置, 高于 Modal 1050) |

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 表单型还设 `maskClosable=true` | 表单型必须 `maskClosable=false` | 误点 mask 表单数据丢失 |
| 详情型还显示 footer | 详情型一般不需 footer (只看不改) | 旧规范明确详情/表单二分 |
| 用 Drawer 装简单确认 | 改用 Modal | 内容简单 + 强阻断 = Modal |
| 用 Drawer 装完整独立流程 | 改用 Landing Page | 内容复杂 + 独立流程 = LandingPage |
| Drawer 套 Drawer | 避免 | 旧规范明确不建议 |
| 宽度超 1024px | 改用 LandingPage | Special 上限 1024 |
| 自画 close icon | 用 `<Icon name="close" />` | 铁律 #8 + #10 |
| Footer button 用 type 而非 variant | `<Button variant="primary">` | Button API 用 variant |
| Confirm 没 await Promise | `onConfirm` 返 Promise, 内部自动 loading | 不返 Promise loading 不生效 |
| placement 用 size 控宽 | placement 'right'/'left' 用 width, 'top'/'bottom' 用 height | 不同方向走不同维度 |

---

## 8. Accessibility

- Root: `role="dialog"`, `aria-modal="true"`
- Close button: `<button>` + `aria-label="Close"`
- 键盘:
  - Tab 进入第一个可聚焦元素
  - Esc 关闭 (`closeOnEsc=true`, 默认)
  - Cancel button 默认有 focus 提示
- Focus trap: TODO (v2 增强)
- Body scroll lock 防止 mask 后页面滚动

未来增强 (TODO):
- Focus trap (键盘焦点限制在 drawer 内)
- 滚动到底部检测 → 自动出现分割线 (旧规范提及)
- 拖拽改尺寸 (resizable)
- 抽屉栈管理 (虽然不建议套, 但 API 支持)

---

## 9. 历史变更

- **2026-06-08 v1** — Phase 5 首版
  - 1 ComponentSet (Drawer 6 variants: Size 3 × HasFooter 2)
  - React Drawer: Portal + body scroll lock + Esc + maskClosable + Confirm Promise loading
  - 4 placement (top/right/bottom/left) — React-only prop, Figma 只画 right
  - 受控 (`open`/`onClose` 必填), 内部 loading 自动
  - 16 Token 全绑定 (11 Component + 5 Global)
  - 严格旧规范 2911:16134 扒值 (width 600/800/1000, title 20/24, footer gap 24)
  - 复用: Button (Cancel/Confirm) + Icon (close 1129:388) — 铁律 #8 / #10
  - Storybook: Playground / Matrix 6 cells / Placements 4 / RealWorld (详情型/表单型/带辅助文案)
