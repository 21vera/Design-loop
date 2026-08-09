---
extend: /zh/components/avatar
---

## 组件元素
<br />

::::row
:::col :span="3"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1mtqqohicxPr3Yk_OlsEkZihJBjl720YS =100%x)
:::
:::col :span="1"
<br />
:::
:::col :span="8"
<br />

1. **图片**
2. **遮罩**
:::
::::

## 类型汇总
|类型|基础样式|使用场景|
|:--|:--|:--|
|<div style="width:120px">**用户/店铺头像**</div>|![test](https://drive.google.com/thumbnail?sz=w3000&id=1QfU7I5sFmfjAHKlAvG-3NArfVouI8F77 =136x)|常用于用户头像。|
|**商品图片**|![test](https://drive.google.com/thumbnail?sz=w3000&id=115KZPQsF0iTnDKIqlC7cVdNE0RyhqH1T =56x)|常用于商品头像。|
|**用户默认/缺省头像**|![test](https://drive.google.com/thumbnail?sz=w3000&id=19oRAj66j3s8_57wZIqBrgvVJSduIrWPQ =56x)|适用于商品图片加载失败、无图片的情况。|
|**商品默认/缺省图**|![test](https://drive.google.com/thumbnail?sz=w3000&id=17_tCou-S0OXgn11qXe7mQO5eY306vyGm =56x)|适用于商品图片加载失败、无图片的情况。|

## 视觉样式
::::row
:::col :span="6"
### 1. 图片蒙层
- 图片统一遮罩: color: 000000 ; opacity: 0.4;
- 圆形头像：全圆角（即圆形）；
- 方形头像圆角: 2px。
:::
:::col :span="6"
### 2. 默认头像
- background: #F6F6F6;
- icon: color: 000000 ; opacity: 0.12。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1rjuM1V8ka3WrdFOhlnrRCm6nhXJkZx3x =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=17X-YjxXr-eMh9MsCA76n72WyjjefHE30 =100%x)
:::
::::
### 3. 尺寸规则
- 头像共有 4 种尺寸选择；
- 除了特殊情况（如需要考虑环境空间等原因，多组头像排列需要尺寸均等分），设计师尽可能遵循本头像的尺寸方案。

|尺寸|用户头像样式|商品图片样式|尺寸大小|
|:--|:--|:--|:--|
|<div style="width:80px">**Large**</div>|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Ke96QG0lB-9jKo5YYJ_GiqAnes7tCpnu =96x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1kF7SjdrZy6inAFvU4VbAPb_OPRCd-q7L =96x)|96*96|
|**Normal**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Ke96QG0lB-9jKo5YYJ_GiqAnes7tCpnu =56x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1kF7SjdrZy6inAFvU4VbAPb_OPRCd-q7L =56x)|56*56|
|**Small**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Ke96QG0lB-9jKo5YYJ_GiqAnes7tCpnu =32x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1kF7SjdrZy6inAFvU4VbAPb_OPRCd-q7L =32x)|32*32|
|**X-smalle**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Ke96QG0lB-9jKo5YYJ_GiqAnes7tCpnu =24x)|![test](https://drive.google.com/thumbnail?sz=w3000&id=1kF7SjdrZy6inAFvU4VbAPb_OPRCd-q7L =24x)|24*24|

## 场景示例
<br />

![test](https://drive.google.com/thumbnail?sz=w3000&id=14-3wLezGiffxvE_cjma8ytkFhPepoakJ =100%x)