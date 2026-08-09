---
extend: /zh/components/checkbox
---

## 组件元素
<br />

:::: row
::: col :span="5"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1NyCbk5zzx12D007uCrSmap20MpFtoZ1H =100%x)
:::
::: col :span="7"
<br />

1. **复选框**: 可进行多选操作。
2. **复选文字**：操作说明文案。
:::
::::

## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| <div style="width:200px">**基本多选<br />DE-Select-Checkbox-1**</div> | ![2_1]( https://drive.google.com/thumbnail?sz=w3000&id=1hXc5G-xD0CGTYdgpF3XNW4nEJke6qAkN =200x) | - 一般复选场景下皆可以通用。 |
| **父子级多选<br />DE-Select-Checkbox-2** | ![2_2]( https://drive.google.com/thumbnail?sz=w3000&id=1_CcUgv0cjCtZuuw28lPBiOYdIHpju-Pd =200x) | - 适用于可选项多，且可选项可组织成集合选项的场景。 |


## 使用用法
通用场景：适用于多个备选项进行多选。
### 1. 基本多选
:::: row
::: col :span="4"
【使用规则】
- 排序：默认可选内容根据首字母a-z的顺序从左至右、由上往下依次排序；若选择有一定的频次统计，则可根据频率级别进行排序；若有其他具体的业务场景，则在另外根据业务重要级考虑排序；
- 交互规则：空心单击选中；再次点击已选中项，则返回空心的未选中状态。
:::
::: col :span="8"
![3_1](https://drive.google.com/thumbnail?sz=w3000&id=1Ytz2ehFDKU70xlhcbh1S_bO33LgdMFqH =100%x)
:::
::::

### 2. 父子级多选的使用
:::: row
::: col :span="4"

【使用规则】
- 布局：全选是全量选项的集合，在层级上是高于现有所有选项的，因此在布局上，需要体现出选项的父子层级关系；
- 排序：勾选父级选项时候，相应的子级全部勾选。
:::
::: col :span="8"
![3_2](https://drive.google.com/thumbnail?sz=w3000&id=1SRwenQf1pi16DDqtDaqU9txH0cS90aKl =100%x)
:::
::::

### 3. 多选带二级操作
:::: row
::: col :span="4"
【使用规则】
- 在普通情况下，默认使用普通横排形式排列选项；
- 在横排多行选项的时候，采用固定选项宽度的方式进行横排；
- 在单个选项内容过长或场景空间有限时，采用竖排形式排列选项。
:::
::: col :span="8"
![3_3](https://drive.google.com/thumbnail?sz=w3000&id=1_dxhyU3xYZcmsUlpQjpq_GNUF7LDxV_V =100%x)
:::
::::



## 视觉样式
### 尺寸
- 基本元件尺寸为16px。
<br />

#### 多选框
- 默认多选框的尺寸及热区尺寸

![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1NF1lXjNCSGgjjBDM_Yc2CPnqPIXsCxXY =100%x)

#### 横排及竖排尺寸
- 根据使用场景横排竖排时采用以下尺寸

![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1p86jZJg1uov6hNMQS7SqJD_1qzGFBeij =100%x)
<br />


### 基本样式
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **Normal** | ![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1lWP5WueIHCd3uh0CtyEKoayYPQC1W7vI =200x) | - background: #FFFFFF;<br />- border: 1px solid #D8D8D8;<br />- border-radius: 2px;<br />- font-color: #333333; |
| **Hover** | ![5_2](https://drive.google.com/thumbnail?sz=w3000&id=18JS5P8-RTALRY56W5z6YrFVIpqGYIof0 =200x) | - background: #FFFFFF;<br />- border: 1px solid #EE4D2D;<br />- border-radius: 2px;<br />- font-color: #333333; |
| **Selected** | ![5_3](https://drive.google.com/thumbnail?sz=w3000&id=1LzJuvz-BiWiRQknrFpYKEHJ47AAOxdRT =200x) | - background: #EE4D2D;<br />- border-radius: 2px;<br />- font-color: #333333; |
| **Indeterminate** | ![5_4](https://drive.google.com/thumbnail?sz=w3000&id=1i8_3vDMlZI3-G0lW94iYmyilZG-v0FXx =200x) | - background: #EE4D2D;<br />- border-radius: 2px;<br />- font-color: #333333; |
| **Disable(unselected)** | ![5_5](https://drive.google.com/thumbnail?sz=w3000&id=1sAaBNSy2-GylinaO2m8VYa4Yb2lYgXb- =200x) | - background: #EEEEEE;<br />- border: 1px solid #D8D8D8;<br />- border-radius: 2px;<br />- font-color: #333333; |
| **Disable(selected)** | ![5_6](https://drive.google.com/thumbnail?sz=w3000&id=1Kt1m7f9H1K6WkHJ_hxMnUdpa8qgEbP-3 =200x) | - 在Selected样式基础上{opacity: 50%}；<br />- font-color：#333333； |
| **Focus** | ![5_7](https://drive.google.com/thumbnail?sz=w3000&id=1mJ868eUU8fpMhDzFew__9C1cc2FYCwo7 =200x) |  |
<br />

## 场景示例
在普通情况下，默认使用横排24px间距的形式排列选项。

![6_1](https://drive.google.com/thumbnail?sz=w3000&id=1g-hDL0LTq51F1UMK6N6l9VwvOn7PtNKB =100%x)
在选项过多需要换行排列的时候，采用固定选项宽度的方式进行横排。

![6_2](https://drive.google.com/thumbnail?sz=w3000&id=1wOaliKDNZ7Dry9yR3e2HT517rPCxJ9SC =100%x)
在单个选项内容过长时，采用竖排形式排列选项。

![6_3](https://drive.google.com/thumbnail?sz=w3000&id=12W6E2BN1jFTR7B9P0FV6h-nipxAuJyM4 =100%x)
在场景空间有限，不足以横向排列选项时，采用竖排形式排列选项。

![6_4](https://drive.google.com/thumbnail?sz=w3000&id=1-9ORQMJzPMNy1jI_ESTY0jGARIseA8T4 =100%x)
