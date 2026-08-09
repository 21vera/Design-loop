# Avatar 组件用法（AI 调用指南）

> **依据来源**（Phase 2.5 Scope 契约逐项标注）：
> - **主**：旧 Shopee Guidelines [GP-Avatar 节点 25:6502](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/?node-id=25-6502)
> - **辅**：旧 Vue `Shopee前端组件源码/components/avatar/`
> - **旧库精确数值**：[节点 4121:290](https://www.figma.com/design/4EgWXbFDmKLRpU0hdZeDh4/?node-id=4121-290)
> - **System Test**：[ComponentSet 897:34](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=897-34) + [Display 898:2](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=898-2)
> - **占位 SVG**：内嵌自旧 Vue `product-img.svg` / `user-img.svg`

---

## 0. 依据来源映射

| Prop | 来源 |
|---|---|
| `size` | ✅ Tier 1 旧 Vue + 旧库（normal → medium 改名）|
| `type: 'product' \| 'user'` | ✅ Tier 1 旧库类型汇总（旧 Vue `circle` boolean 合并）|
| `src` / `onError` | ✅ Tier 2 旧 Vue |
| `alt` | ✅ Tier 3 a11y 补齐 |
| `icon` / `children` | ✅ Tier 2 旧 Vue |

无 Tier 4。

---

## 1. 总览

- **导入**：`import { Avatar, type AvatarProps } from '@shopee/design-system';`
- **Storybook**：`Components/Avatar`
- **Code Connect**：Avatar.figma.tsx

---

## 2. 决策树

```
需要展示头像或商品图?
├─ 商品 → type="product" (圆角 2px)
└─ 用户 → type="user" (圆形)

有图片 url? → 传 src
没有 / 加载失败? → 自动 fallback 到默认占位 (Product=购物袋, User=人物)

特殊需求?
├─ 显示首字母 → 传 children (例: "JD")
├─ 自定义 icon → 传 icon prop
└─ 任意尺寸 → size 传 number (例: size={48})

尺寸怎么选?
├─ 商品大图详情 → size="large" (96)
├─ 列表项 → size="medium" (56, 默认)
├─ 表格头像 → size="small" (32)
└─ 评论点赞列表 → size="xsmall" (24)
```

---

## 3. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `size` | `'large' \| 'medium' \| 'small' \| 'xsmall' \| number` | `'medium'` | 尺寸 |
| `type` | `'product' \| 'user'` | `'product'` | 类型 |
| `src` | `string` | — | 图片 url |
| `alt` | `string` | — | a11y label |
| `icon` | `ReactNode` | — | 自定义 icon 覆盖默认 |
| `children` | `ReactNode` | — | 自定义内容（首字母等）|
| `onError` | `(e) => void` | — | 图片加载失败回调 |

---

## 4. 视觉规格速查

| Size | 像素 | 字号 (children) |
|---|---|---|
| large | 96 | 36 |
| medium | 56 | 22 |
| small | 32 | 14 |
| xsmall | 24 | 10 |

| 类型 | 圆角 | 默认占位 SVG |
|---|---|---|
| product | 2px (`--Avatar-borderRadiusProduct`) | Shopee 购物袋 |
| user | 50% (`--Avatar-borderRadiusUser`, 圆形) | 人物剪影 |

| 状态 | 视觉 |
|---|---|
| 有 src + 加载成功 | 显示图片 (object-fit: cover) |
| 无 src 或加载失败 | 显示默认占位 icon (alpha 12% 黑) |
| 传 children | children 优先 (例如首字母) |
| 传 icon | icon 优先于 src 和默认 |

---

## 5. Shopee 特有规则

1. **Product 圆角 2px, User 圆形** — 旧库强约束, 不要混
2. **默认底色 alpha 4% 黑** (`colorFillQuaternary`) — 不要换成实灰色
3. **默认 icon 用旧库 SVG path** — 已内嵌在 Avatar.tsx, 不要换成 emoji 或其他 icon 库
4. **Image fallback 自动** — 设置 src 失效时不需要手动处理, 内部 state 触发 onError 后自动显示默认占位
5. **`object-fit: cover`** — 图片永远等比缩放裁切, 不变形

---

## 6. 场景示例

### 6.1 用户列表

```tsx
{users.map(u => (
  <div key={u.id}>
    <Avatar type="user" size="medium" src={u.avatar} alt={u.name} />
    <span>{u.name}</span>
  </div>
))}
```

### 6.2 商品网格

```tsx
{products.map(p => (
  <Avatar type="product" size="large" src={p.cover} alt={p.name} />
))}
```

### 6.3 首字母 fallback (无图但要避免占位)

```tsx
{user.avatarUrl
  ? <Avatar type="user" size="medium" src={user.avatarUrl} alt={user.name} />
  : <Avatar type="user" size="medium" style={{ background: getColorByName(user.name), color: 'white' }}>
      {user.name[0]}
    </Avatar>}
```

### 6.4 自定义尺寸

```tsx
<Avatar type="user" size={48} src={user.avatar} />  // 介于 medium 和 large
```

### 6.5 错误处理 + 自定义 fallback

```tsx
<Avatar
  type="product"
  src={product.cover}
  onError={() => trackEvent('avatar_load_failed', { id: product.id })}
/>
```

---

## 7. 组合模式

| 搭配 | 用法 |
|---|---|
| **Badge** | Avatar 上挂 Badge (count/dot/pulse) 显示在线状态 / 未读数 |
| **Tag** | Avatar 旁配 Tag 显示状态 (如 "Verified") |
| **Card** | Card title 旁放 Avatar 作为头像位 |
| **Table 行** | Small Avatar + 名字, 节省垂直空间 |

---

## 8. 反例

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 商品图用 `type="user"` 圆形 | 用 `type="product"` 圆角 | 视觉语义错位 |
| 用户头像用 `type="product"` 方形 | 用 `type="user"` 圆形 | 同上 |
| size 传 `'normal'` | 用 `'medium'` | 旧 Vue 已 deprecated normal |
| 不传 alt | 必传 alt (有 src 时) | a11y 必需 |
| `<img>` 直接包 div 模拟 Avatar | 用 Avatar | 避免重复, 失去 fallback |
| 默认占位 icon 换成 emoji | 用内嵌 SVG | 视觉一致性 |

---

## 9. 与 Badge 的区别

| 维度 | Avatar | Badge |
|---|---|---|
| 用途 | **展示图像** (用户 / 商品) | **提示标识** (数字/小点)|
| 大小 | 24-96 px | 8-30 px |
| 内容 | 图像 / 首字母 / 占位 icon | 数字 / "New"/"Hot" 等 |
| 位置 | 行内主元素 | 通常挂在 anchor 右上角 |

---

## 10. 已知限制 / 后续 TODO

- ❌ 不支持 `shape="square"` 上的圆角自定义 (固定 2px)
- ❌ 不支持 Avatar 组 (Avatar.Group, 多人头像堆叠) — 等真实需求再加
- ❌ 不支持 alt 之外的 a11y 状态描述
