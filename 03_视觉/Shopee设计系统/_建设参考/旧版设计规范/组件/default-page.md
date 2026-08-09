---
extend: /zh/components/default-page
---

## 组件元素 
<br />

:::: row

::: col :span="5"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1gFr6jjtDEQryxFWY_pM0XMpnkvfA5VOy =100%x)
:::
::: col :span="1"
<br />
:::
::: col :span="6"
<br />

1. **图案**：引发当前异常原因的形象化表达，一般为包含品牌元素插图、插画等。
2. **提示文案**：告知引发当前异常的原因及解决办法。
3. **文字链**：引导用户进行操作。
:::
::::

## 类型汇总
| 名称 | 基础样式 | 使用场景 |
| :--  | :--: | :-- |
| **页面空状态** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1_Y99s8_V_hLvUu6wZ4p29ZMZNdhgrHBt =115x) | - 最基础的页面空状态。 |
| **弱操作指引** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1-fqi1dhbMKTiZ84OO8-MoFpHpCWH-eGK =166x) | - 适用于带文字链的弱操作指引。 |
| **强操作指引** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1nLVPqs1VU88rH6Io7cZBD5ZkMdVQDP6V =99x) | - 适用于带提示按钮的强操作指引。 |
| **页面异常报错** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1AQIc2Ci_3h3s4T8Kul0RmLdTCOQAUylC =154x) | - 适用于断网、页面不存在或其他非正常操作后展示的场景。 |

## 使用用法
### 1. 页面空状态
:::: row
::: col :span="5"
【使用规则】
- 位置：位于页面中间；
- 位置：空状态只替代应有数据的位置，页面中其他元素正常展示；
- 触发：当页面检测到没有数据时，出现该空状态；
- 消失规则：当系统检测到新增数据时，该空状态消失，展示已有的数据。
:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1KqPSQSXTPhCAFC8aB9ihALo8YNmkKGhZ =100%x)
:::
::::

### 2. 强引导空状态
:::: row 
::: col :span="5"
【使用规则】
- 当页面的空状态为用户可以自定义管理的功能页，可以提供给用户引导操作，让用户新增数据，如添加银行卡，添加图片等场景。
:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1wBiWGrQATcur-y4ZyBbgWEJDQpV3K0T0 =100%x)
:::
::::

### 3. 页面异常报错
:::: row 
::: col :span="5"
【使用规则】
- 位置：以页面的形式展示，位置在页面的中央偏上方；
- 文案规则：提示文案简洁明了，最多不超过4行；
- 交互规则：
  · 该状态一直存在，直到页面异常问题解决；
  · 当页面异常问题解决后，该提示消失。

【异常流】
- 建议提供给用户重新加载的按钮或设置入口；
- 当前场景可以自定义的情况下，建议使用该样式。
:::
::: col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=15IIWXy55zhdk4TkgNKULveNPgZnExAhW =100%x)
:::
::::


## 视觉样式
### 1. 尺寸
- 描边粗细为1px；
- 文字字号14px，文字颜色#999999；
- 文案最长600px，超过需要折行。
:::: row 
::: col :span="4"
#### 1.1 Normal
- 正常大小的插图，默认下使用该尺寸（96px）。
:::
::: col :span="4"
#### 1.2 Small
- 在内容承载区域有限时使用（56px）。
:::
::: col :span="4"
#### 1.3 带操作指引
- 提示文案末尾添加超链接。
:::
::::
:::: row 
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Qva3l4UMAvkNGU4MK1oWInKLzCEHfWqv =100%x)
:::
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1psiqGM0MDBRxtP1ysJSBSh4h2NOBCxWV =100%x)
:::
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1mS6pk7lITBEHXnaiG4g1Pn5jFFa6XnFO =100%x)
:::
::::

### 2. 页面空状态
以下为当前平台现有空状态汇总，如不能满足项目需按照风格和样式逻辑绘制。
<br />

:::: row 
::: col :span="3"
**没有商品**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1dbUPDNkbDiqt4Y16t5fYGWvZkzbDmYG1 =100%x)
:::
::: col :span="3"
**没有数据**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1rRmkZJO_Lyha3vVSRxZ2pua4sGw1Ii0z =100%x)
:::
::: col :span="3"
**没有订单**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1ytdexKD1FMJXEd5B2eMkqhUEVoaLcQMj =100%x)
:::
::: col :span="3"
**没有交易记录**

![test](https://drive.google.com/thumbnail?sz=w3000&id=19DPSxW2MFRFpPiQxOMKdceA4hn_IcTMQ =100%x)
:::
::::

:::: row 
::: col :span="3"
**搜索结果不匹配**

![test](https://drive.google.com/thumbnail?sz=w3000&id=18g2l0JzMPT_Txww1zAIsDzJ-l_YFX9Q- =100%x)
:::
::: col :span="3"
**没有评价**

![test](https://drive.google.com/thumbnail?sz=w3000&id=15YSEYhhUlh7cSn3-OVjbg1G3mqcGMT2T =100%x)
:::
::: col :span="3"
**没有图片**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1mrrPz1oIPyp5beUYTRtRu--c_Md2tOfy =100%x)
:::
::: col :span="3"
**没有优惠券**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1uhlsDdvBBtpSxooaNe7648U8igneYYQL =100%x)
:::
::::

:::: row 
::: col :span="3"
**没有打折促销**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1Cki7tPoXVieWFCPgaofJHtn1xauprtt6 =100%x)
:::
::: col :span="3"
**没有权限**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1s1DSibht80uBHkZdBAKJLUtG2sE9WsY3 =100%x)
:::
::::



### 3. 页面异常报错

:::: row 
::: col :span="3"
**404报错**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1PDYAglb8X8ppL9u2bfFAszHnobgT3NO5 =100%x)
:::
::: col :span="3"
**系统错误**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1J9Bcd1wW1nY1N6zIU5aqS5K0qdhPWyCM =100%x)
:::
::: col :span="3"
**没有网络**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1EmLJJ5awFEf8GVZRwz2ZrTd10hyzJe8P =100%x)
:::
::: col :span="3"
**系统升级**

![test](https://drive.google.com/thumbnail?sz=w3000&id=1af7BTt9YqD_YLtZu2cFNZWC36U_5gdH5 =100%x)
:::
::::

### 4. 其他标注
![test](https://drive.google.com/thumbnail?sz=w3000&id=1BgBqudDbhW1hREJbOkh_8VpdNekCtw8A =100%x)

## 场景示例
![test](https://drive.google.com/thumbnail?sz=w3000&id=1mFZ8swfPBmjc41UL0C44xcBAvYLMu1u5 =100%x)

![test](https://drive.google.com/thumbnail?sz=w3000&id=1KX_zb5FyIsIVLbGwyBqTiDO4YP3oUdAF =100%x)

![test](https://drive.google.com/thumbnail?sz=w3000&id=13HKmkqjtPlK4jc-BqKw_ygsC0eTdLfwO =100%x)

![test](https://drive.google.com/thumbnail?sz=w3000&id=1gGezS3BO0kYVsKVEcaeOeoOisfKlQH1N =100%x)
