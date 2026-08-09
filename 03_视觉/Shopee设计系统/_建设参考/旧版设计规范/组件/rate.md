---
extend: /zh/components/rate
---

## 组件元素
<br />

:::: row
::: col :span="5"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1OzJaN04H2dCMdQp7Vaz6CprqpQv3FKw0 =100%x)
:::
::: col :span="7"
<br />

1. **图标**: 一个图标代表一分或一级，共五个图标。
2. **辅助文案**：表达选中图标对应的评分数值或等级。
:::
::::


## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| <div style="width:200px">**可点击的评分**</div> | ![2_1](https://drive.google.com/thumbnail?sz=w3000&id=1SwszmygwqRXlfsaFMAx4Xl772RDAzL9H  =200x) | - 适用于需要用户对某一对象进行评价的场景。 |
| **只读的评分** | ![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1VVhElG42F0wT9jXyR5OqpvTACnynG82B =200x) | - 用于展示某一事物的评级时。 |

## 使用用法
1. 在用户打分或者查看分数时使用；
2. 一个星星代表一分或一级；
3. 填色星星代表已达到的数值，灰色星星代表未达到的部分。

### 1. 可点击的评分
:::: row
::: col :span="4"
【使用规则】
- 点击后评分的颜色状态和文案即时变化；
- Hover时星星的颜色随着鼠标动态变化，文案不变化；
- 评分精度可以是1或0.5。
:::
::: col :span="8"
![3_1](https://drive.google.com/thumbnail?sz=w3000&id=10D1f7CBQu13sr0h36AJyShzNWUuL12-m =100%x)
:::
::::

### 2. 只读的评分
:::: row
::: col :span="4"
【使用规则】
- 只读的评分星星不可点击；
- 分值最小单位可以是1、0.5或0.1。对于单位为0.1的评分，星星填充规则见右表；
- 分值单位为0.1时，建议使用辅助文案示意。
:::
::: col :span="8"
![3_2](https://drive.google.com/thumbnail?sz=w3000&id=1IMBor3G08h3HhtVBlXF_D8w1KibuguMj =100%x)
:::
::::

## 视觉样式
- 星星icon，尺寸为16px*16px；填充颜色：#FFBF009；未填充颜色：#E5E5E5；
- 辅助文案，font-size: 14px； color：#333333。


![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1fjaR7HdBtvx2CBkM_vQ2ShLr1_rYCs4v =100%x)

## 场景示例
![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1qPlshYbyXqxcuVYB84rBRCiGMJBkB6Lq =100%x)