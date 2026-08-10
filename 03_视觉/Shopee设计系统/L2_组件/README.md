# L2 组件

单组件的用法、约束、变体选择与反例。

## 入口

[`组件索引.md`](组件索引.md) —— 从 L3 定完骨架后，在此找到组件，再进入对应的 `components/{X}/{X}.usage.md`。

只读取本次页面实际使用的组件文档，不批量加载 `components/`。

## 内容

- `组件索引.md`：状态、componentKey、何时用、详细用法链接；另含原子构成件与整页模板清单
- `components/`：30 份 usage 文档 + Icon 库（约 100 个）+ Illustration（10 个）

⚠️ 引用组件用 `componentKey`，不用 node-id。索引中 6 个历史 node-id 已在 2026-08-09 探活中确认失效。

⚠️ library 中已建但**没有** usage 文档的组件（Toolbar、Spin、Skeleton、Progress、Rate、Slider、Upload、Anchor、Chart、Input、TextArea、CategorySelector、Line）在索引中标为 🔷。它们可以正常使用，变体属性直接读 Figma。

## 已知问题

**文档代际不一致。** 只有 Button、Table、Popover、Steps 四份是「变体属性契约」格式；其余 26 份仍是 React props 版，属性表（`onChange`、`defaultChecked` 等）与 Figma 变体属性不对应。

在改写前，变体属性以 Figma 为准，usage 文档中仍然有效的是：决策树、何时用 / 何时不用、组合模式、反例。

改写模板见 `_建设参考/组件文档模板.md`（该资料已于 2026-08-10 移出包，归档在包外 `Design-loop-归档/_建设参考/`）。

## 边界

- 组件文档决定单组件用法，不替代 L3 页面骨架。
- 变体属性与文档冲突时，以当前 Figma ComponentSet 为准。
- 找不到精确组件时先检查组合方式；新增组件必须进入组件库建设流程。

## 建设优先级

**文档改写**（组件已建，缺 usage）：按列表页所需排序 —— Toolbar、Header、Sidebar、Filter、Pagination、Card、Alert、Tabs。Toolbar 排第一位：它是列表页批量操作的骨架件，库中已建但至今无文档。

**组件建设**（库中确无）：ResultBar 优先，它是列表页骨架唯一无法用组合完整替代的缺口。
