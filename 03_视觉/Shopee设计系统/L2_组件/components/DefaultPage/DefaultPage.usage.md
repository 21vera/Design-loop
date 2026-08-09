# DefaultPage

> 缺省页 — 当列表/数据为空 / 异常时展示插画 + 文案 + 操作引导. **根 fill 容器 + 居中**.

## 1. 总览

- **组件名**: `DefaultPage` + `Illustration`
- **用途**: 列表空 / 搜索无结果 / 加载失败 / 权限不足 等场景
- **导入**:
  ```ts
  import { DefaultPage, Illustration } from '@shopee/design-system';
  ```
- **Storybook**: `Components/DefaultPage` + `Components/Illustration`
- **Figma** (2 ComponentSet):
  - [Illustration (1458:2)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1458-2) — 20 variants (10 type × 2 size)
  - [DefaultPage (1462:351)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1462-351) — 60 variants (10 type × 2 size × 3 action)
- **Code Connect**: ✅

**依据**:
- 旧组件库 [639:7794](https://www.figma.com/design/X9NSPXvdvwGkKTHs62QIMn/-Main--Enterprise-Library?node-id=639-7794) — 10 状态插画 (用户手动复制到 System Test 1445:3889)
- 旧规范 [43:63044](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/-New-Enterprise-Guideline?node-id=43-63044) — 4 模板 + 视觉规格

---

## 2. 10 个 Type (来源旧库)

| Type | 视觉 | 默认 title |
|---|---|---|
| `no-orders` | 剪贴板 | No Orders Found |
| `no-data` | 文档+图表 | No Data |
| `no-product` | 盒子 | No Product Found |
| `no-search-match` | 放大镜+问号 | Your search does not match any results |
| `no-transaction` | 文档 | No transaction history |
| `no-ratings` | 对话框 | You have not received any ratings |
| `no-images` | 图像占位 | You have not received any images |
| `no-voucher` | 票据 | No voucher |
| `no-discount` | 喇叭 | No discount promotions found |
| `no-permission` | 盾 | You don't have access |

---

## 3. 2 Size

| Size | 插画尺寸 | 使用场景 |
|---|---|---|
| `normal` (默认) | 96×96 | 大容器 (Modal/页面/Drawer body) |
| `small` | 56×56 | 小空间 (Card 内 / Table 内 / Drawer 紧凑布局) |

---

## 4. 3 Action

| Action | 视觉 | 触发 |
|---|---|---|
| `none` (默认) | 仅插画 + 文字 | `action="none"` 或不传 |
| `link` | 插画 + 文字 + 蓝 link (inline) | `action="link"` + `actionText` |
| `button` | 插画 + 文字 + 主按钮 (下方) | `action="button"` + `actionText` |

---

## 5. 根 Fill + 居中规则

DefaultPage 设计是 **作为占位放进任意容器**:
- CSS: `width: 100% + height: 100% + display: flex + align/justify center`
- 容器宽高任意 → DefaultPage 自动填满 + 内容上下左右居中
- 不需要业务方手动 wrap container 或 set position

```tsx
{/* 任意容器, DefaultPage 自动 fill + center */}
<div style={{ height: 400 }}>
  <DefaultPage type="no-orders" />
</div>

<div style={{ width: 240, height: 120 }}>
  <DefaultPage type="no-orders" size="small" />
</div>
```

---

## 6. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `type` | `IllustrationType` (10 个) | — | **必填**, 插画类型 |
| `size` | `'normal' \| 'small'` | `'normal'` | 96 or 56 |
| `action` | `'none' \| 'link' \| 'button'` | `'none'` | 操作类型 |
| `title` | `ReactNode` | 按 type 自动取 | 自定义标题 |
| `actionText` | `ReactNode` | `'Reload'` | Link/Button 文案 |
| `onAction` | `() => void` | — | Link/Button 点击 |
| `className` | `string` | — | 自定义 |

---

## 7. 场景示例

### 7.1 列表空 (默认)
```tsx
<DefaultPage type="no-orders" />
```

### 7.2 搜索无匹配 + Link 重试
```tsx
<DefaultPage
  type="no-search-match"
  action="link"
  actionText="Reload"
  onAction={() => refetch()}
/>
```

### 7.3 无 Voucher + Button 跳转
```tsx
<DefaultPage
  type="no-voucher"
  action="button"
  actionText="Get Voucher"
  onAction={() => navigate('/voucher')}
/>
```

### 7.4 Drawer 内 (小空间用 Small)
```tsx
<Drawer open title="操作记录">
  <DefaultPage type="no-transaction" size="small" />
</Drawer>
```

### 7.5 Modal 内自定义文案
```tsx
<Modal open title="确认">
  <DefaultPage
    type="no-data"
    title="暂无数据"
    action="button"
    actionText="去添加"
    onAction={() => navigate('/create')}
  />
</Modal>
```

### 7.6 单独用 Illustration (不带文字)
```tsx
<Illustration type="no-orders" size="small" />
```

---

## 8. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| Illustration Normal | 96×96 | `--Illustration-sizeNormal` |
| Illustration Small | 56×56 | `--Illustration-sizeSmall` |
| Illustration stroke | `#D8D8D8` | `--Illustration-colorStroke` |
| Illustration fill | `#FAFAFA` | `--Illustration-colorFill` |
| Gap (插画↔文字) | 8 | `--DefaultPage-gapIllustrationText` |
| Gap (文字↔Button) | 16 | `--DefaultPage-gapTextAction` |
| Gap (文字↔Link inline) | 8 | `--DefaultPage-linkGap` |
| 文字 | Roboto 14 / 16 / `#999` | `--DefaultPage-textFontSize/LineHeight/colorText` |
| Link 文字 | Roboto 14 / 16 / `#2673DD` | `--DefaultPage-colorLink` |

---

## 9. 反例

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 自画插画 | 用 `<Illustration name="no-orders" />` (来源旧库) | 铁律 #8 + #10 |
| 不放容器直接渲染 (没父尺寸) | 包一层 fixed 高度的 div | DefaultPage 100% h/w 需要父定义 |
| Button 用 a 标签 | 用 `<Button>` library 实例 | 铁律 #8 |
| size="normal" 用在 Table 空状态 | 用 size="small" | Table 行高有限 |
| 自定义 `actionText` 但 `action="none"` | `actionText` 仅在 link/button 时生效 | API 设计明确 |

---

## 10. Accessibility

- Root: `role="status"` (动态状态播报)
- Illustration: `role="img"` + `aria-label={type}`
- Link button: 原生 `<button>` + `aria-label="Reload"` (或自定义)
- Button: 自带 a11y (复用 `<Button>`)

---

## 11. 历史变更

- **2026-06-08 v1** — Phase 5 首版
  - 1 ComponentSet Illustration (20 variants: 10 type × 2 size), 1 ComponentSet DefaultPage (60 variants: × 3 action)
  - Illustration: 真实插画来自旧库 4131:1028, 由用户手动复制 + 我用 detachInstance + clone 提取 vector data 进 ComponentSet
  - DefaultPage: 根 fill 容器 + 居中, 复用 Illustration + Button — 业务方可放进任何尺寸容器
  - 12 Token (5 Illustration + 7 DefaultPage), Excel 601-612
  - React SVG: 10 个 placeholder SVG 实现 (线条风格, currentColor + token-driven). 后续可替换为旧库 exported SVG 提升保真度
  - Storybook: Playground / AllTypes / Actions / Sizes / FillContainers
  - 流程手册: 等高等宽 cell 规则写入 (Display 矩阵细则)
