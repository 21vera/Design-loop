# 视觉

本目录负责 Step 3 和 Step 4。

- [`develop-visual-solution`](develop-visual-solution/SKILL.md)：视觉澄清、Figma 输出和反馈修改
- [`Shopee设计系统`](Shopee设计系统/)：Shopee Guideline、组件文档、Token 与检查项——**本项目的规范真源**
- [`通用视觉规范`](develop-visual-solution/references/通用视觉规范.md)、[`图表选型`](develop-visual-solution/references/图表选型.md)：通用设计知识兜底层，用于补 Shopee 留白
- [`frontend-design`](frontend-design/SKILL.md)：**不强制读取**。写作原则已内化到 `clarify-product-requirement` 与 `通用视觉规范` §六；全文 55 行中 44 行是与本项目 Token、组件锁定冲突的视觉主张。保留作为上游对照的可选参考

规范优先级：**Shopee 有定义 → 用 Shopee；Shopee 留白 → 用通用视觉规范与图表选型；两者都没有 → AI 依通用设计判断并说明依据。留白必须补足，不能因为规范没写就跳过。**

**出图前必过设计规范门禁**：完整读取 [`Shopee设计系统/L1_原子变量`](Shopee设计系统/L1_原子变量/README.md) 与 Figma `✅ Design Token 设计令牌` 页（`Seller Center Library` node `1:2`），再按需读取组件层与页面层。Token 层每轮重新读取，不允许降级、凭记忆或沿用上一轮结果。组件与页面文档可能落后于 library，按 L5「未建组件降级规则」处理并登记。完整定义见 [`设计规范门禁`](../00_总流程/Design%20Loop总流程与调用时机.md)。

**交付前必须自检并回环**：Token 清单比对 + L5 检查项 + 结构健壮性 + 页面完整性。未全部通过就回到出图步骤修改并重新自检，持续循环，不交付半成品。

每次生成、编辑、合成或更新视觉稿前，必须成功调用 Product Design 的具体工作流；自动调用失败时停止出图并提示用户 `@Product Design`。

视觉阶段只执行已选定的产品与交互方向，不改变上游目标和核心链路。

用户提供的视觉规范、截图和反馈必须转成逐条验收矩阵；所有客观要求和页面完整性检查全部通过后才输出待确认稿，用户明确确认后才标记为定稿。
