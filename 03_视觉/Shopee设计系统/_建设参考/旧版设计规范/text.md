---
title: Text Rules 文案规则
description: 语言是内容的载体，承载了系统和用户交流的信息。语法和句法是文案内容需要遵循的规则和组成方式。在组织内容时，目标是让用户能正确接受到所包含的意义，因此必须做到内容精炼且含义明确。在文案内容保持一致的基础上，可以通过不同的语气来传达不同的情绪和态度
designer: Wei Huang
tabs:
  - title: 设计文档
    href: /zh/design/text
  - title: 更新记录
    href: /zh/design/text/records
---

## 通用原则
<br />

1. **一致性**（包含三个方面的一致）：
- 导致相同结果的相同操作文案必须一致；
- 同一层级的句式结构需保持一致。例如，一个导航中的各个tab，统一使用名词；操作菜单列表统一使用动词；
- 目标和结果一致。导航型组件和跳转后的内容应该相符，例如导航文案和内容标题一致
2. **含义明确** 避免模棱两可和歧义。通过增加语境约束可以有效避免表意不清。
3. **内容精炼** 减少不必要的文字。尤其在多语言的环境下，避免啰嗦、长篇大论。
4. **通俗易懂** 尽量避免专业用语，使用通俗易懂贴近用户习惯的语言。
5. **认真严谨** 语言尽量专业严谨。例如行为确认按钮使用 Confirm 而非 Yes、OK、I got it 等。

## 常用类型文案
### 1. 功能文案
【语言】语句采用：使用名词、动词、祈使句。明确地告诉用户应该做什么，结果是确定的；
【常用于】按钮、导航。

:::: row
::: col :span="5"
#### 1.1 命令型按钮
【规则】命令型按钮，使用动词或祈使句来指示用户的行为。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1i6f6hcjM2wYKf-G4Ra2TLbiRK_cdGNwa =100%x)
:::
::::


:::: row
::: col :span="5"
#### 1.2 导航型按钮
【规则】导航型按钮可以使用名词，指示去向的内容。通常是板块、页面、文章的标题。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1Pe1FaIs5clVgqvkLwqcMm3MjqlC2rMXh =100%x)
:::
::::

:::: row
::: col :span="5"
#### 1.3 开关型按钮
【规则】开关的文案表示开关的状态，和开关按钮分离。文案写在开关上可能造成混淆，是指示当前状态还是开关的行为。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1Lzkdx7e8jr38yylwGle_POkaXt0CY_gK =100%x)
:::
::::

:::: row
::: col :span="5"
#### 1.4 「更多」按钮
【规则】可表示跳转新页面 / 跳转详情页 / 更多操作下拉菜单。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1ugkOg9AMfFIye0M99KqsQuxd5ci7n4ds =100%x)
:::
::::

:::: row
::: col :span="5"
#### 1.5 「展开收起」按钮
【规则】
- 「Expand」展开 /「Collapse」收起：表示面板的展开和收起；
- 「View All」查看全部 / 「Collapse」收起：文字内容的展开和收起。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1jR_Z3n1Ts_y9OAVC4b4Sb5l64T7oEnFd =100%x)
:::
::::

:::: row
::: col :span="5"
#### 1.6 步骤型按钮
【规则】
- 「Expand」展开 /「Collapse」收起：表示面板的展开和收起；
- 「View All」查看全部 / 「Collapse」收起：文字内容的展开和收起。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1qMf1opXYhdfcxQEGwgrFYzC6Y0Zahz8G =100%x)
:::
::::

:::: row
::: col :span="5"
#### 1.7 行为确认型按钮
【规则】
- 弹窗中的行为按钮尽量使用具体的、和任务相关的动词，而不是 Yes/No 等通用文案。这样可以帮助用户在不完全阅读信息时，也能快速进行操作；
- 二次确认的用户行为避免和弹框的取消按钮相冲突。### 三级标题
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1qMf1opXYhdfcxQEGwgrFYzC6Y0Zahz8G =100%x)
:::
::::

### 2. 警告文案
【语气】应果断、坚决。突出用户将会面临的后果，达到警示作用。可以使用警告色、感叹号加强警示效果。
【常用于】弹窗、警报、Toast。
【建议】
- 确认/Confirm：较强烈的肯定语气，用于表示确定进行某一行为；
- 确定/OK：语气较轻，用于表示知、了解；
- 弹窗按钮不要使用关闭/Close，有可能误解为关闭该页面、功能。
<br />

:::: row
::: col :span="5"
#### 2.1 行为确认型按钮
【规则】常用于在用户进行某一行为前进行警告或二次确认。
【类型】
- 一般情况；
- 严重警告；
- 直接写出警告、错误的文案；
- 错误提示弹框：常用于在某一错误发生之后提示用户相关信息，必要时给予一定帮助信息。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1m58_TtBk-RRoCZuJ1prfgrogWeRoP2Z7 =100%x)
:::
::::

:::: row
::: col :span="5"
#### 2.2 反馈弹框
【规则】在警告中尽量提供解决方案，而不仅仅是错误名称。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1LLN9zYsR5uIUcLucOktJ-d7hB1bLWdXd =100%x)
:::
::::

:::: row
::: col :span="5"
#### 2.3 表单报错
【规则】在警告中尽量提供解决方案，而不仅仅是错误名称。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1uuFiBQmGWZlBrzsgJoD1HiBNlUOlqDrP =100%x)
:::
::::

### 3. 说明文案
【语言】语句采用：使用名词、陈述句。以支持者的角度给予用户鼓励和有效的帮助。语气友好、亲近，必要时可以使用语气助词，增加亲和感。
【常用于】登陆页、落地页、缺省页、新手引导。

:::: row
::: col :span="5"
#### 3.1 标签
【规则】标签无操作行为，避免使用动词或祈使句。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1sqDhD31-eiAMf2CAr46SXBy9ldFgIY22 =100%x)
:::
::::

### 4. 帮助文案
【语言】语句采用：使用名词、形容词或陈述句。应中性、平实。避免带有主观态度和感情色彩，旨在清晰准确地向用户解释说明某一事物。
【常用于】Tooltips名词解释、表单填写、帮助文档。

:::: row
::: col :span="5"
#### 4.1 提示气泡
【规则】标签无操作行为，避免使用动词或祈使句。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1miS63_cHQSHIq453ia-sXJIbBP1ZEGZu =100%x)
:::
::::

:::: row
::: col :span="5"
#### 4.2 新手引导
【规则】
- 前一步为「back」，下一步「Next」；
- 介绍类弹窗按钮文案统一为「OK」；
- 跳过为「Skip」；
- 引导性按钮「Yes，try it」。
:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=158gCrT_g_eIGXda-C5hNQPfaYWIfGtpr =100%x)
:::
::::

## 标点符号说明
:::: row
::: col :span="5"
### 1. 字符格式 
【规则】
- 中文标点符号为全角（省略号、星号除外）;
- 其他语言标点符号为半角。

### 2. 标点的省略
【规则】
- 完整的句子句末必须有句末点号;
- 祈使句单独出现时可以省略句末点号;
- 文字按钮不使用句末点号。

### 3. 空格的使用
【规则】
- 句中的半角标点符号后有一个空格;
- 左引号前面有一个空格，右引号后面有一个空格。

### 4. 分项列举
【规则】
- 中文环境：末尾可以使用分号或句末点号;
- 其他语言环境：末尾可以使用逗号或句末点号；
- 最后一项使用句末点号。
:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=14fHPtXEHdbIzd_ph5hf38BnX2R6uKyxI =100%x)
:::
::::

#### 附录1: 常用标点汇总

1. 「句内点号」：表示句内各种不同性质的停顿；
2. 「句末点号」： 表示句末的停顿和句子的语气；
3. 「标号」： 标示某些成分的特定性质和作用。

<table>
  <thead>
    <tr>
      <th>符号类型</th>
      <th>符号名称</th>	
      <th>简/繁中文</th>
      <th>EN/VN/ID/MY/TH</th>
      <th>备注</th>	
   </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4" style="font-weight:500">句内点号</td>
      <td>逗号 Comma</td>
      <td>，</td>
      <td>,</td>
      <td>表示短暂停顿</td>
    </tr>
    <tr>
      <td>顿号</td>
      <td>、</td>
      <td>无</td>
      <td>仅中文环境使用顿号，其他语言通常使用逗号代替</td>
    </tr>
    <tr>
      <td>分号 Semicolon</td>
      <td>；</td>
      <td>;</td>
      <td>-</td>
    </tr>
    <tr>
      <td>冒号 Colon</td>
      <td>：</td>
      <td>:</td>
      <td>-</td>
    </tr>
    <tr>
      <td rowspan="3" style="font-weight:500">句末点号</td>
      <td>句号 Period</td>
      <td>。</td>
      <td>.</td>
      <td>1.表示陈述语气和较缓和的祈使语；2.表示英文缩写。</td>
    </tr>
    <tr>
      <td>问号 Question Mark</td>
      <td>？</td>
      <td>?</td>
      <td>-</td>
    </tr>
    <tr>
      <td>感叹号 Exclamation Mark</td>
      <td>！</td>
      <td>!</td>
      <td>表示警告或渲染气氛。建议谨慎使用。不建议多个感叹号连用。</td>
    </tr>
    <tr>
      <td rowspan="6" style="font-weight:500">标号</td>
      <td>引号 Quotations</td>
      <td>“”</td>
      <td>“”</td>
      <td>-</td>
    </tr>
    <tr>
      <td>连字符 Hyphen</td>
      <td>-</td>
      <td>-</td>
      <td>表示合成词。使用时前后没有空格，输入方式为minus。</td>
    </tr>
  </tbody>
</table>

<br />

#### 附录2: 连接符号的种类
<br />

| |Hyphen连字符（小）|En Dash连接号（中）|Em Dash破折号（大）|
|:--|:--|:--|:--|
|**样式**|-|-|-|
|**输入方式**|减号|option+减号|连续两个减号/option+shift+减号|
|**主要用法**|连接合成词|表示数字、日期、时间等连续范围|表示语气转折（破折号）|
|**示例**|Real-time|12 June – 3 July / 1 – 3 days|-|

## 大小写说明

:::: row
::: col :span="5"
【规则】
- 句子第一个单词首字母大写，小写不够正式；
- 句子避免全部大写，全大写语气过重，且不易阅读；
- 合成词第一个单词首字母大写；
- 标题、词组每个单词的首字母大写；
- 节日、月份、星期、地名首字母大写；
- 专有名词和缩写大小写应遵循固定用法；
- 介词以及and、but、for、or、nor、to、as小写；
- 其他用法遵循英文大小写使用规范。

:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1_HRmEzzcx-794ajiZtKtwGQeBW8kFjxe =100%x)
:::
::::

## 缩略说明
:::: row
::: col :span="5"
【场景规则】
- 用于内容长度超出容器限制时；
- 用于减少重复信息时；
- 避免用于标题、导航、按钮等。

【使用规则】
- 使用「…」代替不显示的部分。
- 使用 Tooltip 展示完整信息，详情请参见 Tooltip 规则。
:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=10aTlp4oFSdZetGHgnbH68Ubv5I9Ns0_9 =100%x)

:::
::::





