---
extend: /zh/components/radio
---

## 组件元素 
<br />

:::: row
::: col :span="4"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1zRFecuKAfGvGAZqtEfokSnYoswxTbXrR =100%x)
:::
::: col :span="8"
1. **单选框**：可进行单选操作。
2. **单选文字**：操作说明文案。
3. **教育提示**（可选）：操作型图标，hover出现对单选文字的解释说明。
:::
::::

## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| <div style="width:120px">**基本单选**</div> | ![2_1](https://drive.google.com/thumbnail?sz=w3000&id=1YOfPUJ1GbKWsQr0xB0g-cnRg6sik5-N7 =450x) | - 用于在数个备选值中选中一个值的场景。 |
| **单选带教育提示** | ![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1EN1wF-4Mn0VmPDy7KyNcYP1rn4Wrt89m =450x) | - 用于通过Hover触发显示对该选值的解释说明的场景。 |
| **单选带说明文案** | ![2_3](https://drive.google.com/thumbnail?sz=w3000&id=1sftZ1kdOXQ1qPhDg1CTulp-_T3G40xLp =450x) | - 用于对该选值进行解释说明的场景。 |
| **单选带二级操作** | ![2_4](https://drive.google.com/thumbnail?sz=w3000&id=1yM4iAPkJKw4VkyqPQk0FyHOAm5ZPh63G =450x) | - 适用于Radio选择后有二级扩展内容的场景。 |

## 使用用法 
1. 通用场景：用于多个选值中选中一个状态，并对所有默认选值可见，方便用户选中比较，建议选值不超过7个；
2. 交互规则：空心单击选中；只有点击其他备选项，当前选项选中变成取消选中；
3. 排序：默认按照选值的首字母a-z的顺序从左至右、由上往下依次排序；也可根据使用频率、业务重要级进行排序。

### 1. 基本单选 
::::row
:::col :span="4"
【使用规则】最基本的使用方法，默认按字母排序，根据页面布局可横排，亦可竖排。
:::
:::col :span="8"
![3_1](https://drive.google.com/thumbnail?sz=w3000&id=1WGJwiTT0ydnjRfdMN1t-s1qFRUy-6ZwM =100%x)
:::
::::


### 2. 单选带教育提示
::::row
:::col :span="4"
【使用规则】Hover单选后置图标出现解释说明。
:::
:::col :span="8"
![3_2](https://drive.google.com/thumbnail?sz=w3000&id=1sxOhK9n5vwtnFa1HZiRo2sre_dAEDyHZ =100%x)
:::
::::



### 3. 单选带说明文案
#### 3.1 竖排用法
::::row
:::col :span="4"
【使用规则】单选带说明文案竖排时不限制文案最大宽度，可根据具体页面布局取适当宽度。
:::
:::col :span="8"
![3_3](https://drive.google.com/thumbnail?sz=w3000&id=1fI3wCJeqmKWMN2DawI-7bYr8OdCYKmVk =100%x)
:::
::::


#### 3.2 横排用法
::::row
:::col :span="4"
【使用规则】单选带说明文案横排时，为了方便阅读，限制最小宽度为160px，最大宽度为440px。
:::
:::col :span="8"
![3_4](https://drive.google.com/thumbnail?sz=w3000&id=1cmwXzxSDgf_UuefktoTYGmvmxyt-uPbr =100%x)
:::
::::


### 4. 单选带二级操作
#### 4.1 一般二级操作
::::row
:::col :span="4"
【使用规则】当选中一个选值时，才出现二级操作，可以是输入框，亦是下拉菜单等，根据业务场景搭配，竖排不限制最大宽度，横排（最小宽度为160px，最大宽度为440px。
:::
:::col :span="8"
![3_5](https://drive.google.com/thumbnail?sz=w3000&id=1B_0dRhIp5Fyt3b85uaT59pdfIwhp164e =100%x)
:::
::::


#### 4.2 单选二级操作
::::row
:::col :span="4"
【使用规则】当单选二级展开为单选的时候，建议加灰色底加箭头的展开样式。可根据场景横排和竖排。
:::
:::col :span="8"
![3_6](https://drive.google.com/thumbnail?sz=w3000&id=1dnxJj_AlhZKg4bxCBPdsTxZ3xFa3NVIL =100%x)
:::
::::


<br />

## 视觉样式
### 1. 尺寸
- 基本元件打下为16px；
- 横排时最小宽度为160px，最大宽度为440px。
<br />
#### 1.1 基本单选及单选带教育提示
- 基本单选横排竖排时使用以下尺寸。

![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1we6144CKQ6fR9w1e1VfN-k7pCzrsO6Xt =100%x)
#### 1.2 单选带说明文案及二级操作
- 单选带说明文案横排竖排时使用以下尺寸。

![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1JvkDzwucwqurZITK0DUV7q15EW3s6XrX =100%x)
<br />

### 2. 基本样式
开关主要分为正常状态和置灰不可点击状态。不可点击态统一用50%不透明度的方式展现。
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **Normal** | ![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1_HXEg27ob2X_4owji5VgTmrsYC5XqbVr =200x) | - background: #FFFFFF;<br />- border: 1px solid #D8D8D8;<br />- font-color: #333333; |
| **Hover** | ![5_2](https://drive.google.com/thumbnail?sz=w3000&id=1sX-QQkVqqFowLHFiEyENRKz8LbtbQhFS =200x) | - background: #FFFFFF;<br />- border: 1px solid #EE4D2D;<br />- font-color:#333333; |
| **Selected** | ![5_3](https://drive.google.com/thumbnail?sz=w3000&id=1IKgc7F6qWfXtzw3kTD8gdnl7BBr4VC5T =200x) | - background: #EE4D2D;<br />- font-color:#333333; |
| **Disable(unselected)** | ![5_4](https://drive.google.com/thumbnail?sz=w3000&id=1i4KIo5APcoIbJ3rv43ek9UQaH73bAqRq =200x) | - background: #EEEEEE;<br />- border: 1px solid #D8D8D8;<br />- font-color: #333333; |
| **Disable(selected)** | ![5_5](https://drive.google.com/thumbnail?sz=w3000&id=1xkBi6AhOgXsjvZj_fafuwmJAy1wYr5Vn =200x) | - background: #EE4D2D(opacity: 50%);<br />- border-radius: 10px; |
| **Focus** | ![5_6](https://drive.google.com/thumbnail?sz=w3000&id=1UziRgDVC2nlwqWsn2yFSrp3E5XaoEmyN =200x) | - background: #FFFFFF;<br />- border: 1px solid #E5E5E5;<br />- box-shadow: 0 0 0 2px #FFFFFF, 0 0 0 4px rgba(238,77,45,0.30);<br />- border-radius: 10px; |
<br />

## 场景示例
在普通情况下，默认使用横排24px间距的形式排列选项。

![6_1](https://drive.google.com/thumbnail?sz=w3000&id=1Rv1JEvkU4m78uQbgmYArhKlXsg0-hQtO =100%x)
在选项过多需要换行排列的时候，采用固定选项宽度的方式进行横排。

![7_1](https://drive.google.com/thumbnail?sz=w3000&id=1IlkyZgnHgBgW9UzpPwfhv9plhlPRKU8g =100%x)
在单个选项内容过长时，采用竖排形式排列选项。

![8_1](https://drive.google.com/thumbnail?sz=w3000&id=1mVHnXnxKjA604I7zShhUMR37pnjC4LpB =100%x)
在场景空间有限，不足以横向排列选项时，采用竖排形式排列选项。

![9_1](https://drive.google.com/thumbnail?sz=w3000&id=1vsC7xLdChlUvJ-kaSolLxjBltvJevJ4E =100%x)
