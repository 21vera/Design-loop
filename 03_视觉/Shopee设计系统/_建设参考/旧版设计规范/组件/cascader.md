---
extend: /zh/components/cascader
---
## 组件元素
<br />

::::row 
::: col :span="5" 
![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1VYKcXq9Aku1KOR0JOd58Gp-vXFccobt_ =100%x)
:::
::: col :span="1" 
<br />
:::
::: col :span="6" 
1. **触发框** 触发选项面板展开，展示所选数据层级内容。
2. **级联选项面板** 展示供选择的数据层级内容，默认左侧为父级菜单。
:::
::::

## 类型汇总

| 名称 | 类型 | 使用场景 |
| :--  | :-- | :-- |
|<div style="width:130px">**通用型级联选择器&自由型级联选择器**</div>|![2-1](https://drive.google.com/thumbnail?sz=w3000&id=1sIP2IawMFz6XLQXvnS8qRO5jhdVjwvaz =262x)| - 通用型级联选择器：适用于通用场景；<br />- 自由型级联选择器：用于对选择级联不做限制的多级联数据筛选场景。|
|**组合型级联选择器**|![2-2](https://drive.google.com/thumbnail?sz=w3000&id=1LnsVkbCdIenak6RbbiUpoJBikwKIwBtV =328x)|- 在级联选择与输入框组合的场景下使用。|
|**弹窗式级联选择器**|![2-3](https://drive.google.com/thumbnail?sz=w3000&id=1JK452WCtHPlv8BIb7n962sq9jQtu938j =400x)| - 用于级联数较多的数据筛选场景；<br />- 建议级联数≥5层时使用。|

## 使用用法
- 默认状态：在选择器组合场景中，需统一默认状态（默认均为空态，或者默认均有值）；
- 缩略规则：级联选项面板中的文案不允许省略，超过面板的最大宽度折行展示；触发框中的选择结果展示文案根据业务需求选择前省略和后省略；
- 排序：级联选项面板的选项，默认按照字母A-Z依次从上往下排序，也可根据使用频率、业务重要级进行排序。

### 1. 通用型级联选择器
【使用规则】
- 交互：点击触发框触发一级选项面板，通过选择父级选项向右展开子级选项面板，需要选择至最后一层子级选项面板，即可完成级联选择操作；
- 数量：建议级联在2-4个时使用；
- 搜索：根据实际需求，可在输入框增加搜索功能，定位与输入字符相关的信息。

![3-1](https://drive.google.com/thumbnail?sz=w3000&id=1reSkjRAqKwBkx2ns1H0Mdxv54UaMAOBR =100%x)

### 2. 自由型级联选择器
【使用规则】
- 交互：点击下拉选框触发一级菜单，通过选择父级信息向右展开子级选项栏，无需选择到最后一层子级信息，即可点击收起按钮或点击组件外的区域，完成级联选择操作；
- 数量：建议级联在2-4个时使用。

![3-2](https://drive.google.com/thumbnail?sz=w3000&id=10XoHe8_d52m6W2W-aUziFHGrQ_a7ibe4 =100%x)


### 3. 组合型级联选择器
【使用规则】
-交互：初始状态为第一层级未选择状态，完成第一层级的选择出现相应的第二层级，以此类推至第n层；最后出现录需要手动录入数据的输入框；
-默认：可根据用户的选择频率给予各层级的默认选项。

![3-3](https://drive.google.com/thumbnail?sz=w3000&id=1aIrr7_INiFyqgEJZX_RaOfjdLToZx6QH =100%x)


### 4. 弹窗式多选选择器
【使用规则】
- 场景： 适用于级联≥5层时使用；

- 交互规则：点击触发框；弹出级联选项面板弹窗，在未选择到最后一级时，确认按钮灰显；选择父级选项，向右展示相应的子级选项；以此类推，选中最后一级选项，确认按钮高亮；点击确认即可完成选项操作；选项结果框中展示选中的内容；


- 展示：触发框对选中内容的展示方式依照如下逻辑：
1. 触发框根据内容长度进行横向宽度拓展，和纵向高度拓展；
2. 对选择结果内容进行前省略的方式；

- 搜索：可根据业务需求在级联选择框中配置相应的搜索控件。

![3-4](https://drive.google.com/thumbnail?sz=w3000&id=1LXl4u0Do0hJ9Inh1OSmL8Vmed9j2Qspr =100%x)


## 视觉样式
### 1. 通用型及自有型级联选择器
<br />

![4-1](https://drive.google.com/thumbnail?sz=w3000&id=1y65svERwXAsdJz8wghcGPTfMlp0LtQZm =100%x)


#### 1.1 触发框尺寸
- **border-radius:** 4px; **font-size:** 14px; 
- 选择结果框热区为整个触发框。
::::row 
::: col :span="4"
![4-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1trIR_e26-wIIqTu1dqseDrqGuLugoNyT =100%x)
:::
::: col :span="4"
![2-2-2](https://drive.google.com/thumbnail?sz=w3000&id=1cSPyvQtlvSindRFd28fICp6r4gbF0ZJX =100%x)
:::
::: col :span="4"
![4-2-3](https://drive.google.com/thumbnail?sz=w3000&id=1IttK-rIlxQouG-xxFDJ6Cgc5j7Hil330 =100%x)
:::
::::

![4-2-4](https://drive.google.com/thumbnail?sz=w3000&id=1lSvo-8Ld_cuN4p7T6BTpZ8pnDiAd0rxA =100%x)

![4-2-5](https://drive.google.com/thumbnail?sz=w3000&id=10TErqGsyVhUyuRqitBqK2pmzfqdABfnB =100%x)


#### 1.2 级联选项面板尺寸
**background:** #FFFFFF;  **box-shadow:** 0 6px 16px 0 #000000 0.12；**border-radius:** 4px; **font-size:** 14px; **color:** #333333;

![4-2-6](https://drive.google.com/thumbnail?sz=w3000&id=1Ry7Z-7RF4Ig9rCeJGSb0zPr1xsZ9a6ZB =100%x)

### 2. 分开的级联选择器尺寸

![4-3-1](https://drive.google.com/thumbnail?sz=w3000&id=1ZY_U_jVgyh0zMeQnm6xIIXohBE0P2uhe =100%x)

### 3. 弹窗式级联选择器尺寸

![4-4-1](https://drive.google.com/thumbnail?sz=w3000&id=1r8xcCfpYmzoIL1K67-WBCL9r28yFlaq8 =100%x)


#### 弹窗尺寸

![4-5-1](https://drive.google.com/thumbnail?sz=w3000&id=1AtGvQb4U6svCPMKIASjJpFNF804x6tzZ =100%x)


## 基本状态
### 1. 选择结果框状态汇总
| 状态名称 | 状态样式 | 描述 |
| :--  | :-- | :-- |
|<div style="width:180px">**Normal**</div>|<div style="width:300px">![5-1-1](https://drive.google.com/thumbnail?sz=w3000&id=1hV-wpvIt7qsoAb2My_AwIuuGe9C5SuaE =327x)</div>|**background:** #FFFFFF;<br /> **border:** 1px solid #E5E5E5;<br /> **font-color:** #B7B7B7（未选择）/ #333333（已选择）；|
|**Hover**|![5-1-2](https://drive.google.com/thumbnail?sz=w3000&id=1IPP9_tCNGotfEtrXiUVs-L4IDCLD93el =448x)|**background:** #FFFFFF;<br /> **border:** 1px solid #B7B7B7;<br /> **font-color:** #333333（已选）/ #B7B7B7（未选）;<br /> 清空图标默认#b7b7b7; 清空图标hover:遮罩 {#000000, 0.40};|
|**Trigger**|![5-1-3](https://drive.google.com/thumbnail?sz=w3000&id=1PTKdJ6PG7PO7GOsAbyAwQxMqQnNt_0QQ =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #DBDBDB;<br />**font-color：** #333333（已选）/ #B7B7B7（未选）；|
|**Disabled**|![5-1-4](https://drive.google.com/thumbnail?sz=w3000&id=1nd5CgXIK2W374bcVondKLMwzlZpzQf4R =240x)|**background:** #F6F6F6;<br />**border:** 1px solid #E5E5E5;<br />**font-color:** #b7b7b7；|
|**Loading**|![5-1-5](https://drive.google.com/thumbnail?sz=w3000&id=1VwNEUpFAToI86FaFq04xV6IzbgDl6XMK =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #E5E5E5;<br />**font-color:** #333333（已选）/ #B7B7B7（未选）；|
|**Verify**|![5-1-6](https://drive.google.com/thumbnail?sz=w3000&id=1gFv48Mqe4XFvzSiM1Sgq18xihh7MMJXb =240x)| **background:** #FFFFFF;<br />**border:** 1px solid #FF4742;<br />**font-color:** #B7B7B7（未选）；|

### 2. 级联选择框状态汇总
| 状态名称 | Normal | Hover | Selected | Disable
| :--  | :-- | :-- | :-- | :-- |
| **状态样式** | ![5-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1CYTMvTNifyLqHKT_xY058wHD_DQ0rePC =138x)|![5-2-2](https://drive.google.com/thumbnail?sz=w3000&id=1hg6QCzHI63FIkNjAeApuu4BHki7bLmVU =138x) | ![5-2-3](https://drive.google.com/thumbnail?sz=w3000&id=1otlTk8K8oWoJWgwlfm1Q1Gh-5rOfsO72 =138x) | ![5-2-4](https://drive.google.com/thumbnail?sz=w3000&id=1EjwNgQvsr3yszGAdd7mBm9l0zq7Om0sI =138x) |
|**描述**| **background:** #FFFFFF;<br />**font-weight:** 400；<br />**color:** #333333; | 遮罩 {#000000, 0.04}; | **background:** #FFFFFF;<br />**font-weight:** 500；<br />**color:** #EE4D2D; | 基于Normal整体opacity: 0.50;|

## 场景示例
一般情况下，选择框与级联选择框默认左对齐。

![6-1](https://drive.google.com/thumbnail?sz=w3000&id=1dF4_86taHZheMM3yFxR0cY8-g-fGzjXx =100%x)

在右侧没有空间可显示下拉框时，选择框与级联选择框默认右对齐。

![6-2](https://drive.google.com/thumbnail?sz=w3000&id=1AYh2mklHidiXXzXWIILv8OuFGjdn1k-i =100%x)




