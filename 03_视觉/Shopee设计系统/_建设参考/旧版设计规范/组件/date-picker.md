---
extend: /zh/components/date-picker
---
## 组件元素
<br />

::::row 
:::col :span="5" 
![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1pLj8kPOIg9FwAvV-aIUmJ7ORRfXZzxMf =100%x)
:::
:::col :span="1" 
<br />
:::
:::col :span="6" 
1. **时间输入框** 日期格式按照日-月-年的方式显示。
2. **月分页**
3. **年分页**
4. **月和年快速选择入口**
5. **周期日历表：**
- 按照东南亚国家习惯，每周是从周日计算到周六；
- 日期跨月份显示。
6. **当前日期**
7. **选定日期**
:::
::::


## 类型汇总
根据具体业务场景选择不同的日期选择类型，具体如下：

### 1. 任意日期选择（日、月）
【使用场景】日期选择的场景下可通用，月同理。

![2-1-1](https://drive.google.com/thumbnail?sz=w3000&id=1WLu52cgv8Et4rSTz-Iw3qhUcSSQFM7z4 =100%x)

### 2. 任意日期范围选择
【使用场景】业务场景下要求自由选择某区间段时间时使用。自定义月份/年份选择也可以使用。

![2-1-2](https://drive.google.com/thumbnail?sz=w3000&id=1uMm0eQ3ghBrNUHpWABN6NcH2D6NHGPAl =100%x)

### 3. 带快捷日期选择（时间点、时间范围）
【使用场景】需要快捷选择并能够也做自定义的场景下使用。

![2-1-3](https://drive.google.com/thumbnail?sz=w3000&id=14RoicUEXsiFcfCew8WI5fYYpscf53M6B =100%x)

::::row 
:::col :span="6"
### 4. 自由日期+自由时间组合选择
【使用场景】适用于任意选择单个日期+时间点组合的场景下使用。
:::
:::col :span="6" 
### 5.自由日期+固定时间组合选择
【使用场景】适用于任意选择单个日期+时间点组合，且业务需要对时间进行配置的场景下使用。
:::
::::
::::row 
:::col :span="6"
![2-1-4](https://drive.google.com/thumbnail?sz=w3000&id=1XddBIVABybHhUgZtxFcJqOEDg3JSOeOW =100%x)
:::
:::col :span="6"
![2-1-5](https://drive.google.com/thumbnail?sz=w3000&id=1z976-wObd9sCBV-ZRQonYql2KEBYZicV =100%x)
:::
::::
### 6.特殊日期选择
【使用场景】适用于有不同业务诉求的区间时间选择要求时。

![2-1-6](https://drive.google.com/thumbnail?sz=w3000&id=1nkrhb7T7GkG2rueEkWdtdqEib1FTBX-z =100%x)


## 使用用法

### 1. 任意日期选择
【使用规则】
- 弹出框的交互，默认从下方弹出，当下方空间不够时可上方弹出；
- 时间输入框normal态默认使用暗文为用户提供快速引导，可根据业务需求去除或修改。

![2-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1NQC0bHdtbjCLZYhyo7IDzdjqofsvt7d4 =100%x)

### 2. 任意日期范围选择
【使用规则】直接以一个整体的组件的形式使用，无需拆分成两个时间控件的组合。
【取消机制】
- 当前已有选中的时间，若重新点选时间时，默认即重新选择；
- 重新选择时，若不选择第二个时间，时间选择器离焦，则默认是放弃选择操作，保持现有的时间不变。

![2-2-2](https://drive.google.com/thumbnail?sz=w3000&id=1fB0pzW_1CM_525fi7iOMAFXWYovDsGvr =100%x)

### 3. 带快捷日期选择（时间点、时间范围）
【使用规则】
- 根据业务场景自行增减、修改快捷选项； 
- 该组件是在任意时间选择和任意时间段选择组件的基础上的拓展。


![2-2-3](https://drive.google.com/thumbnail?sz=w3000&id=1jRe1k9izVSj-s7j4X134lYH5Vtm7gHwi =100%x)

::::row 
:::col :span="6"
### 4.自由日期+自由时间组合选择
【使用规则】
- 需要满足日期+快捷时间选择的场景下，即可使用；
- 时间选择采用是24小时制的时间选择。
:::
:::col :span="6" 
### 5.自由日期+固定时间组合选择
【使用规则】
- 根据业务，可以随意定制可选时间点的值；
- 时间选择采用是24小时制的时间选择。
:::
::::
::::row 
:::col :span="6"
![2-2-4](https://drive.google.com/thumbnail?sz=w3000&id=1825P4zR6HrZ_A0HKSOXK3zKqz36B38x4 =100%x)
:::
:::col :span="6"
![2-2-5](https://drive.google.com/thumbnail?sz=w3000&id=1EH6ErxBaN21R0pH5zCNMBLC9Kpxz_a5n =100%x)
:::
::::
### 6.特殊日期选择
【使用规则】
- 可自行跟据业务场景增加删减快捷选项。其中固定的时间与自定义的快捷选择相互不一样；
- 自然周可根据不同地区习惯灵活调整展现形式。

![2-2-6](https://drive.google.com/thumbnail?sz=w3000&id=1OE55IZLPugwiAw-pJLPqb5LReh2nvDL5 =100%x)


## 视觉样式
### 1. 日期选择框尺寸
- 默认宽度为240px，特殊日期选择框320px，最小宽度80px，需要照顾页面整体对齐关系情况，可按照当前页面内容100%确定宽度；
- **border-radius:** 4px;  **font-size:** 14px。
::::row
:::col :span="4"
![3-1-1](https://drive.google.com/thumbnail?sz=w3000&id=1oWYbcKhK7CyQ9fvA8JTF6iPS4zPV5f9K =100%x)
:::
:::col :span="4"
![3-1-2](https://drive.google.com/thumbnail?sz=w3000&id=1V0Fcv-9YqeBN6_0K-xH4Y11eCiksSDow =100%x)
:::
:::col :span="4"
![3-1-3](https://drive.google.com/thumbnail?sz=w3000&id=1vERsHWtW9tZlY67gxiuacNQCYF-FG7p9 =100%x)
:::
::::
### 2. 下拉框尺寸
- **background:** #FFFFFF;  **box-shadow:** 0 6px 16px 0 #000000 opacity 12%；**border-radius:** 4px；font-size: 14px; 
- **font-color:** #333333（正常）/ #EE4D2D（当前）/ #333333 opacity 50%（不可选）。

![3-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1-_aPXAavDih9FV-DlFU01vdqgIqYWnsl =100%x)

### 3. 日期选择框通用样式
| 状态名称 | 状态样式 | 描述 |
| :--  | :-- | :-- |
|<div style="width:240px">**Normal**</div>|<div style="width:320px">![3-3-1](https://drive.google.com/thumbnail?sz=w3000&id=19YaOvwar4wU8hAui5wAxG7bMlE2eCQ6q =240x)</div>|**background:** #FFFFFF;<br />**border:** 1px solid #E5E5E5;<br /> **font-color：**#B7B7B7；|
|**Hover**|![3-3-2](https://drive.google.com/thumbnail?sz=w3000&id=1S-67LzE9D0j53TZDr03eIk3X2UtZOkX1 =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #B7B7B7;<br /> **font-color：**#333333（已选）/ #B7B7B7（未选）；|
|**Selected**|![3-3-3](https://drive.google.com/thumbnail?sz=w3000&id=1FhRX4qAGf7jS5Dl03M5Wg5V6OmDreNbj =240x)|**background:** #FFFFFF;<br />**border:** 1px solid #DBDBDB;;<br /> **font-color：**#333333；|
|**Disabled**|![3-3-4](https://drive.google.com/thumbnail?sz=w3000&id=1fiq2q2Jl9T8lkXYC4miETVL-xZaPgnQ6 =240x)|**background:** #F6F6F6;<br />**border:** 1px solid #E5E5E5;;<br /> **font-color：**#B7B7B7；|

### 4. 下拉菜单状态汇总
| Normal | Hover | Selected | Disable |
| :-- | :-- | :-- | :-- |
![3-4-1](https://drive.google.com/thumbnail?sz=w3000&id=14KrXVcShWjFv5ePLitJ4bTsWrkeBuMA-  =84%x)|![3-4-2](https://drive.google.com/thumbnail?sz=w3000&id=1yoo8NMptqqpnN5rkLs79qlXUdqMWBHQf =84%x)|![3-4-3](https://drive.google.com/thumbnail?sz=w3000&id=1x6NR43OrS4p3yWTrQZW5dlm5YL8mKWLv =84%x)|![3-4-4](https://drive.google.com/thumbnail?sz=w3000&id=1yejBGv4quKfd6qUXw921DewJki9eUclr =84%x)|
**background：**#FFFFFF<br />**font-weight:** 400；<br />**color:** #333333;<br />**font-weight:** 500（当前）<br />**color:** #EE4D2D； | 遮罩 #000000，4%；| **background:** #EE4D2D;<br />**font-weight:** 500；<br />**color:** #FFFFFF; | 基于Normal整体opacity：50% |

## 场景示例
![5-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1AwmJbG60zgfx53tdR9ejai2gHb2YHHia =100%x)
    