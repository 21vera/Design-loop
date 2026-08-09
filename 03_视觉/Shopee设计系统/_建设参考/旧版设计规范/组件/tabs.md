---
extend: /zh/components/tabs
---

## 组件元素
<br />

:::: row
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Yx-vVa1V3zjSEXTD86Vp5mQMEGGKJ2Wb =100%x)
:::
::: col :span="6"
<br /><br />

1. **页签选项**
2. **标记线**：表明当前被选中的内容。
3. **承载线**：承载选项内容。
:::
::::

## 类型汇总 
| 名称 | 组件类型 | 使用场景 |
| :--  | :-- | :-- |
| **基础页签切换** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1VrIBGRejX8x-26YACFg5fPO0yFadEFzR =236x) | - 适用于页签选项具备一定关联但属于不同类别的内容或数据集合的场景。 |
| **带数字的页签切换** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=12fOvpvRbDNEqBKddWRzD3by6zihSlc0a =318x) | - 适用于页签选项内容的数据内容需要被强调的场景。 |
| **带ICON的页签切换** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1a3NyunMWSK5hN_9W_SE7ELZkDKV_KG_4 =296x) | - 适用于页签选项需要意符强化内容间的区别的场景。 |
| **带教育提示的页签切换** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1x328gaK94ENeFEGarWzq3kMHl9hBfA5V =296x) | - 适用于页签选项为专业词汇/新词汇等需要被教育的词汇的场景。 |
| **卡片页签切换** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1wsHB4jTy4VgUKyI1r1HoFdTO11dSHrXA =244x) | - 与基础页签一致，不同的视觉样式 。|
| **模块页签切换** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1MfjxIgcB5c69zF-iRMscM8Joz5ZOx1vf =278x) | - 适用于页签选项内容之间无强关联关系的场景。 |


## 使用用法 

### 1. 基础页签切换
:::: row
::: col :span="5"
- 默认选中第一个页签选项；
- 通过点击进行页签切换。

<font color=#999>备注：其他类型Tab交互一致。</font>

:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1M5N5WXukF8FGccBGytLsCwkn-LpTYH9a =100%x)
:::
::::

### 2. 带数字的页签切换
:::: row 
::: col :span="5"
- 数字表达该页签选项数据的总和；
- 每个页签必须展示数字，包括数据为0的情况；
- 数字展示遵循【数字格式规范】中KMB缩略方式；
- 如有待办事项数字，则采用警示图标，不展示数字。
:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1X6b4cGTtxGcMqekh5DKY1-WpcaFOZ0eG =100%x)
:::
::::


### 3. 带教育提示的页签切换
:::: row 
::: col :span="5"
- Hover在页签选项，展开tooltip；失焦收起。
:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1aXStt3fkiha1l28LKB6oxmicDgzqNUxv =100%x)
:::
::::


## 视觉样式

### 1. 基础样式
- 文字均为14px；
- **Active**: 14px，中粗#EE4D2D；**Normal**：常规#333333；**Hover**：常规#EE4D2D；**Disabled**：常规#333333；opacity: 0.5。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1MSny6UZGvXl48kajT4w0fIRTXhm1RR7O =100%x)

### 2. 尺寸
:::: row 
::: col :span="6"
#### Normal
- 规则：使用于组件上方无标题情况；
- 整体高度：56px，默认尺寸；
- 折行：文案尽可能简洁，超出则折行，最多显示2行。
:::
::: col :span="6"
#### Small
- 整体高度：32px，最小尺寸。
:::
::::
:::: row 
::: col :span="6"

![test](https://drive.google.com/thumbnail?sz=w3000&id=1YHCrXXBMgJTGo1vPojhJlZeQNV19DlbN =100%x)
:::
::: col :span="6"

![test](https://drive.google.com/thumbnail?sz=w3000&id=1xb8XRYsTDJ3DfMdU1mweTViYOtTpCKIE =100%x)
:::
::::

### 3. 其他标注

![test](https://drive.google.com/thumbnail?sz=w3000&id=1jGv4PM-6s1E3H_SQ6miYnAzfWQPp-Em_ =100%x)


## 扩展样式

### 1. 可滑动的基础页签切换
:::: row 
::: col :span="6"
-  默认选中第一个页签选项；
-  若最后一屏页签选项不足一屏，则向前补足一屏。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Rr6mpkGers80epLwQyOj344YWzmHgO_3 =100%x)
:::
::::

### 2. 可滑动的卡片页签切换
:::: row 
::: col :span="6"
-  与「可滑动的基础页签切换」一致。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1chPjkEqDQNPsIFDNyB-rPcZREBZcmvxF =100%x)
:::
::::


## 场景示例

![test](https://drive.google.com/thumbnail?sz=w3000&id=1lsDwDdLnrtalentLMxVsW_yqmoDaSNUU =100%x)
    