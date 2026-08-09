# Pagination

> 分页器 — 将内容/搜索结果分成多个页面, 由翻页符 + 页码 + 每页数量 + 跳转器组成.

## 1. 总览

- **组件名**: `Pagination`
- **用途**: 表格 / 列表 / 卡片 grid 的分页导航
- **导入**:
  ```ts
  import { Pagination } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Pagination`
- **Figma** (5 ComponentSet):
  - [PaginationItem (342:385)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=342-385) — 4 states (default/active/disabled/ellipsis)
  - [PaginationNav (342:398)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=342-398) — 4 (prev/next × default/disabled)
  - [PaginationGoToInput (343:381)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=343-381) — 188×32
  - [PaginationSizeSelect (343:387)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=343-387) — 109×32
  - [Pagination root (344:144)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=344-144) — **6 mode variants**
- **Code Connect**: ✅ (`Pagination.figma.tsx`)

**依据来源**:
- Tier 1: 旧组件库 [4121:501](https://www.figma.com/design/X9NSPXvdvwGkKTHs62QIMn/-Main--Enterprise-Library?node-id=4121-501) — 6 类型完整视觉规格
- Tier 2: 设计规范 [25:11988](https://www.figma.com/design/ffIT3A1gHm5VAk6YUcbxiW/-New-Enterprise-Guideline?node-id=25-11988) — 业务场景
- System Test 246:17 — 已建工件, 本流程全套复用

---

## 2. 6 个 Mode (核心要先记住)

| Mode | 视觉 | 触发条件 |
|---|---|---|
| `simple` | `< 1 / 3 >` | `simple={true}` |
| `basic` | `< 1 2 3 4 5 6 7 >` | 默认, 页数 ≤ 7 |
| `withEllipsis` | `< 1 2 3 4 5 … 34 >` | 默认, 页数 > 7 |
| `basicWithSizeChanger` | `< 1 2 3 … 34 >` + `24 / Page` | `showSizeChanger={true}` |
| `basicWithQuickJumper` | `< 1 2 3 … 34 >` + `Go to page __ [Go]` | `showQuickJumper={true}` |
| `combined` | 全部都有 | 两个都 true |

**Mode 内部智能推断**, 一般无需手设. 也可用 `mode` prop 强制锁定.

---

## 3. 决策树 (AI 必读)

```
分页场景?
├─ 移动端 / 空间紧 → simple={true}
├─ 桌面端列表 / 表格 → 默认 (basic 或 withEllipsis 自动)
│   └─ 用户需要快速跳转? → showQuickJumper={true}
│   └─ 用户需要改 pageSize? → showSizeChanger={true}
│   └─ 两个都需要? → 两个 prop 一起开 (= combined mode)

总数 ≤ 7 页?
├─ 是 → basic (全显示)
└─ 否 → withEllipsis (自动出 ...)

总数 = 0 / 1 页?
└─ 仍渲染但 prev/next 都 disabled, 不影响显示
```

---

## 4. Props 完整签名

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `total` | `number` | — | **必填**, 数据总数 |
| `current` | `number` | — | 当前页码 (1-based, 受控) |
| `defaultCurrent` | `number` | `1` | 非受控初值 |
| `pageSize` | `number` | — | 每页条数 (受控) |
| `defaultPageSize` | `number` | `10` | 非受控初值 |
| `pageSizeOptions` | `number[]` | `[10,20,50,100]` | size changer 可选 |
| `onChange` | `(page, pageSize) => void` | — | 页码改变 |
| `onPageSizeChange` | `(size) => void` | — | size 改变 |
| `showSizeChanger` | `boolean` | `false` | 显示 `24 / Page` |
| `showQuickJumper` | `boolean` | `false` | 显示 `Go to page __` |
| `simple` | `boolean` | `false` | 极简: `< 1 / 3 >` |
| `disabled` | `boolean` | `false` | 整个 disable |
| `mode` | `PaginationMode` | (auto) | 强制锁 mode (覆盖推断) |
| `prevText` / `nextText` | `ReactNode` | — | 自定义 prev/next |
| `goToText` | `ReactNode` | `'Go to page'` | quick jumper 文案 |
| `className` | `string` | — | 自定义 |

---

## 5. 场景示例

### 5.1 基础
```tsx
<Pagination total={340} defaultCurrent={1} pageSize={10} />
// withEllipsis 自动 (34 页 > 7)
```

### 5.2 受控
```tsx
const [page, setPage] = useState(1);
<Pagination total={100} current={page} pageSize={10} onChange={(p) => setPage(p)} />
```

### 5.3 size + jumper (combined)
```tsx
<Pagination
  total={1240}
  pageSize={20}
  pageSizeOptions={[20, 50, 100, 200]}
  onChange={(page, size) => fetchList(page, size)}
  showSizeChanger
  showQuickJumper
/>
```

### 5.4 极简 (移动端)
```tsx
<Pagination total={30} pageSize={10} simple />
// 视觉: < 1 / 3 >
```

### 5.5 自定义 prev/next 文字
```tsx
<Pagination total={50} pageSize={10} prevText="上一页" nextText="下一页" />
```

### 5.6 Disabled
```tsx
<Pagination total={100} pageSize={10} disabled />
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| Item / Nav 方形 | 24×24 | `--Pagination-itemSize` |
| Item 字号 / 行高 | 14 / 18 | `--Pagination-itemFontSize` / `--Pagination-itemLineHeight` |
| Item 默认字色 | `#333` | `--Pagination-colorText` |
| Item active 字色 | `#EE4D2D` + Medium | `--Pagination-colorTextActive` |
| Item disabled 字色 | `#B7B7B7` | `--Pagination-colorTextDisabled` |
| Item ellipsis | `…` | (内联文本) |
| Item-Item gap (标准) | 16 | `--Pagination-itemGap` |
| Item-Item gap (simple) | 8 | `--Pagination-itemGapSmall` |
| Group-Group gap (combined) | 24 | `--Pagination-groupGap` |
| Nav icon size | 16 (in 24×24 frame) | `--Pagination-iconSize` |
| SizeSelect / GoToInput 高 | 32 | `--Pagination-inputHeight` |
| 灰文案 ("24 / Page", "Go to page") | `#999` | `--Pagination-colorTextSubtle` |
| Border (input / size select) | 1px `#E5E5E5` | (复用 colorBorder) |
| Border-radius | 4 | (复用 borderRadius) |

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| 自画 arrow / chevron icon | 用 `<Icon name="arrow-left/right/down" />` | 铁律 #8 |
| Item active 用红色背景 | 仅文字 `#EE4D2D` + Medium (无 bg) | 严格旧库 4121:501 |
| pageSize 切换不重置 current | 切 pageSize 自动回第 1 页 (内部已做) | 业界惯例避免越界 |
| simple 模式还显示页码列表 | simple: `< 1 / 3 >` 仅显示当前/总 | 极简的本质 |
| 页数 ≤ 7 还出 ellipsis | basic mode 全显示 | 不必要 |
| 页数 > 7 不出 ellipsis | withEllipsis 自动 (`computeVisiblePages`) | UX 必须 |
| ellipsis 当 button (可点) | ellipsis 是占位 `<span>`, 不可点 | 没有具体页跳 |
| current 超 totalPages | `commitPage` 内部 clamp 到 [1, total] | 防越界 |

---

## 8. Accessibility

- Root: `<div>` flex 容器
- 数字 item: `<button>`, `aria-current="page"` (active 时)
- ellipsis: `<span aria-hidden>` (不参与 Tab)
- Nav (prev/next): `<button>` + `aria-label="Previous/Next"`
- SizeSelect: 原生 `<select>` (内置 a11y)
- QuickJumper input: `<input type="number">` + `aria-label="Go to page"`
- 键盘:
  - Tab 走焦点
  - Space/Enter 触发
  - QuickJumper Enter 即跳

未来增强 (TODO):
- 左右方向键在 items 间导航
- Home/End 跳首页/末页
- 自定义 itemRender (像 Ant Design)
- SizeSelect 改用 Dropdown 组件 (替代原生 select)

---

## 9. 历史变更

- **2026-06-08 v1** — Phase 5 首版
  - **复用 Figma 已有工件 100%** (5 ComponentSet)
  - React Pagination: 智能 mode 推断 + 受控/非受控 双轨
  - `computeVisiblePages` 算法 — 总是首末页可见, 当前页前后 1 页, 其余 ellipsis
  - 6 mode 全覆盖 (simple/basic/withEllipsis/basicWithSizeChanger/basicWithQuickJumper/combined)
  - 12 Token 全绑定 (8 Component + 4 Global)
  - 复用: Button (Go) + Icon (arrow-left/right/down) — 铁律 #8
  - Storybook: Playground / Matrix 6 cells / RealWorld (简单/动态/极简/disabled)
