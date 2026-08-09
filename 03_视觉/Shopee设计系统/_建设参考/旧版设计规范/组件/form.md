---
extend: /zh/components/form
---

## 组件元素
<br />

::::row 
::: col :span="5" 
![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1cicx7DP3sUMFobmjF6ygAWFqKaAbWyK7 =100%x)
:::
::: col :span="1" 
<br />
:::
::: col :span="6" 
1. **标题层**
- 概括表单主题；
- 该层可容纳以下内容：标题文案、面包屑导航。
2. **内容层**
- 相关的输入项可以组成表单区域，使表单结构更清晰；
- 该层可容纳以下内容：表单区域、区域标题、标签（输入项名称）、输入域（包括文本输入框、单选框、复选框、开关、选择器、上传等）。
3. **操作层**
- 可进行相关操作（eg：保存、取消、提交、确定等）来结束当前操作流程或提交表单数据；
- 该层可容纳以下内容：主操作按钮、次操作按钮。一个表单尽量只有一个主操作按钮。
:::
::::

## 类型汇总
<br /><br />
| 名称 | 类型 | 使用场景 |
| :--  | :-- | :-- |
|<div style="width:130px">**水平分布表单**</div>|<div style="width:600px">![2-1](https://drive.google.com/thumbnail?sz=w3000&id=1TSmMMwB2WKoBMxuAL4WIqrJ03bmcXwsi =340x)</div>|- 适用于常规页面表单排布。|
|**垂直分布表单**|![2-2](https://drive.google.com/thumbnail?sz=w3000&id=1Qzd2PsIoxX-W5Bm-tStYZw1Jsu3kXUcB =340x)|- 适用于弹窗中的表单排布；<br />- 适用于页面横向空间有限的场景；<br />- 适用于需要左右对齐的场景。|
|**行内分布表单**|![2-3](https://drive.google.com/thumbnail?sz=w3000&id=18co_cuBjvT1jpaZAf_JgLnqvyM47pqM9 =600x)|- 适用于排布筛选条件表单；<br />- 适用于布局空间紧凑的场景。|

## 使用用法
### 1. 必填项和选填项
::::row 
::: col :span="4"
【使用规则】表单内必填项标签统一如右图所示，选填项标签统一为普通样式。
:::
::: col :span="8" 
![3-1](https://drive.google.com/thumbnail?sz=w3000&id=1HMZHKHcZL5tbeGdGhOnUdSY_lfAlh9VU =100%x)
:::
::::
### 2. 操作按钮状态
#### 2.1 主操作按钮不置灰

::::row 
::: col :span="4"

【使用规则】操作按钮全程处于激活可点击状态； 点击按钮，对表单进行全局校验。
:::
::: col :span="8" 
![3-2](https://drive.google.com/thumbnail?sz=w3000&id=1ze_ezUM1uw-Ixjr_R1QcdeobaSpxLJi5 =100%x)
:::
::::

#### 2.2 主操作按钮置灰
:::: row
::: col :span="4"

【使用规则】
- 适用于仅有输入框和按钮，输入内容格式较固定，用户熟悉且知道如何输入的表单；
- 按钮功能置灰，用户无法与该功能进行交互，也无法获得任何反馈，因此适用场景比较少，进行交互设计时应考虑具体业务需求；
- 输入项内容符合业务规则则激活主操作按钮。
:::
::: col :span="8" 
![3-3](https://drive.google.com/thumbnail?sz=w3000&id=1F-bP2uSxHEIJ-QO3lnGeoMCKJMQcTpl1 =100%x)
:::
::::

### 3. 校验方式
#### 3.1 主操作按钮不置灰
:::: row
::: col :span="4"

【使用规则】
- 操作按钮一直处于可点击的激活状态，点击后出现全局校验反馈；
- 进行操作动作后，页面定位到第一个有错误反馈的输入域位置；
- 校验文案显示格式遵循Data Entry组件。
:::
::: col :span="8" 
![3-4](https://drive.google.com/thumbnail?sz=w3000&id=1PSyv9_dppSmLsw2wbF4IhMI8uMw9zeVh =100%x)
:::
::::

#### 3.2 即时校验反馈
:::: row
::: col :span="4"

【使用规则】
- 适用于需要及时修改录入内容的场景；
- 适用于操作按钮置灰的场景； - 当焦点离开输入框时对输入框内容进行校验。
:::
::: col :span="8" 
![3-5](https://drive.google.com/thumbnail?sz=w3000&id=1vvvH9zj1toiIVEpFZCRk_9wGkEedHUwt =100%x)
:::
::::
### 4. 动态增减项表单
:::: row
::: col :span="4"
【使用规则】
- 点击新增按钮，向下增加同类输入项；
- 达到数量上限时，新增按钮消失；
- 点击删除按钮删除当前输入项，标签序号自动补齐；
- 若输入项之间有联动关系则需根据具体业务进行设计；
- 固定不可删除的输入项数量由具体业务决定；
- 可新增的数量上限有具体业务决定。
:::
::: col :span="8" 
![3-6](https://drive.google.com/thumbnail?sz=w3000&id=1jNulg6nzC7x04vhwazBWUD_9tKWmxq51 =100%x)
:::
::::
### 5. 动态增减项表单组合
:::: row
::: col :span="4"
【使用规则】
- 点击新增按钮，向下增加同类输入项；
- 达到数量上限时，新增按钮消失；
- 点击删除按钮删除当前输入项，标签序号自动补齐；
- 若输入项之间有联动关系则需根据具体业务进行设计
- 固定不可删除的输入项数量由具体业务决定；
- 可新增的数量上限有具体业务决定。
:::
::: col :span="8" 
![3-7](https://drive.google.com/thumbnail?sz=w3000&id=1q_JV4bXv09yq232R6FTLPNVqFv5O8JfZ =100%x)
:::
::::


## 视觉样式
- 区域标题（Area Name）：**font-family:** Roboto-Medium; **font-size:** 22px; **font-weight:** 500；**color:** #333333;
- 标签：**font-family:** Roboto-Medium; **font-size:** 14px; **font-weight:** 400； **color:** #333333;

### 1. 水平分布表单
- 表单整体默认在页面中水平居中对齐；
- 标签单行最大宽度为200px，超过该长度建议进行折行；
- 标签最小高度为32px，当标签内容高度小于该高度时，内容在该高度内垂直居中（32px为搭配中尺寸输入框高度，搭配大尺寸输入框时标签最小高度为40px）；
- 开关、单选、复选框、单行文本在表单中行高为32px（32px为搭配中尺寸输入框高度，搭配大尺寸输入框时各项最小高度为40px）；
- 标签与操作项顶对齐；
- 右侧内容非常规输入项，建议标签与右侧内容第一行文案对齐，也可根据场景自行调整。

![4-1-1](https://drive.google.com/thumbnail?sz=w3000&id=1PWu18oiWNZ7ZVo4-UjDqWhFBKQnhIdVj =100%x)

![4-1-2](https://drive.google.com/thumbnail?sz=w3000&id=1J9oKsLTfnsJ-X3e5YPhBphTd2LHDvy7h =100%x)

![4-1-3](https://drive.google.com/thumbnail?sz=w3000&id=1jiGQuN4MaVJz-F8haIyVBrHtDvzca_OW =100%x)


### 2. 行内分布表单
- 表单整体在页面中默认左对齐；
- 当列表为一行n列时，按钮水平排布，但列表为n行n列时，按钮垂直排布；
- 输入项列数建议最多不超过3列；
- 文本、开关、单选、复选框、单行文本在表单中行高为32px。

![4-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1r-v1djXTxvfI25xxqig4JZshN0NG3Trn =100%x)


![4-2-2](https://drive.google.com/thumbnail?sz=w3000&id=1uKzwZNUv17yL4-PlMxJPC5tot29NmA45 =100%x)

## 场景示例
输入框和文字说明为左右关系（常规表单）

![5-1](https://drive.google.com/thumbnail?sz=w3000&id=1Cj4z_0W57c7P2Ztf0k_myINuSwvPOxMd =100%x)

在弹窗中，默认采用垂直分布表单。

![5-2](https://drive.google.com/thumbnail?sz=w3000&id=193gtxbJrMh37wJfEbHD4czSuxUsTk_Yc =100%x)

在页面横向排布功能模块导致表单宽度有限，且信息需要更整齐地排布时，采用垂直分布表单。

![5-3](https://drive.google.com/thumbnail?sz=w3000&id=18_zs2ay22Cu_A4lbP2yv1B04WzmgQXZW =100%x)

在“筛选”这类型场景下，优先考虑行内分布表单样式。

![5-4](https://drive.google.com/thumbnail?sz=w3000&id=1AlAI82YkmsVwDHbqYEyJyiQ6IwO_Zfkh =100%x)

