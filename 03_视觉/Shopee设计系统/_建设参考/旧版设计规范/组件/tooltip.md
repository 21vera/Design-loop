---
extend: /zh/components/tooltip
---
## 组件元素
<br>

:::: row
::: col :span="3"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1vw_wSFglBjSq1FJr2imYCoWcTwCuyJSP =70%x)
 :::
::: col :span="1"
<br />

:::
::: col :span="8"
1. **背景框**：黑色80%透明度的背景框。
2. **提示文字**：用于对当前状态的解释说明。
:::
::::

## 类型汇总

|名称|基础样式|使用场景|
|:--|:--|:--|
|**基本样式**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1hnZ0i9oG14KYE6AkmL3kt0HXdGyhIYbh =86x)|- 当目标元素的表意不够明确，或因空间有限内容无法展示完整时使用。|

## 使用用法
### 1. 基本样式
:::: row
::: col :span="5"
**【使用规则】**
- 出现：鼠标悬停在目标元素上默认1s后再出现（如有需要，出现时间可根据业务做调整；
- 关系：始终跟随目标元素，不随页面滚动而与目标元素分离；
- 消失：鼠标离开目标元素时消失；
- 建议：提示文字建议最多不超过3行。

:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1hS4k5Y3DkfLuoE0Ml3USoOx0RbErR7fV =100%x)
:::
::::

### 2. 不同出现方向
:::: row
::: col :span="5"


**【使用规则】**

- 位置：出现位置有12个方向，默认展示在目标元素的上方；
- 建议：根据目标元素与其他界面元素的关系来确定位置，尽量不遮挡其他界面元素。
:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1_pcU1FcyDw3bJLbh3tVUIAubDnrjPhm4 =100%x)

:::
::::

## 视觉样式

### 尺寸

- 默认两端各留8px，最大宽度320px。

![123](https://drive.google.com/thumbnail?sz=w3000&id=1mZYmg_ACIILDBzaO24RyY9TCx0BQmMaj =100%x)

## 类型汇总

|名称|基础样式|元件属性|
|:--|:--|:--|
|**Normal**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1hnZ0i9oG14KYE6AkmL3kt0HXdGyhIYbh =86x)|background: #000000, 0.80<br>font-size: 14px，#FFFFFF <br>line-height: 18px|

## 场景示例

Tooltip的位置默认在对象上方，但是会随着内容的滑动，调整显示方向，如下图示例。


![123](https://drive.google.com/thumbnail?sz=w3000&id=17VnnaHWjBTysP4KwlghT2Nl2FZmFOJ8q =100%x)
