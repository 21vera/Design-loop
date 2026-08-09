---
extend: /zh/components/pagination
---

## 类型汇总 
| 名称 | 组件类型 | 使用场景 |
| :--  | :-- | :-- |
| <div style="width:120px">**极简分页**</div> | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1nFbPwtP2AeZcMADvI280njKndOL01shK =209x) | - 应用于展示空间受限或无须更多的分页功能的简单翻页时 |
| **基础分页** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=11FWIIHNnVI3tnAKTXzlxZ9b18wVW5M4v =332x) | - 应用于主页面需要加载多个数据的时候<br />- 页面总数：基础分页 9 个坑位 |
| **带省略的基础分页** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1afh2N-WDEMlEbTS41pK8NvqbWDw8usK7 =416x) | - 页面总数：当总页数多于 9 页时 |
| **带快速跳转的分页** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1JykSBId1f7bT1WhU0QcbR2GBezSIAoWd =502x) | - 允许用户快速跳转页面 |
| **页数展示调整的分页** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1zVxN6DsCXm8B4qaPq1e-DmnvpJTMidvg =439x) | - 允许用户自行调整每页显示的条目数量 |
| **页数展示调整与快速跳转的分页** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1Yz6ifC8ykEgWKnAFH3jokmF5YYzfkj2r =608x) | - 允许用户自行调整页面展示条目数量，以及快速跳转页面 |


## 使用用法

【位置】置于容器内容区块的底部，与内容右对齐；

【使用规则】
- 一般情况下，当超 9 页时，显示省略号，省略号必然位于第 2 坑位或倒数第 2 坑位；
- 省略号出现的情形归纳如下（假使当前共有 n 页且 n > 9）：

   · 当前页数位于 1 / 2 / 3 号坑位时：倒数第 2 号坑位显示省略号；

   · 当前页数位于n / n-1 / n-2 号坑位时：在 2 号坑位显示省略号；

   · 当 n > 11 且当前页数不位于以上所列举6个坑位时：在2号与倒数第2号坑位均显示省略号；
- 翻页器对应每页展示的数量可以根据业务需求设定；
- 点击切换页面，当前页面刷新；
- 如果当前页面信息内容 1 页可展示完毕，分页器应当根据当前情况隐藏。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1Pz8SVj4rDrTQzbuvw7RDKOo4_-woogfV =100%x)


## 视觉样式

- Normal：**font-size**: 14px; **color**: #333333; 
- Selected: **font-size**: 14px; **color**: #EE4D2D, 字重600；
- Hover: **font-size**: 14px; **color**: #EE4D2D;  icon颜色与字体hover样式一致；
- 辅助文字: **font-size**: 14px; **color**: #999999;
- 跳转页面默认暗纹字体颜色与input规范一致。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1UWtFMQkCPjscY6P5jB5zKLZdry2jVJLJ =100%x)


## 场景示例
![test](https://drive.google.com/thumbnail?sz=w3000&id=1SS7YFmrAGLQ39U0hO0r26ZNIhrOE3gSx =100%x)