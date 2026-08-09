# 交互

本目录负责 Step 2 的市场调研、方案发散、流程完整性检查和可点击粗原型。

**「链路完整」= 主流程完整。** 主流程（可见入口 → 核心任务 → 预览或确认 → 返回或取消 → 成功 → 状态更新 → 再次进入）必须做成可点击并实际走通；边界情况（失败、恢复、加载、权限、空态、超量、数据变化、中断恢复）必须完成内部定义，但只在画板中以 `情况｜系统处理` 的简短中文标注呈现，不默认做成交互。只有某个边界会改变方案的核心机制或成立条件时，才并入主流程原型。

调用顺序：

1. [`research-market-solutions/SKILL.md`](research-market-solutions/SKILL.md)
2. [`explore-interaction-directions/SKILL.md`](explore-interaction-directions/SKILL.md)
3. [`build-rough-prototypes/SKILL.md`](build-rough-prototypes/SKILL.md)

包内依赖：

- [`agent-reach`](agent-reach/SKILL.md)：市场证据和网页来源
- [`通用视觉规范`](../03_视觉/develop-visual-solution/references/通用视觉规范.md)：粗原型阶段的信息层级、布局密度与文案表达
- [`图表选型`](../03_视觉/develop-visual-solution/references/图表选型.md)：涉及图表时的类型选择与兜底

> `ui-ux-pro-max` 已于 2026-08-09 移出流程，目录暂时保留但不再安装、不再调用。其唯一有价值的图表选型知识已收编为上面的 `图表选型.md`。原因见 [`依赖清单`](../00_总流程/setup-design-loop/references/依赖清单.md)。

市场调研强制调用 `agent-reach` 与 Mobbin，但不下载或归档竞品图片。AI 自行提出研究问题，把研究得到的机制、来源与适用理由直接映射到粗方案。

最终只向用户交付一个 HTML 画板：其中包含 3 个基于同一节点级 Figma 原稿、通过超高还原 QA 且主流程完整可点击的方案，并用简体中文写明各方案优缺点、研究借鉴、边界情况、AI 推荐和当前项目机会。页面内产品文案仍使用 Step 1 已确认的目标市场语言。

每次生成或更新画板都必须在同一视口、同一状态执行原稿并排、50% 叠加和可用时的像素差异 QA；未改区域有肉眼可辨差异就继续修改。Figma 复制导致商品图丢失时，先恢复原素材，再依据标题或 SKU 从公开电商商品页补充同款或同品类近似高清图片。三个方案须两两存在至少 2 项本质机制差异；推荐理由必须分为产品满足度与交互优势。边界流程完成内部定义后以简短中文标注，不默认做成交互。
