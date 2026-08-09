---
extend: /zh/components/alert
---

## 组件元素
<br />

::::row
:::col :span="6"
![](https://drive.google.com/thumbnail?sz=w3000&id=1R25suErzsimlnWQF7ZJkvW6bsoco3__2 =100%x)
:::
:::col :span="1"
<br />
:::
:::col :span="5"
1. **容器**：承载消息提示内容的图形元素。
2. **图标**：直观表达提示含义，让信息类型更加直观。
3. **提示文案**：词组或短句，常规一行即可。
4. **文字链（可选）**：提供跳转，引导进一步操作。
5. **关闭按钮（可选）**：用户关闭后，提示消失。
:::
::::

## 类型汇总
|名称|基础样式|使用场景|
|:--|:--|:--|
|<div style="width:100px">**普通提示**</div>|![test](https://drive.google.com/thumbnail?sz=w3000&id=1vqwNXNJz19NEKBmZWl_l8hunScKEd3Ev =480x)|用于展示用户需要特别关注的重要功能、系统提示|
|**可关闭提示**|![test](https://drive.google.com/thumbnail?sz=w3000&id=153xdww7lzwgVW-yPn6ah2rKVjLel4sXJ =480x)|用于展示用户需要关注的重要功能、系统提示|
|**带辅助文字提示**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Aefo-Pi2YW30pjLjCgjYNVpIgzNdKS-8 =480x)|用于展示有一定解释内容的重要功能、系统提示|
|**带文字链接提示**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1Wxnn5zhTOamgGNS946lU7m7NR-KW8WVl =480x)|用于展示需要关注并有明确行动指引的提示|
|**无icon提示**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1t_cSikexZi3V9NxjWZ0wV8oCa-BVy_4w =480x)|用于展示层级较低的，警示性较弱但是需要用户长期关注的提示|

## 使用用法
- **交互规则**：随页面加载出现；
- **位置**：页面顶部、页面标题与主导航之间或主导航与页面内容之间；
- **格式**：提示问文字不超过 3 行；
- **类型**：含 4 种类型：成功、错误、常规、警告；
- **数量**：同一位置最多出现 2 条alert；
- **排序**：同一位置最多出现 2 条alert，展示优先级为不可关闭>可关闭类型，其他情况依据业务场景评估。

### 1. 普通提示
::::row
:::col :span="5"
【使用规则】提示只有在警告情况解除后方消失，用户无法关闭。
:::
:::col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1U8EsM1Q6hdbDCWaSiOGccKNcMU6La9NR =100%x)
:::
::::

### 2. 可关闭提示
::::row
:::col :span="5"
【使用规则】用户点击关闭按钮后，不再展示提示。
:::
:::col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=10Bqiu7h0RqAz5QgxiJgN10NL7o_QAKc7 =100%x)
:::
::::

### 3. 带辅助文字提示
::::row
:::col :span="5"
【使用规则】文字包含标题及辅助解释，标题不可超出一行，辅助解释不超出3行。
:::
:::col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1ZYiFQdM66EUf05QfQNRL4ivAnWTub23c =100%x)
:::
::::

### 4. 带文字链接提示
::::row
:::col :span="5"
【使用规则】
 - **交互**：点击文字链按钮，跳转链接页面；
 - **位置**：文字链位于辅助文字末尾；
 - **数量**：允许同一alert含多条文字链，建议不超过两个，位置尽可能位于辅助文字末尾。
:::
:::col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1u4IbylN4LNDVt_hzT0LEN4JS4Uh50SRE =100%x)
:::
::::

### 5. 无图标提示
::::row
:::col :span="5"
【使用规则】层级较低，但用户需长期关注。
:::
:::col :span="7"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1wmuxz_5VwZzxTH2AqO8891nVFF9wPO9e =100%x)
:::
::::

## 视觉样式 
### 1. 尺寸
宽度：警告提示条宽度会撑满所在区域宽度，在有效区域内两端对齐。

::::row
:::col :span="6"
#### 1.1 默认尺寸
Basic高度40px；适用于页面顶部、页面标题及主导航之间等大部分场景。
:::
:::col :span="6"
#### 1.2 小尺寸
Basic高度40px；Small高度32px，仅适用于模块内部。
:::
::::
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1n263-VxYv2tslA4u6LcitEJpzlt867Ke =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1vod7JOS-ZFZauX8Wn1v4U_CVDGmcTSHi =100%x)
:::
::::
### 2. 类型
含有4种提示类型：成功、错误、常规、警告。

::::row
:::col :span="6"
#### 2.1 成功
- **文字**：font-size: 14px；color: #666666；
- **容器**：background: #EAF8EE；border: 1px solid rgba(85,204,119,0.60)；border-radius: 4px；
- **图标**：color: #55CC77。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1SbuVdS6pCQbuX7afkH-IN9aROS4VeWBO =100%x)
:::
:::col :span="6"
#### 2.2 失败
- **文字**：font-size: 14px；color: #666666；
- **容器**：background: #FFE9E8；border: 1px solid rgba(255,71,66,0.60)；border-radius: 4px；
- **图标**：color: #FF4742。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1oRsanRk8r4WJohaBgU0hI-v2s43sQ9ya =100%x)
:::
::::
::::row
:::col :span="6"
#### 2.3 常规
- **文字**：font-size: 14px；color: #666666；
- **容器**：background: #E5EEFB；border: 1px solid rgba(38,115,221,0.60)； border-radius: 4px；
- **图标**：color: #2673DD。

![test](https://drive.google.com/thumbnail?sz=w3000&id=12lqxfWEOVoU-3UAXav5AYha3IxuYT-ot =100%x)
:::
:::col :span="6"
#### 2.4 警告
- **文字**：font-size: 14px；color: #666666；
- **容器**：background: #FFF7E0；border: 1px solid rgba(255,191,0,0.60)；border-radius: 4px;
- **图标**：color: #FFBF00。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1A1USZO70fReeWveKWyA7G7Y7RstP4RLN =100%x)
:::
::::
## 基本状态
|状态名称|状态样式|描述|
|:--|:--|:--|
|<div style="width:100px">**Normal**</div>|![test](https://drive.google.com/thumbnail?sz=w3000&id=1SMwbtYdbCvBxw5zwiknMloXFHUxP2jA9 =480x)|icon-color：#B7B7B7|
|**Hover**|![test](https://drive.google.com/thumbnail?sz=w3000&id=1776yXRvhwEfuCo5IJucg9fqW_s4_Ho9R =480x)|icon-color：#B7B7B7 + {#000000, 0.40}|

## 场景示例
![test](https://drive.google.com/thumbnail?sz=w3000&id=1DD_f7T4wJ-h5dP_GU8ybWZSBUitxlw65 =100%x)

    