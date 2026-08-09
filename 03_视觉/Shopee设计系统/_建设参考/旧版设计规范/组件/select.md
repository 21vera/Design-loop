---
extend: /zh/components/select
---

## 组件元素
<br />

::::row 
::: col :span="4" 
![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1sunzEL41bhVMpyn8OMU6JoMHP3YvcS1i =100%x)
:::
::: col :span="1" 
<br />
:::
::: col :span="7" 
1. **触发框:** hover即触发边框。
2. **结果文字**
3. **清空图标（可选）:** 需要用户进一步执行的相关操作。
4. **后置图标:** 下拉触发后箭头向上，触发前箭头向下。
5. **选定项:** 选中即变品牌色。
6. **未选项:** 未选中为标准文字色。
7. **选项面板:** 白色带投影的背景框。
:::
::::

## 类型汇总
::::row 
::: col :span="6"
### 1. 单选选择器
【使用场景】适用于全部普通场景下的选择情况。
:::
::: col :span="6" 
### 2. 多选选择器
【使用场景】适用于需选择多个预设值的场景。
:::
::::
::::row 
::: col :span="6"
![2-1](https://drive.google.com/thumbnail?sz=w3000&id=1johhefFNluOhFbCJCdUJ9fPfXZilI5JR =100%x)
:::
::: col :span="6"
![2-2](https://drive.google.com/thumbnail?sz=w3000&id=1hngT4r5o8QsHrRqgkHZhRt_VDcxox4op =100%x)
:::
::::
::::row 
::: col :span="6"
### 3. 辅助搜索选择器
【使用场景】适用于某个输入项需要多种辅助属性解释/明确输入信息的内容。
:::
::: col :span="6" 
### 4. 带搜索的选择器
【使用场景】适用于数据筛选场景，在选项很多的情况下使用。
:::
::::
::::row 
::: col :span="6"
![2-3](https://drive.google.com/thumbnail?sz=w3000&id=1NriDPDadcCkvo5tvcoANi9dELK43kpU8 =100%x)
:::
::: col :span="6"
![2-4](https://drive.google.com/thumbnail?sz=w3000&id=1i23nu1mNBTrsE91-FbdNCF66bVZcI4DE =100%x)
:::
::::
::::row 
::: col :span="6"
### 5. 可新增选项的选择器
【使用场景】适用于某个输入项需要多种辅助属性解释/明确输入信息的内容。
:::
::: col :span="6" 
<br />
:::
::::
::::row 
::: col :span="6"
![2-5](https://drive.google.com/thumbnail?sz=w3000&id=1XGlnMwEKIBXLgqDcIpmVGX1NGoSDcPeh =100%x)
:::
::: col :span="6"
<br />
:::
::::


## 使用用法
选择器由选择触发框与选项面板组合而成，可根据场景选择选择不同的组合。
### 1. 单选选择器
【使用规则】
- 排序：选项默认按照字母A-Z依次从上往下排序，也可根据使用频率、业务重要级进行排序；
- 交互：点击触发框，弹出选项面板，点选选项，收起选项面板，触发框反馈已选内容，完成选择操作。

![3-1](https://drive.google.com/thumbnail?sz=w3000&id=1yXOnWt381-F_YRjtEIIsLQRTS4_wZseX =100%x)


### 2. 可清空选项的单选器
【使用规则】
- 交互：hover在触发框，展现清空按钮，点击清空按钮，清除已选项。

![3-2](https://drive.google.com/thumbnail?sz=w3000&id=1H8y1ciEhtRNU9uh9VPR7Lucbv-EPzmnW =100%x)


### 3. 多选选择器
【使用规则】
- 排序：选项默认按照字母A-Z依次从上往下排序，也可根据使用频率、业务重要级进行排序；
- 交互：点击触发框，弹出选项面板，点击选中选项，触发框反馈已选内容，点击选项面板外任意地方或者触发框，收起选项面板，完成选择操作。

![3-3](https://drive.google.com/thumbnail?sz=w3000&id=18aLZkMSQUwTp0YHpJCeWhIlxaotPBWuV =100%x)


### 4. 辅助搜索选择器
【使用规则】
- 给予默认搜索类型选项值；
- 交互：点击搜索框中的选择器弹出选项面板，点选选项，收起选择面板完成选项切换。

![3-4](https://drive.google.com/thumbnail?sz=w3000&id=1bC80lqNV8h9iFdyClOCU7Ce2ViU_5391 =100%x)


### 5. 带搜索的选择器
【使用规则】
- 交互：点击触发框弹出选项面板，在选项面板中搜索框输入字符，实时显示与字符匹配的选项，点选选项，触发框反馈已选选项；删除搜索框中的字符，回到默认选项状态。

![3-5](https://drive.google.com/thumbnail?sz=w3000&id=1xNl7a5b9t7Uk8pZ41wvn7ZFteFjvOXmV =100%x)


### 6. 可新增选项的选择器
【使用规则】
- 交互：点击触发框弹出选项面板，点击选项面板中的「增加选项按钮」，操作栏切换为输入栏；输入相关录入项名称，点击确认完成选项录入，并自动选中；点击选项面板以外的区域或者触发框，选项面板收起。

![3-6](https://drive.google.com/thumbnail?sz=w3000&id=1PlwxykdNIoytL1JNR-QdKozfOeaRWZNn =100%x)



## 视觉样式
### 1. 触发框长度区间
- 在宽度的选择上，建议尽量保证内容能够被完全显示，但当空间有限时，可使用“…”；
- 默认宽度为240px;
- 往下可以按80px递减为160px，120px，单选触发框最小宽度为80px，多选触发框最小宽度为240px;
- 往上可以按80px、120px、160px递增为320px，440px，600px;
- 如果以上规则无法满足，可以选择按照当前页面内容100%确定宽度。

![4-1](https://drive.google.com/thumbnail?sz=w3000&id=1kRYYJ1YJV_G-2630MtmuxwlK6P7eV7-l =100%x)


### 2. 基础单选触发框、辅助搜索触发框尺寸
- **border-radius:** 4px; **font-size:** 14px; 
- 输入框热区为整个输入框。辅助搜索选择结果框，建议右侧输入框的宽度不小于左侧选择框宽度的1.5倍。
::::row 
::: col :span="4"
![4-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1QQ4sjWTJC3kfPQVYZ5TD1ZpWjnJRb0DB =100%x)
:::
::: col :span="4"
![4-2-2](https://drive.google.com/thumbnail?sz=w3000&id=1EKATXtCPj3rxVRgWM4Nhn-ePZUoOvIEO =100%x)
:::
::: col :span="4"
![4-2-3](https://drive.google.com/thumbnail?sz=w3000&id=14dMBrLM-aBIOez21rzKziI1SLz-U4JJn =100%x)
::::

### 3. 基础多选触发框尺寸
- 标签 **font-size:** 14px; **font-color:** #333333; **background:** #FAFAFA; **border:** 1px **solid:** #E5E5E5; **border-radius:** 2px; **hover-background:** 叠加4% #000000；
- 默认情况下，当标签长度超过192px时，对标签内容进行“…”缩略，如实际场景有需要，可由业务前端修改标签最大宽度;

![4-3-1](https://drive.google.com/thumbnail?sz=w3000&id=1CgNRo3jMYfqwv758zmWy7bUEu1AY6MSs =100%x)

- 单行多选触发框分默认尺寸（32px）、大尺寸（40px）两种。
- 默认情况下为单行，可通过增加触发框宽度露出选项标签，超过该宽度则显示“…”；当可选数量上限较大且对选择结果有较强露出需求时，在不影响布局的前提下，可拓展触发框的高度，但最多不超过5行（高度：144px），超过5行则显示“…”；
- 根据选项数量拓展触发框高度，会影响页面布局的稳定性，请谨慎使用。

![4-3-2](https://drive.google.com/thumbnail?sz=w3000&id=1Qyk73bKCj53hEYzafwoVozEQxR5jlZtU =100%x)


### 4. 选项面板样式
- 样式：**background:** #FFFFFF; **box-shadow:** 0 6px 16px 0 #000000 12%；**border-radius:** 4px; **font-size:** 14px, #333333;
- 宽度：选项面板默认与选择结果框等宽，若选项内容较长，可根据选项长度合理增加选项面板宽度，最大宽度为440px，若选项长度超过最大宽度，则对该项进行换行（440px是240px默认宽度输入框搭配的最大宽度，如实际场景有需要，可由业务前端修改最大宽度）；
- 高度：基础选项面板最大高度为218px（即显示6.5个非折行选项的高度和), 超过该高度出现滚动条，带搜索的选项面板、带新增功能的选项面板，最大高度为在6.5个选项的高度基础上增加搜索框或新增选项栏的高度。
- 滚动条的展示：当选项超过6个时，鼠标hover选项面板区域，滚动条出现，鼠标离开选项面板区域，滚动条消失。

#### 4.1 单选选项面板

![4-4-1](https://drive.google.com/thumbnail?sz=w3000&id=1NCg73rGm1XTx5275XeyuXnUNjky2j4J- =100%x)

#### 4.2 多选选项面板

![4-4-2](https://drive.google.com/thumbnail?sz=w3000&id=1Y78202UTzjzzWzND_3Ytd_8gIKfQ3jOy =100%x)

#### 4.3 带搜索的选项面板

![4-4-3](https://drive.google.com/thumbnail?sz=w3000&id=1X8kSZli_y0TgztKE_Dx1D9y3bpQbbL0c =100%x)

#### 4.4 带新增选项的选项面板

![4-4-4](https://drive.google.com/thumbnail?sz=w3000&id=1DKn3rkW8HDyIwiins3wKDAVaolifFM6g =100%x)


### 5. 触发框-基本样式
| 状态名称 | 状态样式 | 描述 |
| :--  | :-- | :-- |
|<div style="width:160px">**Normal**</div>|<div style="width:300px">![5-1](https://drive.google.com/thumbnail?sz=w3000&id=12wWxzGnJrAx5fNzYsGY3d1VNU-LOfBU- =240x)</div>|**background:** #FFFFFF;<br />**border:** 1px solid #E5E5E5;**font-color:** #B7B7B7（未选择）/ #333333（已选择）；|
|**Hover**|![5-2](https://drive.google.com/thumbnail?sz=w3000&id=1bWoF4Fv0iXcA0JHioqwfbDnW26pcgxme =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #B7B7B7;**font-color:** #333333（已选）/ #B7B7B7（未选）；<br />清空图标默认#b7b7b7; 清空图标hover:遮罩 {#000000, 0.4}；|
|**Trigger**|![5-3](https://drive.google.com/thumbnail?sz=w3000&id=1tfrmzfpVHLK0MuiA10yfphYEcrCm5z9Y =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #B7B7B7;**font-color:** #333333（已选）/ #B7B7B7（未选）；|
|**Disabled**|![5-4](https://drive.google.com/thumbnail?sz=w3000&id=1wIDDckrPFympf2Bk56EQi_YTPL9Q2-pV =240x)|**background:** #F6F6F6;<br />**border:** 1px solid #E5E5E5;<br />**font-color:** #b7b7b7；|
|**Loading**|![5-5](https://drive.google.com/thumbnail?sz=w3000&id=1HaN6ZHJwzrBi5rrp0huDmO1ibJxmJOEk =240x)| **background:** #FFFFFF;<br />**border:** 1px solid #E5E5E5;<br />**font-color:** #333333（已选）/ #B7B7B7（未选）；|
|**Verify**|![5-6](https://drive.google.com/thumbnail?sz=w3000&id=1ttr36VPnNMJo0oxeDi2t1cqhq7B63_mI =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #FF4742;**font-color:** #B7B7B7（未选）；|

### 6. 选项面板-基本样式
| 状态名称 | Normal | Hover | Selected | Disable |
| :--  | :-- | :-- | :-- | :-- |
|<div style="width:160px">**固定时间状态样式**</div>|![6-1](https://drive.google.com/thumbnail?sz=w3000&id=1D0tO8kKn0stf0m6Gk98tARKD4WwVaRZu  =90%x)|![6-2](https://drive.google.com/thumbnail?sz=w3000&id=1o7BIKkcew963AZ6r4WwM-SGjlevwB2t5 =90%x)|![6-3](https://drive.google.com/thumbnail?sz=w3000&id=1pOEeL7Y_SvHswVy9lYEVfayd-ec-33sF =90%x)|![6-4](https://drive.google.com/thumbnail?sz=w3000&id=1y_u8YH1W-Ok16H-VIXxcH1gucWCVgW4S =90%x)|
|<div style="width:160px">**描述**</div>|**background:** #FFFFFF;<br />**font-weight:** 400；<br />**color:** #333333;| 遮罩 000000，4%；| **background:** #FFFFFF;<br />**font-weight:** 500；<br />**color:** #EE4D2D;|基于Normal整体opacity：40%；|


## 场景示例
在普通情况下，触发框与选项面板等宽。

![7-1](https://drive.google.com/thumbnail?sz=w3000&id=1jG-Wvu0TyTV9-5akTG7rRNhJbbEMoFbu =100%x)


在选项面板中选项内容较长时，触发框与选项面板默认左对齐。

![7-2](https://drive.google.com/thumbnail?sz=w3000&id=1H-nG9XAZGmXxs5fuPLOfVgN58XTIe5U4 =100%x)


在选项面板靠近页面右侧边缘时，触发框与选项面板默认右对齐。

![7-3](https://drive.google.com/thumbnail?sz=w3000&id=1wt5t-gpP81Fmbm8L1V26rDYFIJo3vPUI =100%x)
    