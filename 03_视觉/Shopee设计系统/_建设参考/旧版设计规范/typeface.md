---
title: Typeface 字体
description: 字体作为产品信息传达的核心主体，我们需要保证每段信息在各个平台上有着合理且统一的显示体验。
designer: Ying Yi
tabs:
  - title: 设计文档
    href: /zh/design/typeface
  - title: 更新记录
    href: /zh/design/typeface/records
---

## 类型汇总

* 为了方便设计团队在日常设计协作中产出更加统一。设计师在设计产品页面时，英文字体首选使用 “Roboto” ，中文则使用 “Pingfang”；
* 以下类型汇总只适用于 EDS Desktop 的产品界面字段设计（暂不包含 Mobile 设计）。

|Category|Font-Size / Font-Weight|Line-Height（统一使用倍数值）|使用场景|
|:--|:--|:--|:--|:--|:--|
| <span style="font-size: 34px; font-weight: 700; line-height: 1.2;">Display</span> | 34px / 700（Bold） | 1.2 倍（约 41px） | Landing Page Title |
| <span style="font-size: 30px; font-weight: 500; line-height: 1.2;">Page Title</span> | 30px / 500（Medium） | 1.2 倍（36px） | 页面标题 1 |
| <span style="font-size: 26px; font-weight: 500; line-height: 1.2;">Large Title</span> | 26px / 500（Medium）| 1.2 倍（约 31px） | 特殊场景可用于作页面标题 |
| <span style="font-size: 22px; font-weight: 500; line-height: 1.2;">Medium Title</span> | 22px / 500（Medium）| 1.2 倍（约 26px） | 模块一级标题 |
| <span style="font-size: 18px; font-weight: 500; line-height: 1.2;">Small Title</span> | 18px / 500（Medium）| 1.2 倍（约 22px） | <ul><li>模块二级标题</li><li>弹窗标题</li><li>数据信息等</li></ul> |
| <span style="font-size: 14px; font-weight: 400; line-height: 1.2;">Body</span> | <ul><li>14px / 400（Regular）</li><li>14px / 500（Medium）</li></ul> | <ul><li>单行：1.2 倍（约 17px）</li><li>段落：1.5 倍（21px）</li></ul> | <ul><li>通常界面字段行高为 1.2 倍</li><li>段落内容（譬如文章）则为 1.5 倍</li></ul> |
| <span style="font-size: 12px; font-weight: 400; line-height: 1.2;">Caption</span> | <ul><li>12px / 400（Regular）</li><li>12px / 500（Medium）</li></ul> | 1.2 倍（约 14px） | <ul><li>辅助信息</li><li>标签文案通常为 Medium</li></ul> |

## 界面字段行高规则
::::row
:::col :span="6"
「界面字段」的布局设计和「文章排版」不同。

通常在界面设计中，「界面字段」line-height 需要保持安全的数值前提下，设计师尽可能通过元素与元素之间的间距进行精确设计。

为了避免 line-height 数值过大造成不同程度的设计还原问题，因此推荐「界面字段」的默认值为 **line-height: 1.2**。

如右图图所示，使用 line-height: 1.2 (Figma 值为 120%) 的效果。无论在单行或者多行的排版下都有着比较好的展示兼容性。

<span style="color: #666; font-size: 12px;">注：character-height = font-size * line-height</span>
:::
:::col :span="6"
![Line Height](assets/design/typeface/line_height.png =100%x)
:::
::::

## 字体家族
优秀的 Font System 首先是要选择合适的字体家族。Font-family 优先使用系统默认的界面字体，同时提供了一套利于屏显的备用字体库，来维护在不同平台以及浏览器的显示下，字体始终保持良好的易读性和可读性，体现了友好、稳定和专业的特性。
<br />
```
font-family: Roboto,system-ui,-apple-system,BlinkMacSystemFont,Helvetica Neue,Helvetica,Arial,sans-serif;
```
<br />

\* 详细参考「在 Web 内容中使用系统字体」：[https://csspod.com/using-the-system-font-in-web-content/](https://csspod.com/using-the-system-font-in-web-content/)
<br />

## 特殊应用

### 泰文排版应用

::::row
:::col :span="6"
由于泰文这类高形字（Tall）会占用较大的高度，需要针对此字体进行特殊 Line-Height 定义。 推荐将 Line-Height 定义为当前 Font-Size 的 **1.5 倍**。
:::
:::col :span="6"
![Thai Fonts](assets/design/typeface/thai_fonts.png =100%x)
:::
::::

### 运营性字体应用

::::row
:::col :span="6"
针对运营属性的页面排版设计（譬如 Banner），我们建议使用 Shopee Font 为主信息进行排版，使整体视验更符合 Shopee 品牌特性。

**目前 Shopee Font 2021 支持以下语种：**
* 拉丁文（譬如英文、印尼文）
* 泰文

关于 Shopee Font 详情和下载请前往：
[Shopee Font 官网](https://shopee.design/download#852)

:::
:::col :span="6"
![Ads Fonts](assets/design/typeface/ads_fonts.png =100%x)
:::
::::

## 场景示例

### 排版示例 1

![Scenario Example 1](assets/design/typeface/scenario_example_1.png =100%x)

### 排版示例 2

![Scenario Example 2](assets/design/typeface/scenario_example_2.png =100%x)

### 排版示例 3

![Scenario Example 3](assets/design/typeface/scenario_example_3.png =100%x)

### 排版示例 4

![Scenario Example 4](assets/design/typeface/scenario_example_4.png =100%x)
