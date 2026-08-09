# Search

> 搜索框 — 3 类型 (Simple / Fuzzy / Sectioned), 复用 Input 输入框 + Dropdown 推荐下拉.

## 1. 总览

- **组件名**: `Search`
- **用途**: 列表/页面顶部全局搜索, 商品/订单/用户检索, 多维度筛选搜索
- **导入**:
  ```ts
  import { Search, type SearchSuggestion, type SearchOption } from '@shopee/design-system';
  ```
- **Storybook**: `Components/Search`
- **Figma** (4 ComponentSet):
  - [SearchInput (1310:119)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1310-119) — 12 variants (Status 3 × HasValue 2 × HasOption 2)
  - [SearchItem (1311:59)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1311-59) — 6 variants (State 3 × Emphasis 2)
  - [SearchMenu (1312:78)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1312-78) — 3 type variants (plain / emphasis / categorized)
  - [Search 组合 (1313:109)](https://www.figma.com/design/KTvcllui6OGgNPI5f1DfHe/System-Test?node-id=1313-109) — Type 3 (Simple / Fuzzy / Sectioned)
- **Code Connect**: ✅ (`Search.figma.tsx`)

**依据来源**:
- Tier 1: System Test 4 个 ComponentSet (用户确认)
- Tier 2: 旧规范 40:49076 — 3 类型 + 视觉样式全规格 + 接缝处直角无圆角
- 旧 Vue 库 — 业务交互逻辑参考 (旧组件库无 Search master)

---

## 2. 3 种类型 (核心要先记住)

| Type | 描述 | 业务示例 |
|---|---|---|
| `simple` | 纯搜索框, 仅 input + clear + 🔍 | Header 全局搜索, 简单 list 内过滤 |
| `fuzzy` | 搜索框 + 即时推荐下拉 (Plain / Emphasis / Categorized 3 形态) | 商品搜索 (输入即给推荐), 用户搜索 |
| `sectioned` | Option 多维度前置 (接缝处直角无 gap) + 搜索框 + 推荐 | 订单中心 (按 Order/Product/User 切换搜) |

**核心样式约束 (严格对照旧规范):**
- Sectioned 类型: Option select 与 Input box 接缝处 **gap=0**, **直角无圆角**, **共享 1px 描边**
- 激活态描边: 用 hover 灰 `#B7B7B7`, **不用橙色** (与 Cascader / Input focus 不同)
- Input 输入框: **4 边都有 border** (在 Sectioned 中也是 4 边 border, 由 Option 取消右 border 来避免双线)

---

## 3. 决策树 (AI 必读)

```
要给用户提供搜索能力?
├─ 单维度 (一个输入框) → Simple
│   └─ 想要即时推荐 (输入触发 menu) → Fuzzy
├─ 多维度 (按类别/范围 + 关键词) → Sectioned
└─ 远程联想 / 历史记录 → Fuzzy 的 suggestions prop 灵活传

推荐数据形态?
├─ 单列 plain 列表 → SearchSuggestion[]
├─ Recommendation 加重 + Others 普通 → { Recommendation: [...], Others: [...] }
└─ 按 Category 分组 → { 'Category 1': [...], 'Category 2': [...] }

触发 onSearch 的时机?
├─ Enter 键 (默认, 推荐) → onSearch(value)
├─ 点击放大镜 🔍 → onSearch(value)
└─ 选中 suggestion → onSelectSuggestion(item) + 自动 commit label 到 value
```

---

## 4. Props 完整签名

### Search

| Prop | 类型 | 默认值 | 说明 |
|---|---|---|---|
| `type` | `'simple' \| 'fuzzy' \| 'sectioned'` | `'simple'` | 搜索类型 |
| `value` | `string` | — | 受控值 |
| `defaultValue` | `string` | `''` | 非受控初值 |
| `onChange` | `(value: string) => void` | — | 值改变 |
| `onSearch` | `(value: string) => void` | — | Enter / 🔍 触发 |
| `placeholder` | `string` | `'Search'` | 占位符 |
| `clearable` | `boolean` | `true` | 有值时显示清空按钮 |
| `disabled` | `boolean` | `false` | 禁用 |
| `suggestions` | `SearchSuggestion[] \| SearchSuggestionGroup` | — | Fuzzy/Sectioned 时的推荐 |
| `onSelectSuggestion` | `(s: SearchSuggestion) => void` | — | 选中推荐回调 |
| `options` | `SearchOption[]` | — | Sectioned 类型的维度选项 |
| `selectedOption` | `string` | — | 受控选中维度 |
| `defaultOption` | `string` | `options[0].value` | 非受控初始维度 |
| `onOptionChange` | `(value: string) => void` | — | 维度切换回调 |
| `className` | `string` | — | 根容器 |
| `menuClassName` | `string` | — | 推荐 menu |

### SearchSuggestion

| Prop | 类型 | 说明 |
|---|---|---|
| `value` | `string` | **必填**, unique 标识 |
| `label` | `ReactNode` | **必填**, 显示内容 |
| `emphasized` | `boolean` | 加重显示 (Roboto Medium) |
| `disabled` | `boolean` | 禁用此项 |

### SearchSuggestionGroup

```ts
type SearchSuggestionGroup = Record<string, SearchSuggestion[]>;
// 例: { Recommendation: [...], Others: [...] }
```

### SearchOption

| Prop | 类型 | 说明 |
|---|---|---|
| `value` | `string` | **必填**, unique |
| `label` | `ReactNode` | **必填**, 显示内容 |

---

## 5. 场景示例

### 5.1 Simple — Header 全局搜索
```tsx
<Search
  type="simple"
  placeholder="Search orders, products, users…"
  onSearch={(q) => router.push(`/search?q=${q}`)}
/>
```

### 5.2 Fuzzy — 商品搜索 (即时推荐 Plain)
```tsx
const [keyword, setKeyword] = useState('');
const suggestions = useDebouncedSuggestions(keyword);  // 远程联想

<Search
  type="fuzzy"
  value={keyword}
  onChange={setKeyword}
  placeholder="Find products…"
  suggestions={suggestions}
  onSelectSuggestion={(s) => goToProduct(s.value)}
/>
```

### 5.3 Fuzzy — 加重推荐 (Recommendation + Others)
```tsx
<Search
  type="fuzzy"
  suggestions={{
    Recommendation: [
      { value: 'r1', label: 'Top Product 1', emphasized: true },
      { value: 'r2', label: 'Top Product 2', emphasized: true },
    ],
    Others: [
      { value: 'o1', label: 'Other Product 1' },
      { value: 'o2', label: 'Other Product 2' },
    ],
  }}
/>
```

### 5.4 Fuzzy — Categorized (按类目分组)
```tsx
<Search
  type="fuzzy"
  suggestions={{
    'Products': [
      { value: 'p1', label: 'iPhone 15 Pro' },
      { value: 'p2', label: 'MacBook Air' },
    ],
    'Orders': [
      { value: 'o1', label: 'Order #2026-001' },
    ],
  }}
/>
```

### 5.5 Sectioned — 多维度搜索 (订单中心)
```tsx
const [scope, setScope] = useState('all');
const [query, setQuery] = useState('');

<Search
  type="sectioned"
  options={[
    { value: 'all', label: 'All' },
    { value: 'product', label: 'Product' },
    { value: 'order', label: 'Order' },
    { value: 'user', label: 'User' },
  ]}
  selectedOption={scope}
  onOptionChange={setScope}
  value={query}
  onChange={setQuery}
  placeholder="Search…"
  suggestions={getSuggestionsByScope(scope, query)}
  onSearch={(q) => searchByScope(scope, q)}
/>
```

### 5.6 禁用态
```tsx
<Search type="simple" placeholder="Loading…" disabled />
```

---

## 6. 视觉规格 (1:1 Figma)

| 项 | 值 | Token |
|---|---|---|
| Input 高 | 32px | `--Input-inputHeight` (复用) |
| Input padding | 6px 12px | `--Input-inputPaddingBlock/Inline` (复用) |
| Input gap (text↔icon) | 8px | `--Search-inputGap` |
| Input border-radius | 4px | `--Search-inputBorderRadius` |
| Input border default | `#E5E5E5` | `--Search-colorBorder` |
| Input border **active (focus)** | `#B7B7B7` (灰, 非橙) | `--Input-colorBorderHover` (复用) |
| Input bg | `#FFFFFF` | `--Search-colorBg` |
| Input bg disabled | `#F6F6F6` | `--Input-colorBgDisabled` (复用) |
| 文字 color | `#333333` | `--Search-colorText` |
| Placeholder color | `#B7B7B7` | `--Search-colorPlaceholder` |
| Icon size (search / clear) | 16px | `--Search-iconSize` |
| Icon color | `#999999` | `--Cascader-colorArrowIcon` (复用) |
| **Sectioned 接缝** | gap=0, Option 右两角=0 + 右 border=0; Input 左两角=0 + 保留左 border | (CSS `.rootSectioned`) |
| Menu border-radius | 4px | `--Dropdown-menuBorderRadius` (复用) |
| Menu shadow | 2 层柔阴影 | `--Cascader-menuShadow` (复用) |
| Menu padding-block | 8px | `--Dropdown-menuPaddingBlock` (复用) |
| Suggestion item 高 | 32px | `--Dropdown-itemHeight` (复用) |
| Suggestion item padding | 6px 12px | `--Dropdown-itemPaddingBlock/Inline` (复用) |
| Suggestion item hover bg | `#F5F5F5` | `--Dropdown-colorBgHover` (复用) |
| Suggestion **emphasized** | Roboto Medium | (font-weight: 500) |
| Section header font / color | 12px / `#999` | `--Search-sectionHeaderFontSize` / `--Search-colorSectionHeader` |

---

## 7. 反例 (AI 不能这样做)

| ❌ 错误 | ✅ 正确 | 原因 |
|---|---|---|
| `type="sectioned"` 但 Option 与 Input 之间留 gap | gap=0, 接缝处直角 + 共享 border | 严格旧规范, 用户红框指出过 |
| 激活态用橙描边 `--colorPrimary` | 用 hover 灰 `--Input-colorBorderHover` | Search 不同于 Input/Cascader, 设计规范明确 |
| 自画 🔍 / ⊗ / ▾ icon | 用 `<Icon name="search" />` / `<Icon name="error-s" />` / `<Icon name="arrow-down" />` | 铁律 #8 + #10 |
| `arrow-down-s` 用于 Sectioned Option select | 统一 `<Icon name="arrow-down" />` (完整版) | 用户明确指过 |
| Input box 在 Sectioned 中缺左 border | Input 保留全 4 边 border, **由 Option 取消右 border** | 用户红框指出过 |
| 没 onChange + 用 value 受控 | 加 onChange 或改 defaultValue | 受控不更新 = bug |
| suggestions 每次渲染新引用 | useMemo 包装或 useDebounce | menu 频闪 |
| onSearch 没防抖直接打 API | useDebounce 包 onChange, Enter 才 onSearch | 否则频繁请求 |
| Sectioned 无 options | 必须传 options, 否则降级为 simple/fuzzy | API 设计前提 |
| Fuzzy 输入空字符串还显示 menu | hasSuggestions 检查 (内部已做) | 空列表显示空 menu 体验差 |

---

## 8. Accessibility

- Root: `role` 无 (容器), Input `type="text"`
- Input: 原生 `<input>`, 浏览器原生 a11y
- 推荐 menu: `role="listbox"`, 每项 `role="option"`
- Clear button: `aria-label="Clear"`, `tabIndex={-1}` (不抢焦点)
- Search icon: `role="button"`, `aria-label="Search"`
- Sectioned Option select: 复用 `<Dropdown>`, 自带 trigger button + listbox a11y

键盘:
- Tab 进入 input
- 输入字符: Fuzzy/Sectioned 自动展开 menu
- Enter: 触发 onSearch
- Esc: 关闭 menu
- 点击外部: 关闭 menu

未来增强 (TODO):
- 上下方向键导航 suggestions + 自动 focus 第一项
- Cmd+K / Slash 快捷打开 (全局搜索场景)
- 搜索历史记录 (localStorage)
- 高亮匹配文本 (highlight 命中字符)

---

## 9. 历史变更

- **2026-06-08 v1** — Phase 5 + 多轮调整
  - 4 ComponentSet (SearchInput 12 + SearchItem 6 + SearchMenu 3 + Search 组合 3)
  - React Search: 3 type 统一组件, Portal menu, 复用 Dropdown 做 Option select 前置
  - suggestions 双形态 (数组 / 分组 map) — `isGroupedSuggestions` 自动判断
  - 受控 + 非受控 value / selectedOption
  - Esc + click-outside 关闭
  - 13 Token 新增 (8 Component + 5 Global), 大量复用 Input/Dropdown/Cascader token
  - **2026-06-08 修 1** — Sectioned 接缝: gap=0, 接缝处直角, 共享 1px border
  - **2026-06-08 修 2** — 激活态描边由 `#EE4D2D` 橙 → `#B7B7B7` 灰 (严格设计规范, 与 Input/Cascader focus 区分)
  - **2026-06-08 修 3** — Input 保留全 4 边 border, Option 取消右 border (避免接缝双线)
  - **2026-06-08 修 4** — HasOption=Yes variant 由 341w → 280w (Display 排版均齐, Input FILL 余下 179w)
  - Storybook 严格对齐 Figma: Matrix 3 cells = Type × 3 (Simple/Fuzzy/Sectioned); Variants 拆 Fuzzy 子形态 + Disabled
