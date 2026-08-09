---
title: Adaptation 适配
description: 使用统一的元素和规则来确保不同屏幕尺寸之间的一致性，为创建和谐、秩序、易于遵循的页面体验提供基础。
designer: Gewei Feng
---

## 界面的适配

### 统一画板

为了尽可能减少沟通与理解的成本，组织内部设计画板使用统一的尺寸。Seller 与 Supply Chain 默认的画板尺寸为 1366px，Pepole Team 默认的画板尺寸为1920px。由于B端产品线较多，服务人群亦有所不同，设计师可根据产品对应用户的主流分辨率做调整。

### 栅格系统

以规则的网格阵列来指导和规范网页中的版面布局以及信息分布。不仅可以让网页的信息呈现更加美观易读，更具可用性。而且，对于前端开发来说，界面将更加的灵活与规范。

#### 栅格元素

- **边距（Margins）**：栅格设计区域外与屏幕或元素左右间的距离；
- **栏（Columns）**：是盛放内容的区域；
- **水槽（Gutters）**：是两个栏中间的间距，有助于分隔内容和列之间的空间。

![Grid Element](assets/design/adaptation/grid_element.png =100%x)

#### 栅格单位

- PC端我们采用8px为基础，倍数增加；
- 采用 24 栅格体系，在适配时通常水槽的宽度不变，栏的宽度会随之伸缩。

#### 应用规则

- 尽量保持偶数思维；
- 父级元素需对齐栅格，子级可以不完全对齐列，如有必要子元素可再做栅格；
- 内容元素必须位于若干Column上；

::::row
:::col span="6"
![Application Rule Good 1](assets/design/adaptation/application_rule_good_1.png =100%x)
:::
:::col span="6"
![Application Rule Bad 1](assets/design/adaptation/application_rule_bad_1.png =100%x)
:::
::::

- 除非有意，否则不要把Column作为外部填充；

::::row
:::col span="6"
![Application Rule Good 2](assets/design/adaptation/application_rule_good_2.png =100%x)
:::
:::col span="6"
![Application Rule Bad 2](assets/design/adaptation/application_rule_bad_2.png =100%x)
:::
::::

- 安全边距有助于保证界面可读性和美观度，安全边距一般不小于水槽宽度；

::::row
:::col span="6"
![Application Rule Good 3](assets/design/adaptation/application_rule_good_3.png =100%x)
:::
:::col span="6"
![Application Rule Bad 3](assets/design/adaptation/application_rule_bad_3.png =100%x)
:::
::::

- 水槽宽度越大，界面留白和呼吸感会更好，反之则更紧凑。PC端水槽建议不要超过32px。

::::row
:::col span="6"
![Application Rule Good 4](assets/design/adaptation/application_rule_good_4.png =100%x)
:::
:::col span="6"
![Application Rule Bad 4](assets/design/adaptation/application_rule_bad_4.png =100%x)
:::
::::

### 适配类型汇总

在设计过程中，设计师还需要建立适配的概念，根据具体情况判断系统是否需要进行适配，以及哪些区块使用何种适配方案更合适，以使得界面有更好的浏览阅读体验。

| 名称 | 使用场景 | 布局特点 | 设计方法 |
|:-|:-|:-|:-|
| **响应式布局** | <ul><li>用于解决不同分辨率之间的兼容</li><li>常用于复杂类型网站设计</li></ul> | <ul><li>为不同设备、视口提供不同版本的设计，即创建多个布局，每个布局对应一个屏幕分辨率范围</li><li>一定范围内，屏幕分辨率变化时，页面里元素的宽度或高度变化，但整体布局不变</li></ul> | <ul><li>主要变化区域的尺寸使用百分比定义，可以根据可视区域和父元素的实时尺寸进行调整，尽可能的适应各种分辨率</li><li>往往配合 max-width/min-width 等属性控制尺寸变化范围以免过大或者过小影响阅读</li><li>建议选择2~3个主流分辨率进行适配即可</li></ul> |
| **静态布局** | <ul><li>不需要兼容不同分辨率</li></ul> | <ul><li>页面元素与布局固定，不随屏幕分辨率变化而变化</li><li>当屏幕分辨率小于页面内容大小时，则出现滑动条</li></ul> | <ul><li>设定好页面宽度与元素宽高、位置即可</li></ul> |

### 经典布局适配方案

界面适配方案并非要限制设计产出，更多的在于引导设计者如何做到「更好」。设计师也可以根据产品特性探索更多适合的适配方案。下面以Seller Center为例，列举2种常用方案。

据统计，使用Seller Center的用户的主流分辨率为1920px、 1366px，个别系统还存在 1280px 的显示设备。

#### 1. 固定侧边栏，内容响应式布局

【使用场景】

- 适用于导航内容与信息层级较为多且复杂的情况，该布局具备较好的扩展性；

【适配方案】

- 将左边的导航栏固定，对右边的内容区域进行动态缩放。
- 侧边栏：固定宽度=220px
- 内容区（去除安全边距）：min-width=1012px，max-width=1620px
- 屏幕横向分辨率在1280px ~ 1920px间，信息可完整展示，内容区采用24栅格响应式布局，Column用百分比定义
- 屏幕横向分辩率在1280px ~ 1536px间，margin=24，gutter=16
- 屏幕横向分辨率1537px ~ 1920px间，margin=40，gutter=16
- 屏幕横向分辨率＜1280px，主内容区信息可能被遮挡，出现滚动条，同时可考虑收起侧边导航或增加适应此区间内布局来达到更好的展示效果。

![Classic Layout 1](assets/design/adaptation/classic_layout_1.png =100%x)

#### 2. 无侧边栏，静态布局

【使用场景】

- 适用于需聚焦操作流程或信息内容的次级场景。

【适配方案】

- 主内容区域固宽，始终与浏览器可视区域水平居中对齐；
- 屏幕横向分辨率在1280px ~ 1920px间，信息可完整展示，内容区width=1232px，gutter=16，min-margin=24；
- 屏幕横向分辨率＜1280px，主内容区信息可能被遮挡，出现滚动条。

![Classic Layout 2](assets/design/adaptation/classic_layout_2.png =100%x)

## 组件的适配

组件适配即组件自适应屏幕或模块，描述了视觉呈现（填充、大小、布局或对齐）的变化，或将一个组件切换为更适合设备大小和用例的另一个组件。这种类型的适配会影响内容和对象在屏幕上的比例和位置，以及它们之间的关系。所以在做组件适配时，每个组件均需考虑其大小限制，以及缩放组件时，定义其内部元素相对于容器的位置和对齐方式。设计师可从以下几个维度描述。

| 属性 | 值 | 注意点 |
|:-|:-|:-|
| **容器尺寸** | <ul><li>默认容器尺寸</li><li>外边距 (margin)</li><li>填充的最大值和最小值</li></ul> | 屏幕分辨率变化时，页面里元素的宽度或高度变化，但整体布局不变 |
| **边框** | <ul><li>粗细</li></ul> | 边框=1px ，一般不需要响应式变化 <br /> 边框＞1px ，如果需要响应式变化需标注 <br /> <span style="color: #EE4D2D">（组件如果有边框，请统一使用内边框）</span> |
| **元素尺寸** | <ul><li>默认元素尺寸</li><li>填充的最大值和最小值</li></ul> | 文字：一般不变 <br /> 图标：与文字并排的图标宽高与 font-size 不一样，需则考虑是否需要适配 |
| **内容结构** | <ul><li>内部各元素相对于容器的位置（内边距 padding )</li><li>内部个元素之间的间距</li><li>对齐方式</li></ul> | - |

![Component Adaptation](assets/design/adaptation/component_adaptation.png =100%x)

【Tips】

设计师与开发沟通界面或某模块使用组件的适配方案时需请注意：

1. 清晰的定义动态布局范围
2. 关键数据的交付（尺寸、安全范围、间距、位置等）
3. 为了保障用户可用性，请设置清晰的点击区域，PC端最小点击区域不要小于 16*16px。
4. 对于缩放复杂的组件时，如应用栏，内部元素可以分组并锚定到容器内的多个点。
