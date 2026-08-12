# Case 文件夹模板

> **⚠️ 唯一来源声明**：本目录是 Design Loop 全部「输出结构」的唯一数据源。各 SKILL.md 的输出/输入定义只写「按对应模板输出」+ 差异点，不再内嵌完整输出结构。改动输出结构时只改本目录，再同步各 SKILL 的差异点描述。

本目录是保留在 Design Loop 包内的只读源模板。每个新 Case 由 AI 自动复制到桌面 `Design Loop Cases/<Case名称>/`，各步骤只写入桌面副本的对应文件夹。

不得在本模板目录内直接开展真实 Case，也不得把过程稿、截图、HTML、研究结果、Figma 链接或反馈记录写回源包。

目标 Case 目录已存在时不得覆盖；确认属于同一 Case 才续写，否则使用不冲突的新目录名。

## 模板 ↔ SKILL 引用关系

| 模板 | 对应 SKILL 输出 | 引用方式 |
|---|---|---|
| `01_需求澄清/需求总结模板.md` | `01_产品/clarify-product-requirement/SKILL.md` | SKILL 按本模板输出 + 只写差异点 |
| `02_竞品调研/研究摘要模板.md` | `02_交互/research-market-solutions/SKILL.md` | SKILL 按本模板输出 + 只写差异点 |
| `03_粗方案/方案评估模板.md` | `02_交互/build-rough-prototypes/SKILL.md`、`02_交互/explore-interaction-directions/SKILL.md` | SKILL 按本模板输出 + 只写差异点 |
| `04_Figma/视觉预期与链接模板.md` | `03_视觉/develop-visual-solution/SKILL.md` | SKILL 按本模板输出 + 只写差异点 |
| `05_反馈/反馈记录模板.md` | `03_视觉/develop-visual-solution/SKILL.md`（Step 4） | SKILL 按本模板输出 + 只写差异点 |

```text
Case名称/
├── 01_需求澄清/
├── 02_竞品调研/
├── 03_粗方案/
├── 04_Figma/
└── 05_反馈/
```

## 写入时机

| 步骤 | 写入目录 |
|---|---|
| Step 1 | `01_需求澄清` |
| Step 2 市场研究 | `02_竞品调研`，只保存必要文字结论，不保存竞品图片 |
| Step 2 粗方案 | `03_粗方案`，保存统一 HTML 画板与简要评估 |
| Step 3 | `04_Figma` |
| Step 4 | `05_反馈`，定稿链接同步更新到 `04_Figma` |
