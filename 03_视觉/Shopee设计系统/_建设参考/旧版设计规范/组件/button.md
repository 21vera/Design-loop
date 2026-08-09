---
extend: /zh/components/button
---

## 组件元素
::::row
:::col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1-E-n6xZ9luLoINxL0PhLMxCDxjUFd8Qt =100%x)
:::
:::col :span="1"
<br />
:::
:::col :span="7"
1. **按钮容器**
2. **Icon**
3. **文字**
:::
::::
## 类型汇总
|名称&编号|样式|使用场景|
|:--|:--|:--|
|<div style="width:120px">**主按钮**</div>|![test](https://drive.google.com/thumbnail?sz=w3000&id=1QAiCgcuXch1ySVWXft0KqrzhqQS9UzXk =82x)|- 用于需要强引导时，为了让用户能在操作上（类似表单、弹出框等场景）快速做出判断, 来突出其中一项相对更重要或者更高频的操作；<br />- 通常情况下同一操作区域只允许有一个主按钮；<br /> - 在多种按钮类型中，主按钮的强度最高。|
|**次按钮**|![test](https://drive.google.com/thumbnail?sz=w3000&id=12z2H_vAACy4TknZqY23thiq3h8pP5U7P =176x)|- 中等强调的按钮，常用于在对话中不需要引导操作的场景；<br />- 同一个操作区域次按钮数量不限，但同组操作需要统一操作目标；<br />- 其强度低于实心按钮。|
|**虚线按钮**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1GBb7Iebk6sAQZMJhQVhrkVqVETMcA2cB =176x)|- 当这个按钮需要一定条件下才能触发时，使用虚线按钮，告知用户可以有这样的操作。在特殊状态下，可以隐藏掉不需用户操作的按钮；<br />- 权重性较低，主要用于添加附件等场景。|
|**危险按钮**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1BB_cK9PFdtcx_qwTJZhqEO1gaScmTnKj =75x)|- 用于提示操作后对用户的数据有消极影响；<br />- 在操作后一般会配合弹窗，对用户的行为进行二次确认。|
|**文字按钮**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1xhe6xmYvLKaZ7o4AXus8zrAS5TKygoiz =206x)|- 通常用于不太醒目的操作, 包括那些位于列表，文本或卡片中，相对于普通按钮，它可以更大程度上节省纵向的空间，让列表呈现的内容更多；<br />- 文字按钮的优先级低于实心按钮和带框按钮。|
|**加载按钮**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1DJhJMLslvngzDEAXEpbVQUu6Gey0dWdW =261x)|- 表示该操作正在发生时使用状态按钮，例如加载中，提交中；<br />- 在这种状态下，按钮不可点击，当这个流程结束后，会有明显的反馈。|
|**下拉按钮**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1_Or-n7WEwmWxaRNPtd8jZj-lBvwsdoEY =296x)|- 当某条数据同时存在多个操作时，建议折叠显示使用；<br />- 推荐使用 1 个主操作 1 + n 个次操作，建议3个以上操作时把更多操作放到 Split Button 中组合使用。|
|**文字链接**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1YOlX6W0qCUxxdg2ibDkggXzCPkhnIkmZ =56x)|- 通常存在于列表或文本中，词性多为名词，作用与论文参考注释类似，便于用户随时参考某一词汇的定义说明；<br />- 文字链接的优先级低于文字按钮。<br />- 在一些不需要引起用户关注超级链接的场景下，不适用该文字链组件。（例如商品/订单/类目列表）|

## 使用用法
::::row
:::col :span="6"
### 1. 主按钮
【使用规则】
- 可独立使用，内可嵌套图标，图标可以放在文字前、后，也可以单独存在，尽量不要使用折行文本；
- 在使用后有渐入渐出的动效反馈，鼠标悬停时有相应变化以提供足够暗示。
- 当两个选项之间有明显区别的时候，应当让两个按钮拥有不同的视觉重量，让其中一个成为视觉的重心。处于视觉重心上的按钮会获得更多的注意力。
:::
:::col :span="6"
### 2. 次按钮
【使用规则】
- 次按钮可以独立使用，内可以嵌套图标，图标可以放在文字前、后，也可以单独存在，尽量不要使用折行文本；
- 在使用后有渐入渐出的动效反馈，鼠标悬停时有相应变化以提供足够暗示。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=16lo2FD-rulBvM3mZGeHOA9teKSMgbv2Y =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1jjrDBvjU405z86_Jw25uA9hLF7WzMbJy =100%x)
:::
::::
::::row
:::col :span="6"
### 3. 虚线按钮
【使用规则】
- 在使用后有渐入渐出的动效反馈，鼠标悬停时有相应变化以提供足够暗示。
:::
:::col :span="6"
### 4. 危险按钮
【使用规则】
- 危险按钮一般不独立使用，在一些非常特殊的场景下 ，需要告警时使用该按钮；
- 在使用后会有明显的二次确认提示。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1uK0WZmNHlXxpZX1GkEjkfA9ziWm_WOOC =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1p4dx_0O8MpOaEurU-detpNre0t9XepVe =100%x)
:::
::::
::::row
:::col :span="6"
### 5. 文字按钮
【使用规则】
- 文字按钮可以独立使用，内可以嵌套图标，图标可以放在文字前、后，也可以单独存在，尽量不要使用折行文本；
- 当页面上按钮过多时，可以考虑文字按钮去降低优先级较低的操作，从而让页面更加简洁。
:::
:::col :span="6"
### 6. 加载按钮
【使用规则】
- 在同一个操作区域最多出现一次。
- 加载按钮一般会配合动态的图标一起使用，来打破用户在等待过程中的焦虑。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1DmTDS8IA-mox11d6G3aFaWOrp3bWWR7o =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=18UXYfO9Un8-q-k1OqO2Oqrah0SZuVx8f =100%x)
:::
::::
::::row
:::col :span="6"
### 7. 下拉按钮
【使用规则】
- 在同一个操作区域最多出现一次；
- 用户可以使用该控件选择绑定到主按钮的默认值，或者从绑定到辅助按钮的下拉列表中显示的互斥值列表中进行选择。在特殊情况下，使用复合型按钮可以采用常规操作按钮+复合型按钮的组合；
- 在分割按钮中, 下拉框既可以改变主按钮的行为(如本例所示), 又或是立刻触发相应的动作。
:::
:::col :span="6"
### 8. 文字链接
【使用规则】
- 通常会用一些特殊的方式来显示超链接。如不同的文字色彩、大小或样式来区别于其它文案信息；
- 指针移动到超链接上时，鼠标样式变为手形，当这个链接已经被缓存过时，则转为 {Opacity: 0.50}；
- 在一些不需要引起用户关注超级链接的场景下，不适用该文字链组件（例如商品/订单/类目列表）。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1oa7mrV_y-hkw93-jfKK6fODTPxsLE37h =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1V-ERxGVeeeQuNh88ogd4Ce7ioCS6Yui1 =100%x)
:::
::::
## 视觉样式
- 按钮的 Text 字重均为 500 / Medium；
- 按钮圆角统一为 4px。

::::row
:::col :span="6"
![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1uq4wWKdrppaaR6UDFgcKjmenxLm6dGwe =100%x)
:::
:::col :span="6"
![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1Et7He_9vujf-PWRVpEBUQGr_yPLg-vre =100%x)
:::
::::
::::row
:::col :span="6"
![4_3](https://drive.google.com/thumbnail?sz=w3000&id=1rN4709gZvZwRH_SKysPDOzaRCTJrnS6V =100%x)
:::
:::col :span="6"
![4_4](https://drive.google.com/thumbnail?sz=w3000&id=1pDVBTh_s68ghK2PXOk1qKa3JuTOdFi5s =100%x)
:::
::::
::::row
:::col :span="6"
![4_5](https://drive.google.com/thumbnail?sz=w3000&id=15TRea24aMF5gLrftumUxOqxRIgcIv8qe =100%x)
:::
:::col :span="6"
![4_6](https://drive.google.com/thumbnail?sz=w3000&id=13ogcmP77kCIC2uEBOhJADqNy4ctetAI2 =100%x)
:::
::::

## 基本状态
|状态名词|样式||||样式描述|
|:--|:--|:--|:--|:--|:--|
|<div style="width:120px">**Normal**</div>|![test](https://drive.google.com/thumbnail?sz=w3000&id=1RnkEk9yolU-xS9DbWs5il-Q9WAwFbihO =95x)<br /> 填充色 #EE4D2D|![test](https://drive.google.com/thumbnail?sz=w3000&id=1555q4eFm7ygC7ltwWqGEqvacc0zFzXuH =95x)<br /> 边框色 #EE4D2D|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Fsr8_kOs8nq_6uk60ykUhKdexnYJsDNi =95x)<br /> 边框色 #E5E5E5|![test](https://drive.google.com/thumbnail?sz=w3000&id=1rmTVAVmcLu3L6aoMffdMSkldGIt3tUiS =73x)<br /> 填充色 #EE4D2D|- |
|**Hover**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1ZQg_fywJjqa6wVZycr-59XHoTTXaw_4Z =95x)<br /> 叠加 #000000 4%|![test](https://drive.google.com/thumbnail?sz=w3000&id=1AWAS2eT7Xn5nyoTHhWaomfiD12Etsrt_ =95x)<br /> 叠加 #EE4D2D 4%|![test](https://drive.google.com/thumbnail?sz=w3000&id=1362jk7_eSJR--LrGbuzKt1lCmkUFULZg =95x)<br /> 叠加 #000000 4%|![test](https://drive.google.com/thumbnail?sz=w3000&id=1OXLcSir8zs1jpmlaDiVJ55_i2Jzx1ZNc =73x)<br /> 叠加 #000000 4%|颜色层叠加: #背景色 4% |
|**Press**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1yPjaKcTw_sPSPjBBvg4DpYDX8ipZ9u0z =100x)<br /> 叠加 #000000 8%|![test](https://drive.google.com/thumbnail?sz=w3000&id=1xbcsb7yrUeLsZK8isQcJUNYB3U8z0h6T =95x)<br /> 叠加 #EE4D2D 8%|![test](https://drive.google.com/thumbnail?sz=w3000&id=1o2zWsWdycfVXGcc3KjnPS8Usd0rRKj2p =95x)<br /> 叠加 #000000 8%|![test](https://drive.google.com/thumbnail?sz=w3000&id=17sWUyHFTtbtRxvIidqu7anZ6AOAuAk5V =73x)<br /> 叠加 #000000 8%|颜色层叠加: #背景色 8%|
|**Disable**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1E8ncDKleFVZZufyhvTUs85l424WUyZZx =95x)<br /> ![test](https://drive.google.com/thumbnail?sz=w3000&id=1HXdlY1KKVxSf1vkztPcCsq3vMDZ6r3sk =120x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1iczMKhOOB6xrJ4wCwY7eqcS_8NqWijCZ =95x)<br /> <br /> ![test](https://drive.google.com/thumbnail?sz=w3000&id=1eCNzz8I13DYVwLe5rHD8iH4Z_2C9zXFa =120x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1HkWNsHQ5vEFGeB0344Li0RMipBzga6TM =95x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1EhjVrrGuXDxgUOWwLZ5clm8EIxk4ndrP =73x)|- 按钮整体 {Opacity: 50%}；<br />- 且光标为 Disabled 指针。|
|**Focus**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1KiGhx2gwXUfvMc58ZVaDoGlFbIOeOz9O =106x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1ri0_nNSsBFTeTf_xSy-0AphwAYTuWWNJ =106x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1R_tPfuePM-tCwW7_qrZ0vwqioBn04Sf7 =106x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1FQjW7E3cnhTNbzRWc8bV1T5U5LXFDu8j =80x)|- 第一层阴影：box-shadow: 0 0 0 2px #FFFFFF; <br />- 第二层阴影：box-shadow:0 0 0 4px <br />rgba(238,77,45,0.30);|
![test](https://drive.google.com/thumbnail?sz=w3000&id=1sz1XcqW55rr77A2BQuhHyF0AU_6pbf20 =100%x)
## 场景示例
按钮的位置按照期望用户的浏览方式进行判断，按钮的位置即是用户最终视线的停留位置，通过选用合适的按钮位置，让用户的视线流尽量流畅不用折返。
::::row
:::col :span="6"
### 1. 左对齐
在引导用户视线从上往下浏览的场景中（主要为表单页），推荐按钮至于整体布局的左侧，并且表示「确认按钮」在左侧，「取消按钮」在右侧。
:::
:::col :span="6"
### 2. 右对齐
在引导用户视线从左上到右下的场景中（主要为模态弹窗），我们认为左上是我们阅读的开始位置右下是落脚位置，所以右边位置放确认来说更加合理，此时「确认按钮」在右侧，「取消按钮」在左侧。

注：当在大多数场景中，弹窗的按钮居右展示，主按钮在右边，如果需要达到一个特定的目标如避免用户退出应用，我们作为设计师可以使用反向设计来达到我们的商业目的。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Vbf5n2Yu2p9cCAMHP3JtR5olUwc0D3Cu =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1ztpwd-3J2UMU3LzrmVcM_axImr5oJPHg =100%x)
:::
::::
::::row
:::col :span="6"
### 3. 居中对齐
当需要用户的视线集中聚焦在中间的场景，常用于含有插图场景中，按钮居中展示。
:::
:::col :span="6"
### 4. 右上角对齐
当需要引导用户不需要阅读全部内容便可以做出决策，或页面过长时，可以将按钮在右上角展示，此时「确认按钮」在右侧，「取消按钮」在左侧。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=123ashozhgSpkL-peqPTCep_UE3m04zf_ =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1BP7OxIgJn-CCj2g9MBac2CKsiWsSjkks =100%x)
:::
::::
![test](https://drive.google.com/thumbnail?sz=w3000&id=1t-ghqSATWMYa2_pP7npGyE9js0Exh484 =100%x)
