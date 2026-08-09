---
extend: /zh/components/switch
---
## 组件元素
:::: row
::: col :span="6"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1WTwQqGF3pIs7VT8foTCS-rIHW1Y34jCe =250x)
:::
::: col :span="6"
1. **轨道（Track）**: 限定开关滑块可移动的范围。
2. **滑块（Slider）**
:::
::::

## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| **普通开关<br/>DE-Switch** | ![2_1](https://drive.google.com/thumbnail?sz=w3000&id=1JLkj0n_ofDhnYvQv_Rwp4D4hWoJdBsgr =200x) | - 适用于通用场景。 |
| **带有文字的开关<br/>DE-Switch** | ![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1YbDfP7mH49wh1vmuvjWyWQ4vyfgXwaKE =200x) | - 有较深的教育场景，比如说是帮助中心。 |

## 使用用法 
### 1. 基础开关 
【交互规则】触发：鼠标点击拖住滑块可以左右移动；或，鼠标点击轨道的左右两块区域，控制滑块的左右移动。
![3_1](https://drive.google.com/thumbnail?sz=w3000&id=1_uXqSXwt_kfM4qSXaC6Q71ptjzLfoEeq =100%x)
### 2. 带有 tooltips 的开关
【使用规则】针对开关的操作影响的关联属性过多时，可加上tooltips的解释配合使用。
![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1aCu8o389XtqCMCl4lkG3iCNey9bPb68E =100%x)
### 3. 带有文字的开关
【使用规则】教育、高级功能操作的场景。
![5_1](https://drive.google.com/thumbnail?sz=w3000&id=12wP3u-jEd5_XFEK8iu8iBdMB3Ak6-hVG =100%x)
<br/>

## 视觉样式
尺寸大小分为正常尺寸和小尺寸，一般不推荐使用小尺寸开关。

:::: row
::: col :span="4"
#### Normal
- 正常尺寸大小;
- background: #55CC77; circle：#FFFFFF;
:::

::: col :span="4"
#### Small
- 小尺寸大小，只在展示区域承载有限的情况下才可以使用, 不允许按钮内出现文字;
- background: #55CC77; circle：#FFFFFF;
:::

::: col :span="4"
#### 带有tooltip开关
- 停留在开关时tooltip提示;
:::
::::

:::: row
::: col :span="4"
![6_1](https://drive.google.com/thumbnail?sz=w3000&id=1O_us0OhdVStapPc9b-xUpN28cCYvfRCR =100%x)
:::

::: col :span="4"
![6_2](https://drive.google.com/thumbnail?sz=w3000&id=1lQOLwsVOiP5VX9vNyPMqlfeRES7rttzs =100%x)
:::

::: col :span="4"
![6_3](https://drive.google.com/thumbnail?sz=w3000&id=17Qu5GonuxaIfjLFXX7GE0ArnkFYdlr2N =100%x)
:::
::::
<br/>

### 基本样式
开关主要分为正常状态和置灰不可点击状态。不可点击态统一用50%不透明度的方式展现。
| 状态 | 展示样式 | 描述 |
| :--  | :-- | :-- |
| **Normal** | ![7_1](https://drive.google.com/thumbnail?sz=w3000&id=1WGfxSQIOlaXClo4sG66HUndoJexyFW2_ =200x) <br/><br/><br/><br/><br/><br/>![7_2](https://drive.google.com/thumbnail?sz=w3000&id=148cwN_aTJopI_N-M1_pCXKTHDMnseJp8 =200x)| - background: #55CC77; <br/> - circle：#FFFFFF; <br/> - font-color：#FFFFFF; <br/><br/><br/> - background: #B7B7B7; <br/> - circle：#FFFFFF; <br/> - font-color: #FFFFFF； |
| **Disabled** | ![7_3](https://drive.google.com/thumbnail?sz=w3000&id=1g0u4gsnCQSWEZct2TU7c76Z3KT7nas62 =200x) <br/><br/><br/><br/><br/><br/><br/><br/><br/><br/> ![7_4](https://drive.google.com/thumbnail?sz=w3000&id=1A2pa0KZCFKJijjONUhexpGPzU1gc1wBn =200x) | - background: #55CC77; <br/> - circle：#FFFFFF; <br/> - font-color：#FFFFFF; <br/> - opacity：50%; <br/> <br/> <br/> - background: #B7B7B7; <br/> - circle：#FFFFFF； <br/> - font-color: #FFFFFF; <br/> - opacity：50%； |


## 场景示例
一般情况下，开关的操作不会影响对应文案颜色的变化。

![8_1](https://drive.google.com/thumbnail?sz=w3000&id=1LVcWsXVh4jmZLzjujR28nS6zLi3czMRs =100%x)

    