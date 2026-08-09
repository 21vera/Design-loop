# Alert

> 提示条 — 显示页面级别的状态/警告/反馈, 不打断主流程. **1:1 旧库 4131:1028**.

## 1. 总览

- **组件名**: `Alert`
- **用途**: 页面顶/区块顶的状态提示 (区别于 Toast 悬浮短时, Alert 持续展示)
- **导入**:
  ```ts
  import { Alert } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Alert`
- **Figma**: [Alert ComponentSet (1430:94)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1430-94) — **40 valid variants** (Status 4 × Layout 2 × HasIcon 2 × HasLink 2 × HasClose 2 减 invalid)
- **Code Connect**: ✅ (`Alert.figma.tsx`)

**依据来源**:
- Tier 1: 旧组件库 [4131:1028](https://www.figma.com/design/X9NSPXvdvwGkKTHs62QIMn/-Main--Enterprise-Library?node-id=4131-1028) — 4 status 各 10 form variants, 严格 1:1 还原
- Tier 2: 设计规范 [43:62235](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/-New-Enterprise-Guideline?node-id=43-62235)

---

## 2. 5 个 Axes (核心要先记住)

| Axis | 值 | 触发 prop |
|---|---|---|
| **Status** | info / warning / success / error | `status` |
| **Layout** | Single (默认) / Multi | 传 `description` 自动进 Multi |
| **HasIcon** | Yes (默认) / No | `showIcon={false}` 关闭 |
| **HasLink** | No (默认) / Yes | 传 `link={...}` |
| **HasClose** | No (默认) / Yes | `closable={true}` |

**总 valid 组合 = 40** (Multi 强制 HasIcon=Yes / HasLink=No, 排除 24 个 invalid)

---

## 3. 4 Status 颜色 (3 层视觉系统)

| Status | bg (浅) | border (中) | **icon (深, semantic)** |
|---|---|---|---|
| `info` | `#EBF2FB` | `#4EABF5` | **`#2673DD`** (colorInfo) |
| `warning` | `#FFF6E1` | `#FFCE3D` | **`#FFBF00`** (colorWarning) |
| `success` | `#F2FBF4` | `#7ED898` | **`#55CC77`** (colorSuccess) |
| `error` | `#FFF1F0` | `#FF736F` | **`#FF4742`** (colorError) |

**铁律 #11**: icon 用 **semantic 色** (深, 饱和), 永远不用 border 色 (偏浅).
**Close button** 统一灰 `#999` (`colorIcon`).

---

## 4. 2 Layout 区别

| Layout | 触发 | padding | title | 视觉 |
|---|---|---|---|---|
| **Single** | 不传 `description` | 11-12 / 12-16 微差 | 14/16 (或 18 for Info bare) `#666` | icon + title + (link) + (close) 同行 |
| **Multi** | 传 `description` | 16/12-16 | **16/20 `#333`** (更大更深) | icon + title + (close) 同行 + 下方缩进 24 显示 description (14/18 `#666`) |

**padding 细节 (旧库严格扒)**:
- Info F1/F5 (bare = 无 link/close): `pl-16 pr-12 py-11` items-center
- Info F2-F4/F6-F8 (含 link 或 close): `pl-16 pr-16 py-12` items-start
- Warn/Success/Error all single: `pl-16 pr-12 py-12` items-start
- Info Multi: `p-16` (4 边 16)
- Warn/Success/Error Multi: `pl-16 pr-12 py-16`

---

## 5. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `status` | `'info' \| 'warning' \| 'success' \| 'error'` | `'info'` | 4 种状态 |
| `title` | `ReactNode` | — | 标题/主要文字 |
| `description` | `ReactNode` | — | 描述 (传则进 Multi layout) |
| `showIcon` | `boolean` | `true` | 显示 status icon |
| `icon` | `ReactNode` | — | 自定义 icon (覆盖 status icon) |
| `link` | `ReactNode` | — | 链接 (仅 Single layout 显示, 紧跟 title 后面) |
| `closable` | `boolean` | `false` | 显示关闭按钮 |
| `onClose` | `() => void` | — | 关闭回调 |
| `visible` | `boolean` | — | 受控可见 (不传则非受控) |
| `className` | `string` | — | 自定义 |

---

## 6. 场景示例

### 6.1 Single 单行
```tsx
<Alert status="info" title="您的店铺名 7 天内不可再次修改" closable />
```

### 6.2 Single 含 Link (Link 紧跟 title)
```tsx
<Alert status="error" title="提交失败" link={<a href="/help">联系客服</a>} closable />
```

### 6.3 Multi 多行 (含 description)
```tsx
<Alert
  status="warning"
  title="折扣过高可能导致亏损"
  description="当前折扣 90%, 远高于行业建议."
  closable
/>
```

### 6.4 无 icon (纯文字)
```tsx
<Alert status="info" title="Information Text" showIcon={false} />
```

### 6.5 自定义 icon
```tsx
<Alert status="success" title="充值到账" icon={<Icon name="add" />} />
```

### 6.6 受控隐藏
```tsx
const [visible, setVisible] = useState(true);
<Alert
  status="info"
  title="保存草稿"
  closable
  visible={visible}
  onClose={() => setVisible(false)}
/>
```

---

## 7. Token 完整清单 (37 个, Excel 564-600)

### Global 层 (17 个)
| Token | 值 | 来源 |
|---|---|---|
| `--Alert-colorBgInfo` | `#EBF2FB` | 旧库 |
| `--Alert-colorBorderInfo` | `#4EABF5` | 旧库 |
| `--Alert-colorBgWarning` | `#FFF6E1` | 旧库 |
| `--Alert-colorBorderWarning` | `#FFCE3D` | 旧库 |
| `--Alert-colorBgSuccess` | `#F2FBF4` | 旧库 |
| `--Alert-colorBorderSuccess` | `#7ED898` | 旧库 |
| `--Alert-colorBgError` | `#FFF1F0` | 旧库 |
| `--Alert-colorBorderError` | `#FF736F` | 旧库 |
| `--Alert-colorTextTitleSingle` | → `colorTextSecondary` (#666) | alias |
| `--Alert-colorTextTitleMulti` | → `colorText` (#333) | alias |
| `--Alert-colorTextDescription` | → `colorTextSecondary` (#666) | alias |
| `--Alert-colorTextLink` | → `colorInfo` (#2673DD) | alias |
| `--Alert-colorIconInfo` | → `colorInfo` (#2673DD) | **semantic 非 border** |
| `--Alert-colorIconWarning` | → `colorWarning` (#FFBF00) | **semantic** |
| `--Alert-colorIconSuccess` | → `colorSuccess` (#55CC77) | **semantic** |
| `--Alert-colorIconError` | → `colorError` (#FF4742) | **semantic** |
| `--Alert-colorIconClose` | → `colorIcon` (#999) | close 灰 |

### Component 层 (20 个)
| Token | 值 |
|---|---|
| `paddingBareBlock` | 11 |
| `paddingSingleBlock` | 12 |
| `paddingMultiBlock` | 16 |
| `paddingInlineLeft` | 16 |
| `paddingInlineRightSmall` | 12 |
| `paddingInlineRightLarge` | 16 |
| `iconSize` | 16 |
| `closeIconSize` | 16 |
| `iconGap` | 8 |
| `descriptionIndent` | 24 |
| `borderRadius` | → `borderRadius` (4) |
| `titleSingleFontSize` | 14 |
| `titleSingleLineHeight` | 16 |
| `titleBareLineHeight` | 18 (Info F1/F5 特殊) |
| `titleMultiFontSize` | 16 |
| `titleMultiLineHeight` | 20 |
| `descriptionFontSize` | 14 |
| `descriptionLineHeight` | 18 |
| `linkFontSize` | 14 |
| `linkLineHeight` | 16 |

---

## 8. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| Status icon 用 `colorBorder*` | 用 `colorIcon*` alias `colorInfo/Warning/Success/Error` | **铁律 #11**, 3 层视觉系统 bg/border/icon 别混 |
| Close button 没绑色 (留默认) | 必须绑 `colorIconClose` (#999) | **铁律 #12**, 每元素必须 token |
| 折叠 boolean 当 Property (8 variants) | Cartesian 全枚举 40 variants | **铁律 #13**, 触发布局变就必须 variant |
| Padding/字号 硬编码 | 全部 alias 到 token | **铁律 #12** |
| icon shape fill 只覆盖 VECTOR | 覆盖 ELLIPSE+VECTOR+BOOL_OP+POLYGON+RECT+STAR | **铁律 #15**, 避免 Warning ELLIPSE 漏色 |
| 自画 status icon / close icon | 用 Icon 库 instance | **铁律 #8** + **#10** |
| 短时反馈 / 强阻断流程 | Toast (短时) / Modal (阻断) | Alert 是持续非阻断 |

---

## 9. Accessibility

- Root: `role="alert"` (屏幕阅读器自动播报)
- Status icon: `aria-hidden` (信息已在 title)
- Close button: `aria-label="Close"`
- Link: `<a>` 自身
- 颜色对比通过 WCAG AA
- 键盘: Tab 可达 Close, Enter/Space 触发

---

## 10. 历史变更

- **2026-06-08 v1** — Phase 5 首版 (8 variants, 错)
- **2026-06-08 v2** — 全重做 (按用户反馈 1:1 旧库)
  - 删 8 variants, 严格按旧库重建 **40 variants** (Status 4 × Layout 2 × HasIcon 2 × HasLink 2 × HasClose 2 减 invalid)
  - 每 variant padding 按旧库 1:1 (含 Info bare F1/F5 特殊 py-11 items-center, title 14/18)
  - Token 总数从 16 → **37** (8 status color + 4 text color + 5 icon color + 20 component + 1 titleBareLH)
  - **icon 改用 semantic 色** (非 border) — `colorInfo/Warning/Success/Error`, 修正 4 status icon
  - **close button 用 `colorIcon` (#999)** — 显式绑定避免 fall through 默认
  - Warning icon ELLIPSE 上色 (之前 type filter 只覆 VECTOR/BOOLEAN_OPERATION 漏了 ELLIPSE)
  - **Link 紧跟 title** (旧版被推到右边). CSS: title `flex: 0 1 auto` + close `margin-left: auto`
  - **高度自适应内容** (counterAxisSizingMode AUTO, CSS 无固定 height)
  - Display 改 Property × Value Matrix (5 axes 5 rows)
  - 流程文档加 5 条新铁律 (#11-15) 防类似错
