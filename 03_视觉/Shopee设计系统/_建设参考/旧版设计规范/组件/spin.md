---
extend: /zh/components/spin
---
## 组件元素 
<br />

:::: row
::: col :span="3"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Yagr8SpFuMSaZjaRoazYyae7JfAsmMB7 =80%x)
:::
::: col :span="9"
<br />

1. **常用Loading**
2. **辅助文字**
:::
::::

## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| **强加载** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1FGxqjvsRNOCi990bDz7YJpRevYqLhVPB =16x) | - 橙色适用于信息层级最高的场景。 |
| **弱加载** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1kqngGHgUje1s4HRfcLURiC-THgXgiODj =16x) | - 灰色适用于信息层级较弱的场景。 |
| **带辅助文字** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=13CZCLB_OtW-v8F_nwRyrqFuPjXSnDPzK =51x) | - 添加辅助文字适用于能帮助用户理解当前状态时的场景。 |
| **控件内加载** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1FF_fLlKbL_4FVWQoGUJbx2ZzFvzfzevX =107x) | - 白色只会适用于填色按钮中。 |

## 使用用法 
- 触发：动态指示器以顺时针方向转圈，表示正在加载中；
- 消失规则：当数据获取成功时，loading消失。

### 1. 常规loading
:::: row
::: col :span="6"
【使用规则】
- 位置：在获取数据时出现在页面/模块正中央。

【异常流】
- 当多个相邻的子模块需要加载时，建议使用Skeleton骨架屏样式；
- 为子模块/图片加载时，可不使用提示文字；
- 当图片在页面流里，或存在多张相邻的图片时，建议使用Skeleton骨架屏样式。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=198rHww9FmPEZbkMfdMqOHT0PYRQN1YkD =100%x)
:::
::::

### 2. 组件内loading
:::: row 
::: col :span="6"
【使用规则】
- 触发：在提交数据后出现；
- 位置：在获取数据时出现在组件正中央；
- 位置：当组件为button时，loading的动态提示器位于button文字左侧。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1eQQ1ulfNNoUR8D_mQ9LV-U5I3SozeyRr =100%x)
:::
::::


## 视觉样式
### 1. 尺寸
:::: row 
::: col :span="3"
#### 1.1 Normal
- 正常尺寸。
:::
::: col :span="3"
#### 1.2 Normal(带文字)
- 正常尺寸；
- 文案一般上下结构；
- 文案可以自定义，一般不用。
:::
::: col :span="3"
#### 1.3 Small
- 小尺寸。
:::
::: col :span="3"
#### 1.4 Small(组件内)
- 小尺寸一般在组件或按钮内出现；
- 组件内loading动态和文字一般水平结构。
:::
::::
:::: row 
::: col :span="3"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1vhhIST8KbR72MQz6Mv9bRxjg73ntjIN5 =100%x)
:::
::: col :span="3"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1aSDrkK3r_mVKyD8LcuuY054GQIy58aD6 =100%x)
:::
::: col :span="3"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1PsLDCbP6ruOwKTZjQg8KolIobXvHdNT6 =100%x)
:::
::: col :span="3"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1BI06Hj-Nu7n_I9EHu1YoOXpnOsb4dfrf =100%x)
:::
::::

### 2. 基本样式
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **强加载** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1yPt7I_VpZ1nKpaxYbwBqiHyS6h3sIPmK =32x) | **background**：#EE4D2D; |
| **弱加载** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=10Nv3xRKXOKBOks0b8ZQnqAF3e5Q6VZOU =51x) | **background**：#EE4D2D;<br /> **Label_front**：14px；<br />**font-color**：#333333； |
| **带辅助文字** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1qK7kHVrAFkCUiGNUPFnPqp1YVSOEnA3I =16x) | **background**：#999999； |
| **控件内加载** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1S0d2wtTi1_UtGUui7JSiJ_XWexrZE5Bd =107x) | **background**：#FFFFFF；<br /> **Label_front**：14px；<br /> **font-color**：#FFFFFF； |


## 场景示例
![test](https://drive.google.com/thumbnail?sz=w3000&id=1oboPmk34JLXhTvYD-2BQSMAsfaaNC3MX =100%x)

![test](https://drive.google.com/thumbnail?sz=w3000&id=1X79jCQgIC1MslBAhQFOUsgltNYqfEntl =100%x)

![test](https://drive.google.com/thumbnail?sz=w3000&id=1YLwIVQRkH2sdoJTwDjL-4qHsG3OCsfD2 =100%x)
    