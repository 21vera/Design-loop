---
extend: /zh/components/slider
---
## 组件元素
:::: row
::: col :span="8"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1ZJWeI4pX3wRX6zOnlx9ANxI_3HvMPn1a =500x)
:::
::: col :span="4"
<br/>

1. **轴线**
2. **滑块**
3. **数据结果**
:::
::::

## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| <div style="width:200px">**单滑块的滑动条<br/>DE-Slider-1**</div> | ![2_1](https://drive.google.com/thumbnail?sz=w3000&id=1U734pR7wivHcN7KgGemLHGii8cfP5PLh  =416x) | - 用于录入一个数值的场景。 |
| **带数字输入框的滑动条<br/>DE-Slider-2** | ![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1G4qPFCVEyIUbeYxwtcswSyTLUqK6774M  =416x) | - 用于录入数值精度较高时；<br/>- 用于取值范围较大时。 |


## 样式逻辑
- 滑块hover热区为16*16px。

![3_1](https://drive.google.com/thumbnail?sz=w3000&id=1Sy65asnzXIhBPnFG1vsLKj5R02Kyg2Tr =100%x)

### 长度区间
- 滑动条默认宽度为240px;
- 往上可以按80px、120px、160px递增为320px，440px，600px;
- 如果以上规则无法满足，可以选择按照当前页面内容100%确定宽度。

![3_2](https://drive.google.com/thumbnail?sz=w3000&id=1CgvzJGgehol47tP3psuxFbxl4-dQ0NxA =100%x)
<br/>

### 基本样式
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **Normal** | ![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1odAU_LNaqViiEaGXSSPSFCUgKWy4rlGM =500x) | - 轴线已选中部分background: #EE4D2D; <br/>- 轴线未选中部分background: #E5E5E5;<br/>- 滑块border: 2px solid #EE4D2D;<br/>- 步进器border: 1px solid #E5E5E5; |
| **Hover** | ![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1Zkl9o102CLZKx9nd08RIxp9OaAUsrETw =500x)<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/> ![4_3](https://drive.google.com/thumbnail?sz=w3000&id=1D4LYGy4SrpwAKlSQ_4rd0XgjNTgLD2Yv =500x) | - 轴线已选中部分background: #EE4D2D; <br/>- 轴线未选中部分background: #E5E5E5;<br/>- 滑块border: 2px solid #EE4D2D;<br/>- 步进器border: 1px solid #B7B7B7;<br/><br/><br/><br/><br/>- 轴线已选中部分background: #EE4D2D; <br/>- 轴线未选中部分background: #DBDBDB ( 即#333333 叠加4% #000000 ）; <br/>- 滑块border: 2px solid #EE4D2D;<br/>- 步进器border: 1px solid #B7B7B7; |
| **Disabled** | ![4_4](https://drive.google.com/thumbnail?sz=w3000&id=1lfmd6UosCxyW2o2ezq32gb7mZW1cmYx_ =500x) | - 轴线已选中部分background: #F6A696 (即#EE4D2D 叠加50% #FFFFFF ）; <br/>- 轴线未选中部分background: #E5E5E5;<br/>- 滑块border: 2px solid #F6A696 (即#EE4D2D 叠加50% #FFFFFF ）;<br/>- 步进器border: 1px solid #E5E5E5;<br/>- 步进器background: #F6F6F6;  |
<br/>

## 使用用法
### 1.单滑块的滑动条
:::: row
::: col :span="5"
#### 使用用法
【交互规则】：滑动条的取值可以通过以下三种方式改变：
- 鼠标点击滑块后拖拽；
- 鼠标点击轴线上任意一点；
- 通过外部输入框输入具体的数值：

【排序规则】：水平方向的滑动条从左向右数值依次变大。
:::
::: col :span="7"
<br/>

![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1fQ9bVPaGf4532WaTdUuMUTSqbID_76gh =100%x)
:::
::::
<br/>

### 2. 带数字输入框的滑动条
:::: row
::: col :span="5"
#### 使用用法
【交互规则】：滑动条的取值可以通过以下三种方式改变：
- 鼠标点击滑块后拖拽；
- 鼠标点击轴线上任意一点；
- 通过外部输入框输入具体的数值。

【排序规则】：水平方向的滑动条从左向右数值依次变大。
【行为】：
- 输入数值或点击步进器时，滑块即时移动到对应位置。
- 移动滑块时，输入框内的数字即时改变。
- 当输入框录入值超过滑动条极值时，滑块自动处于端点。输入框显示滑动条对应极值。
:::
::: col :span="7"
<br/>

![5_2](https://drive.google.com/thumbnail?sz=w3000&id=10wTybuvxL15LUFeWizCe5kUh2zb2sVXy =100%x)
:::
::::
    