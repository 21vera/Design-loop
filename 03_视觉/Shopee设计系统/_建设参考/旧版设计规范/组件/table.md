---
extend: /zh/components/table
---

## 组件元素 
<br />

:::: row
::: col :span="7"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1L3fb-ZfqNG7MHXBmYSF6aG0XXH280hBt =100%x)
:::
::: col :span="5"
<br /><br />

1. **列表容器**：列，表 ，筛选，排序；
2. **数据内容**：图片、字符串、数字、日期、状态、按钮、翻页器。
:::
::::

## 类型汇总 
### 1. 常规表格
【使用场景】
- web 列表中基础的列表样式，用于业务相关的各项数据的平铺展示，操作项置于最后一列；
- 当表内数据过长时，可以限制最大的承载长度时超出用”…”,Hover后Tooltips展示全部的内容；
- 异常流：当部分数据读取不到时，使用“-”代替，当整体数据无法读取到时，保留表头，使用占位图标进行占位。

![2_1](https://drive.google.com/thumbnail?sz=w3000&id=1mBSK8TLc6XsVZRUw10QJl9EtbxjrHtBs =100%x)

### 2. 带斑马纹的表格
【使用场景】
- 当需要快速区分不同行数据时，可使用带斑马纹表格，通过斑马纹可以区分信息组，引导用户横向阅读信息，不注重纵向的数据比较；
- 当表内数据过长时，可以限制最大的承载长度时超出使用”…”,Hover后Tooltips展示全部的内容。

![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1yJglqg54IvI-WfCHmYym7fZYTBvQXvoO =100%x)

### 3. 固定表头表格
【使用场景】
- 当纵向内容过多时，可选择固定表头。当数据量存在动态变化时，可以为表设置一个最大高度；
- 滚动条仅在滑动时出现，表头初始状态不出现阴影，滚动表格后出现。

![2_3](https://drive.google.com/thumbnail?sz=w3000&id=1QcfOT_bbZ5YsZuneeFb5GRwghZ40H97M =100%x)

### 4. 分页加载表格
【使用场景】
- 翻页控件与表格右对齐，置于框内；
- 当翻页器与斑马纹表格搭配使用时，若表格最后一行为白色背景，需在改行底部加上分割线；
- 表格信息一页加载不完全且表单的每行数据同等重要，对数据展示无优先级要求时，采用这个加载方式。

![2_4](https://drive.google.com/thumbnail?sz=w3000&id=1yI4MoYBmgMKBGVtaf4_2v113mosEVMZ6 =100%x)

### 5. 固定列表格
【使用场景】
- 当横向内容过多时，可选择固定列；通常固定具有特征的列，以及重点的操作项目；滚动条仅在左右滑动时出现。

![2_5](https://drive.google.com/thumbnail?sz=w3000&id=19ap2oQG3en6R27QP_9n3lnr2fD5wSXeG =100%x)
### 6. 综合型表格
【使用场景】
- 综合型表格适用于业务数据展示复杂的场景。当表格数据之间既包含并列关系，又包含从属关系时，可以使用这种表格的样式进行数据的分组；
- 基于综合型表格可方便地对业务数据进行组合、分解和重新布局排列。

![2_6](https://drive.google.com/thumbnail?sz=w3000&id=1IFTMDEU3qAae-kBFJdy-qAr5wxYvqpJ3 =100%x)

### 7. 父子表格
【使用场景】
- 适用于由于空间限制，当表格内容较多不能一次性完全展示的场景；
- 用于表现各个Item之间存在从属关系，或者递进关系等，对于主从或者递进关系的表格，建议Item层级 ≤5，且不适宜对每个主 item 进行默认展开的场景，但为了能够说明表格具有这种特殊关系，建议每次展开一条主 item，其他主 item 呈收起状态；
- 当各Item的表现具有树形结构式，采用树形结构的方式进行数据展示，当数据中有 children 字段时会自动展示为树形表格，一般每个父级包含关系不超过三层，表格默认每次只打开一层。

![2_7](https://drive.google.com/thumbnail?sz=w3000&id=1Gd8_Pp7--cN8EQ78oPxUTPQDhF0eJDr2 =100%x)


## 视觉样式
### 1. 表头样式
- 默认宽度为240px，特殊日期选择框320px，最小宽度80px，需要照顾页面整体对齐关系情况，可按照当前页面内容100%确定宽度；
- border-radius: 4px; font-size: 14px。
<br />
### 1.1 表头背景样式
- 常规表头样式：background: #F6F6F6；
- 综合型表头样式：background: #F6F6F6；border: 1px solid #E5E5E5；border-radius: 4px;
- 表头文字样式：font-weight:400；font-size:14px；color: #666666；换行时，行高为18px；
- 表头单行高度默认为40px，列标题换行时，表头高度根据内容增高，上下各留12px;
- 列标题换行时，列标题顶对齐。

![3_1](https://drive.google.com/thumbnail?sz=w3000&id=1GYLdLL1faXKAs1_R39LcT6DnTMCPxP3C =100%x)
#### 1.2 列标题样式
- 当列标题长度超过列宽时，则采用“…”进行省略，鼠标悬停“…”时，使用Tooltip展示完整列标题；
- 当进行“…”会影响列标题理解时，可采用换行形式进行展示，但换行行数建议最多不超过两行，当超过两行时，则采用“…”进行省略；
- 排序、说明、下拉的操作热区均为以图标为中心的16*16px的区域；
- 排序操作：单击排序，进行升序排列，二次单击，进行降序排列，三次单击，取消排序。

![3_2](https://drive.google.com/thumbnail?sz=w3000&id=1oL2B4_24-7uArXiPZAy7PptP8V_DqmUg =100%x)
<br />

### 2. 行样式
#### 2.1 基础行样式
- 表格单元格文本样式默认为：font-weight:400；font-size: 14px；color: #333333；
- 若单元格内部信息层级较多，可根据场景增加文本样式，常见有：
font-weight:500；font-size: 14px；color: #666666及font-weight:400；font-size: 12px；color: #999999；
- 行背景色：#FFFFFF，分割线：1px solid #EEEEEE；
- 行左右padding为16px，列间距为16px；
- 一般情况下，在同一表格中建议将每行内容高度保持一致，但在Product此类复杂表格中，不作要求。

![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1L95R-DPuz0yW0jYGu6bLHF8-3WxxuRNu =100%x)
#### 2.2 扩展行样式

![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1y_aZ2-Nrvp2OnwhqWOVsbOcMBV8bClkV =100%x)
### 2.3 行状态

![4_3](https://drive.google.com/thumbnail?sz=w3000&id=1FyUF33izaMYG8QkqOnl0ZF1C2pZIGAMB =100%x)
<br />

### 3. 行、列信息对齐方式
#### 3.1 行对齐
![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1uGt7rM14kxfE2l4J075jAZMeSuQe67yC =100%x)
#### 3.2 列对齐
- 默认情况下，列信息左对齐；
- 数字列的对齐，默认为左对齐，但在需要突出纵向列信息对比的场景下，数据可作右对齐处理；
- 列标题对齐与列信息对齐方式一致。

![5_2](https://drive.google.com/thumbnail?sz=w3000&id=1aZo921cozW-xy0oAIIHwHSBt0-TXccGo =100%x)
<br />

### 4. 分页加载样式
![6_1](https://drive.google.com/thumbnail?sz=w3000&id=1tf5pqHv4zamtOI3Jr2C59TxRIvuknf-G =100%x)
<br />

### 5. 固定表头样式
![7_1](https://drive.google.com/thumbnail?sz=w3000&id=1rMRRjhYeuyJ69FWxk44nQz3cSdP2XfJE =100%x)
<br />

### 6. 固定列表格样式
![8_1](https://drive.google.com/thumbnail?sz=w3000&id=11AjIWTcu1W3asj4ZqclLF4pp4KINDVFp =100%x)
<br />

### 7. 表格中的按钮形式
-在表格中需要使用按钮的场景，默认情况下使用文字按钮；
-建议当操作项超过3个时，则用“More”进行折叠，鼠标hover于“More”上时，展开下拉菜单展示其他操作，特殊情况按钮最大数量可根据业务灵活调整；
-默认情况下，操作项垂直排布，仅当表格内容为单行时，可考虑水平排布；
-当表格出现横向滚动时，操作列为固定列。

![9_1](https://drive.google.com/thumbnail?sz=w3000&id=1szG35cuuoaJO3PDcGl5saQas7UzzjztT =100%x)
<br />

### 8. 表格空白态
-表格信息为空时，表格内容区域默认高度为200px。

![10_1](https://drive.google.com/thumbnail?sz=w3000&id=16XKBE4G8M0ARJyFaf02g97dz9XKtnY1n =100%x)
<br />

### 9. 复杂表格-父子级表格
-子级表格背景色值：#FAFAFA，一般情况下，不建议父子级表格和斑马纹同时使用；
-子级首列缩进16px。

![11_1](https://drive.google.com/thumbnail?sz=w3000&id=13Jy_okectSBmWi6EV2Epj1fVcXE59hQw =100%x)
<br/>
    