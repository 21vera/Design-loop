---
extend: /zh/components/modal
---

## 组件元素

:::: row
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1kf1uD6h-xE8m7I0aJGB0hiMwBN_Uf7hZ =100%x)
:::
::: col :span="6"
1. **标题**：简明扼要，直击要义，建议不超过一行；
2. **副标题 (可选)**：，当标题过长或者不能尽其意时，可使用标题+副标题的形式；
3. **关闭按钮**：主动点击后关闭当前弹窗；
4. **内容**：包括文本、表单、表格等，一般承载引导信息、解释信息或操作项，需要用户阅读、操作和查看；
5. **主操作区**：位于操作层右侧，需要用户做决策，主动点击后关闭当前弹窗；可以是1个按钮或2个按钮，复杂场景中最多允许出现3个；
6. **辅操作区 (可选)**：位于操作层左侧，一般为拓展的提示性的文字或简单操作，可以与弹窗本身、内容区信息相关，如：已选择n项等文字提示，不再提示、全选等。
:::
::::

## 类型汇总 & 使用用法
【通用用法】
 - 用户触发操作后，在页面中央弹出弹窗，弹窗以外区域使用遮罩；
 - 触发弹窗后，点击弹窗以外区域，弹窗不可关闭；
 - 按钮文案可根据具体业务场景自主定义，但请确保按钮文案简洁易懂。
:::: row
::: col :span="6"
### 1. 普通提示弹窗
【使用场景】

对用户进行信息知会，不需做决策的情况下均可使用。

【使用规则】

用户点击“Confirm”按钮或关闭按钮，弹窗消失。


:::
::: col :span="6"
### 2. 普通确认弹窗
【使用场景】

用户触发某一个操作后，需用户做出继续进行的判断，常用于二次确认弹窗。

【使用规则】

 - 相较于提示弹窗，确认弹窗提供2个选择，让用户做决策或者关闭弹窗，其中“Cancel按钮”是作为一种判断操作而出现，区分“Close按钮（关闭X）”的意义； 
 - 操作区最右侧为优先级高的操作，另一个按钮执行与前者相反的操作；
 - 点击“Confirm”，弹窗消失并执行弹窗内的所有操作；
 - 点击“Cancel”，弹窗消失且取消执行弹窗内的所有操作；
 - 点击“关闭”按钮，弹窗消失但且不执行弹窗内的所有操作。
:::
::::
:::: row
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=18WsoCj0Hhva2Ag78TscoYj5J1n6tQHPj =100%x)
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1p0UBbkQs-saBHdmIpgXZOemk1shhd8uW =100%x)
:::
::::
:::: row
::: col :span="6"
### 3. 含自定义辅助操作/信息的弹窗
【使用场景】

- 用于需为弹窗提供全局拓展的提示性的文字或简单操作的场景，如：已选择n项等文字提示，不再提示、全选等。

【使用规则】

- 弹窗操作区所包含辅助操作可分为两类：1. 影响弹窗内容或与弹窗内容相关的描述，如“全选”“已选择n项”；2. 影响弹窗本身的操作，如“勾选后不再提醒”；
- 设计师可根据业务场景合理选择辅助区所承载操作，但所搭载组件需遵守组件本身的规则。

:::
::: col :span="6"
### 4. 带简单操作弹窗
【使用场景】

- 用于当用户触发某操作之后，必须先进行某项任务，才能到达目标的场景。如登录，密码二次确认、重要信息修改等。

【使用规则】

 - 操作区用法同基础确认弹窗；
 - 在内容区展示需要用户确认的表单或操作，关于表单或操作的校验与对应组件规范保持一致；
 - 当表单较复杂、信息较多时，可考虑使用带步骤的弹窗或者新开一个页面承载。
:::
::::
:::: row
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1CJItqz0EU_C2pHqS76vMjpQfjujjO0pd =100%x)
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1CqMpR8PMSnIUmHJMPitSw2epQlg9YxP6 =100%x)
:::
::::
:::: row
::: col :span="6"
### 5. 带多步骤弹窗
【使用场景】
- 在当用户触发某操作之后，必须先按先后关系处理某些任务才能达到目标，可使用此类型弹窗，以降低用户操作成本，专注当前内容。

【使用规则】
 - 操作区用法同基础确认弹窗；
 - 进入下一步操作时，可通过“Back”按钮，返回上一步；
 - 关于表单或操作的校验与对应组件规范保持一致；
 - 当步骤超过3次时，建议在内容去增加步骤条提示。
:::
::: col :span="6"
### 6. 带插图弹窗
【使用场景】
- 可用于成功、失败等状态的提示、新手引导、或带有情感化色彩的弹窗。

【使用规则】
- 该弹窗只是从信息排版上与上述弹窗不同，使用用法没有差异；
- 当作为提示作用出现在业务场景中，用法同普通提示弹窗；
- 当作为确认作用出现在业务场景中，用法同普通确认弹窗。

:::
::::
:::: row
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1LTiq4bh-ZHTGBWJ35E1xeommugCCWx-H =100%x)
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1HZIOV2C_HZuwdpDatZtc33FchA70F4Jt =100%x)
:::
::::
### 7. 自定义弹窗
【使用场景】
- 适用于内容区已承载多个通道入口载体的场景。

【使用规则】
- 自定义弹窗标题区同普通弹窗用法一致，无底部操作区。内容区可根据业务场景自定义，但需承载执行后可以关闭弹窗的操作或入口。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1-LmaH-y6q2nCLx83Un28ZCO1DYgZYKHZ =100%x)
### 8. 含复杂组件组合的弹窗
【使用场景】
- 用于用户触发与当前页面强相关的、需要用户集中处理的任务，且任务本身由多级或多种不同复杂组件组合而成的场景。其与新开页面的区别在于：弹窗确认后，不打断用户在页面内进行主要流程的其他操作，如：图片编辑，选择商品等。

【使用规则】
 - 标题区与操作区同普通弹窗用法一致；
 - 内容区的复杂组件的操作与对应的子组件规范保持一致；
 - 此类型弹窗内容区的结构多元，包括但不限于右侧样式，还有上下结构或者更复杂的结构，根据当前场景设计，遵循使用规则即可。

![test](https://drive.google.com/thumbnail?sz=w3000&id=11DmIUlJRaYdusV98a9XOGmRJHHD8-hn0 =100%x)


## 视觉样式
### 1. 基础样式
:::: row
::: col :span="6"
#### 1.1 页面位置关系及样式
- 背景遮罩样式：background: rgba(0,0,0,0.50)；

- 弹窗面板样式：background: #FFFFFF；border-radius: 4px；box-shadow: 0 1px 8px 0 rgba(0,0,0,0.12)。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1lXNmY53fooW9wbljzW8dwnh8rVSIPR42 =100%x)
:::
::::
#### 1.2 弹窗尺寸
- Normal尺寸用于常规的简单文本提示、简单表单输入以及带插图的弹窗；
- 若弹窗内容较丰富度较高，可根据内容丰富度选择Medium、Large和Ex-Large尺寸；
- 若弹窗内容结构较复杂，以下尺寸均无法满足，可根据具体场景自定义弹窗尺寸，弹窗宽度最小值400px，最大值1104px。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1wn8fVkz_4QAUbqSStRXFf1WSmVsWRYC0 =100%x)
<br />

**自适应高度弹窗示例**

![test](https://drive.google.com/thumbnail?sz=w3000&id=17F67CrKf-Nt7uheh2FivRxMv3nFC300a =100%x)
<br />

**固定高度弹窗示例**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1F9DqJyQhU83Q956Txn3C4E8m_BE-dYUk =100%x)
### 2. 常用弹窗
常用弹窗包括：普通提示弹窗、普通确认弹窗、带辅助操作弹窗、带简单操作弹窗。
#### 2.1 标题区
- 主标题样式：font-weight：500； font-size：20px；color：#333333；
- 副标题样式：font-weight：400； font-size：14px；color：#999999；换行时，行高为18px。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1kcIFmJW5b1WHXT5VxzRSEOMyLr0i81Yg =100%x)
#### 2.2 操作区
- 主操作区位于操作层右侧，承载按钮最多不超过3个，按钮右对齐，主按钮在最右侧；
- 辅操作区位于操作层左侧，辅操作区信息、控件左对齐；
- 主操作区与辅操作区间最小间距为32px。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1EvVQrraOv8b3cMhPUV6kBbxy42l9gecz =100%x)
#### 2.3 内容区
:::: row
::: col :span="6"
- 基础弹窗内容左对齐，左右边距24px，上下默认边距为0；
- 弹窗内容区最小高度为32px；
- 提示型弹窗内容区默认文案样式为：font-size: 14px； color: #333333;（若文本需突出主次关系，可按照业务需求选择颜色）; 文案换行行高为20px。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Q-7EC5KuzoBAlLIh80-OolUOdQS3qqfe =100%x)
:::
::::
#### 2.4 弹窗滚动条
:::: row
::: col :span="6"
- 当需要展示的内容超过模态弹窗的最大高度时，需在内容区增加滑动条，当鼠标移到弹窗内容区域时，滚动条即出现；
- 滚动条色值为50% #333333；
- 当内容需进行滚动时，底部操作区背景出现投影，投影样式：box-shadow: 0 -4px 4px 0 #000000 0.04。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1WruupgCL5kk3pkck2Cxk84RJo0CTikVK =100%x)
:::
::::
### 3. 带插图的弹窗
#### 3.1 带插图的弹窗的基础结构 & 样式
- 插图弹窗结构：插图+标题区+内容区+操作区；
- 标题文案样式：font-size：20px；font-color：#333333；font-weight：500；
- 内容文案默认样式：font-size：14px；font-weight：400；文本颜色视场景而定；
- 弹窗内元素默认水平居中，当内容为长文本段落时，段落内部左对齐，段落整体与弹窗水平居中；当内容为短文本段落时，段落内部居中对齐；
- 小插图尺寸为48*48px，大插图宽高根据弹窗宽度确定，插图建议保持5:2横纵比；
- 插图弹窗不建议出现滚动条。


![test](https://drive.google.com/thumbnail?sz=w3000&id=1hFQN35PLyScv7wk6CzxrnrsrM3m7LvtB =100%x)
#### 3.2 带插图的弹窗操作区
操作区按钮组合整体水平居中，主按钮在最右侧，详细按钮使用方法见按钮规范。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1HlaYso7WLaLZgWlYTVpb2lhCHG6ImdfP =100%x)

### 4. 自定义弹窗
::::row
:::col :span="6"
- 标题区同常用弹窗一致，内容区根据业务场景自定义，案例可参照场景示例；
- 弹窗内容区最小高度为180px；
- 弹窗内容左对齐，左右边距24px，上下默认边距为0。
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1amHR9u2Lf7y1Zr3112uHaGE3Z8zpq29w =100%x)
:::
::::

## 场景示例
带操作类型弹窗中的表单采用垂直布局表单，表单排版遵照Form（表单）规范。表单类型弹窗建议采用自适应高度形式。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1MoTQj1ffm_Quz-3aKAdq9kQvcoXZIBfm =100%x)
带有状态示意的弹窗，建议采用小插图形式。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1PdE9Vmpm4IqTjlujdFtFYzWV1Mg0p93s =100%x)
新手教育、用户引导类型弹窗，可采用大插图形式。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1xvtiozChWX-YGf5hyiMSy5KwRS7jdJfz =100%x)
自定义弹窗使用实例如下，自定义弹窗适合对内容布局有高度自定义需求的场景。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1SDm_QuGEto85YZOKZGQ9dIhNR-FxrOjx =100%x)


