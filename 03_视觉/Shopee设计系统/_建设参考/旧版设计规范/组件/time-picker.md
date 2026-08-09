---
extend: /zh/components/time-picker
---
## 组件元素
<br />

::::row 
:::col :span="5" 
![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1C9pt1w-45neblhtVjfOd7UOJwEUaDw6C =100%x)
:::
:::col :span="1" 
<br />
:::
:::col :span="6" 
1. **时间输入框：** 日期格式按照 hh:mm:ss 的方式显示。
2. **时间加减操作**
3. **时间表：**
	- 小时选择，24小时制，从00-23；
	- 分选择，60分制，从00-59；
	- 秒选择，60秒制，从00-59。
4. **选定日期**
5. **选择确认**
:::
::::

## 类型汇总
时间选择器分为任意时间选择和固定时间选择，任意时间选择可选择时间点，可根据场景选择使用时分秒、时分不同的组合。固定时间选择可选择时间点和时间段。
::::row 
:::col :span="6"
### 1. 任意时间选择（时分秒、时分）
【使用场景】适用于通用场景,可以选择使用 时分秒、时分不同的组合。
:::
:::col :span="6" 
### 2. 固定时间选择（时间点、时间段）
【使用场景】适用于选择固定时间/段的场景。
:::
::::
::::row 
:::col :span="6"
![2-1](https://drive.google.com/thumbnail?sz=w3000&id=1WT6WeH8cCWCHDoqvhM1Bbh0rHeZFwdQk =100%x)
:::
:::col :span="6"
![2-2](https://drive.google.com/thumbnail?sz=w3000&id=1t78rMyuhwM7XTAHWjhJRSiomgV29Gwe7 =100%x)
:::
::::

## 使用用法
::::row 
:::col :span="4"
### 1. 任意时间选择
【使用规则】
- 默认选中当前触发输入框的时间，特殊业务可自定义;
- 居中固定位置即为选中位；
- 点击数字及选中，并且定位到居中固定位。选择完时间，点击“confirm”代表此次选择行为的确认录入；
- hh：mm：ss 分别是3个并排的独立热区，每块热区支持单独的鼠标滚轮滚动；每块热区，增加上下切换键，支持点击切换列表视图，每次点击切换变更一个时间；
- 时间的显示切换到起点/终点位置时，则上下切换键状态不可点击，同样滑动也终止；
- 对于一些业务场景需要对选择的时间有限制条件，则不可选的时间可以用置灰的方式显示，hover上去是不可点击效果。
:::
:::col :span="8"
![3-1](https://drive.google.com/thumbnail?sz=w3000&id=1u8lzgCQ5oCf1te91d6bWCyeRIgRSx8qi =100%x)
:::
::::
:::: row
:::col :span="4"
### 2. 固定时间选择
【使用规则】
- 遵守「[Select 下拉选择](#/select/design)」交互规范；
- 根据业务，可以随意定制可选时间点的值；
- 时间选择采用是24小时制的时间选择。
:::
:::col :span="8"
![3-2](https://drive.google.com/thumbnail?sz=w3000&id=1o11Kw9_2GX3MpSu4leNNlPhPAka8oJBQ =100%x)
:::
::::

## 视觉样式
### 1. 时间选择框尺寸
- 默认宽度为160px，业务中特殊情况可按40的倍数调整；
- **border-radius:** 4px; **font-size:** 14px。
:::: row
:::col :span="4"
![4-1](https://drive.google.com/thumbnail?sz=w3000&id=19Ob_t60d-qYhhMMV4wtlOM7e5Skw44qJ =100%x)
:::
:::col :span="4"
![4-2](https://drive.google.com/thumbnail?sz=w3000&id=178y5p8RC7qECwcuulX8lqQzJWZ1EMD6S =100%x)
:::
:::col :span="4"
![4-3](https://drive.google.com/thumbnail?sz=w3000&id=13Jp2PQOEx0Uu52nyQnVjWfF5KRAutv59 =100%x)
:::
::::
### 2. 下拉框尺寸
- **background:** #FFFFFF; **box-shadow:** 0 6px 16px 0 #000000 12%; **border-radius:** 4px; **font-size:** 14px; **color:** #333333。
:::: row
:::col :span="6"
![4-4](https://drive.google.com/thumbnail?sz=w3000&id=1MTeD0Lfzxg4XxvePOfcuzxk34KE5wARr =100%x)
:::
:::col :span="6"
![4-5](https://drive.google.com/thumbnail?sz=w3000&id=1NodOn3eyk8YMwtJLVwRZpGrd9-GWrvhN =100%x)
:::
::::

## 基本状态
### 1. 时间选择框状态汇总
| 状态名称 | 状态样式 | 描述 |
| :--  | :-- | :-- |
|<div style="width:240px">**Normal**</div>|<div style="width:300px">![5-1-1](https://drive.google.com/thumbnail?sz=w3000&id=1gm6IbiAKXkbjJh3NgeCNfWGtq6NMb3c2 =160x)</div>|**background:** #FFFFFF;<br />**border:** 1px solid #E5E5E5;<br /> **font-color：**#B7B7B7；|
|**Hover**|![5-1-2](https://drive.google.com/thumbnail?sz=w3000&id=1pcLK-jxN1mxkvejJx6FnhvvXHEwSlOOo =160x)|**background:** #FFFFFF;<br />**border:** 1px solid #B7B7B7;<br /> **font-color：**#333333（已选）/#B7B7B7（未选）；|
|**Selected**|![5-1-3](https://drive.google.com/thumbnail?sz=w3000&id=1n6lwpGslKAn3Yc-uG868yqTsEwhU6DJy =160x)|**background:** #FFFFFF;<br />**border:** 1px solid #DBDBDB;;<br /> **font-color：**#333333；|
|**Disabled**|![5-1-4](https://drive.google.com/thumbnail?sz=w3000&id=13M_5bWUsCjOtODYJoBTUH1WOAW8RGwPo =160x)|**background:** #F6F6F6;<br />**border:** 1px solid #E5E5E5;;<br /> **font-color：**#B7B7B7；|

### 2. 下拉菜单状态汇总
| 状态名称 | Normal | Hover | Selected | Disable |
| :--  | :-- | :-- | :-- | :-- |
|<div style="width:160px">**固定时间状态样式**</div>|![5-2-1](https://drive.google.com/thumbnail?sz=w3000&id=1HFBDtSYmkjlA99BELH2gDcBuyXXfRXcY  =90%x)|![5-2-2](https://drive.google.com/thumbnail?sz=w3000&id=1Zur-tjXKzAmemK9l637fWfBinxcaq_em =90%x)|![5-2-3](https://drive.google.com/thumbnail?sz=w3000&id=1Vp6vLNgZ2VWogIlWCA1R1UAUYmgO2UIF =90%x)|![5-2-4](https://drive.google.com/thumbnail?sz=w3000&id=1QqJpvbxp__meBWOn-k_HwKguog5eo2-L =90%x)|
|<div style="width:160px">**描述**</div>|**background:** #FFFFFF;<br />**font-weight:** 400；<br />**color:** #333333;| 遮罩 000000，4%；| **background:** #FFFFFF;<br />**font-weight:** 500；<br />**color:** #EE4D2D;|基于Normal整体opacity：50%；|
|<div style="width:160px">**任意时间选择样式**</div>|![5-2-5](https://drive.google.com/thumbnail?sz=w3000&id=1yIljIJLAObFb0JufJRkD3xzLdVMINACW  =90%x)|![5-2-6](https://drive.google.com/thumbnail?sz=w3000&id=1jrjmiEZ7Vsv1EYAdXgeBXDtwBI816M5- =90%x)|![5-2-7](https://drive.google.com/thumbnail?sz=w3000&id=1mmiJxR1fJ4xT7LZSxZIJCart6r4iiQxJ =90%x)|![5-2-8](https://drive.google.com/thumbnail?sz=w3000&id=1wcHX_ppKXGVdzYJa6Sc0pYS14-h0VHy- =90%x)|
|<div style="width:160px">**描述**</div>|**background:** #FFFFFF;<br />**font-weight:** 400（未选）<br />**color:** #999999（未选）| 遮罩 #000000，40%；| **font-weight:** 500（已选）<br />**color:** #EE4D2D（已选）| 不可选时间可以直接直接做隐藏, 或者40%不透明度；<br />icon 40%不透明度；|

## 场景示例
![6-1](https://drive.google.com/thumbnail?sz=w3000&id=1U-z-YjQ48-xGp7DZ4Msk2FKr9OpV5b0B =100%x)
