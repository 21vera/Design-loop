---
extend: /zh/components/toast
---

## 组件元素
::::row
:::col :span="5"
![test](https://drive.google.com/thumbnail?sz=w3000&id=18mm7iAxb_pHBJ_QAZLfomEM3SzuyCfFk =100%x)
:::
:::col :span="7"
<br />

1. **容器**：承载消息提示内容的图形元素；
2. **图标**： 直观表达提示含义，让信息类型更加直观；
3. **提示文案**： 词组或短句，常规一行即可。
:::
::::
## 类型汇总
|名称|基础样式|使用场景|
|:--|:--:|:--|
|**成功形态**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1_JFI85PKI5tWDHY9qGDfFe4tpNORo-fx =360x)|- 在用户进行提交、确认等操作后触发；<br />- 反馈操作成功。|
|**错误形态**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1jzXnVA1yr7VD5e3IJV_B_KZ0xAwDDcne =360x)|- 在用户进行提交、确认等操作后触发；<br />- 反馈操作失败。|
|**常规形态**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1xL_H8ELu3XcdGrblKDRh-Ao43Pxox2A2 =360x)|- 在用户进行提交、确认等操作后触发；<br />- 反馈操作失败。|
|**警示形态**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1BNna0K72PJ_y7byFsWMMdLmc4rMXqnc2 =360x)|- 在用户进行提交、确认等操作后触发；<br />- 反馈操作失败。|
## 使用用法
1. **交互规则**：用户触发某页面级操作，提示自上而下落入页面顶部；
2. **消失规则**：默认出现3s， 自动淡出消失；
3. **位置**：悬浮页面顶部。

### 普通提醒
::::row
:::col :span="6"
【使用规则】
- 格式：提示问文字建议不超过2行；
- 文案：应清晰描述现状、解释原因、明确指示。

<br />

【异常流】用户同时触发多条不同Toast：
- 数量遵循一次性最多展示2条；
- 触发：其他提示在第一条消失后陆续出现，从上到下依次排列；
- 位置：旧的一条提示下移，新的提示出现在原提示位置；
- 类型：用户反复触发统一操作，相同Toast提示叠加展示。 

:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1CVrWyhjvjlKQ-i8PPdSPJSKed5_3Bv71 =100%x)
:::
::::
## 视觉样式 
### 1. 尺寸
- 背景：background: #FFFFFF; box-shadow: 0 0 16px 0 rgba(0,0,0,0.10), 0 8px 16px 0 rgba(0,0,0,0.06); border-radius: 4px；
- 文字：font-size: 14px; font-weight: 400；font-color: #333333；
- 图标：size: 16px。

::::row
:::col :span="4"
#### 1.1 基础
![test](https://drive.google.com/thumbnail?sz=w3000&id=1oKduoqVQ--hQrGVbDeLWl_afjtT6O8q0 =100%x)
:::
:::col :span="8"
#### 1.2 长度
- 最小宽度160px，最大宽度600px。
![test](https://drive.google.com/thumbnail?sz=w3000&id=1SjRK6wm2t_L6haG1dxTnUH8wzQewBeSz =100%x)
:::
::::
#### 1.3 两行文字
![test](https://drive.google.com/thumbnail?sz=w3000&id=1-I3wVSka2rCSf1JdA1OT6D_JXXVwjApe =100%x)
### 2. 位置说明
![test](https://drive.google.com/thumbnail?sz=w3000&id=1BIaH5yxRAcdsbIcVGKRO2Fw-Gkd5ceDO =100%x)