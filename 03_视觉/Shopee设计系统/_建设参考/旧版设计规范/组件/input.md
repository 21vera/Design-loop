---
extend: /zh/components/input
---

## 组件元素
<br />

:::: row
::: col :span="5"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1HYhkyHDK59rjMm_gGKWgw4s37wyiSDfu =90%x)
 :::
::: col :span="7"
1. **标签文字**：用于告知用户输入框内文本内容，每个输入框都应有一个标签，且始终可见；常规放于容器外部。

2. **输入框** 

3. **前置图标**（可选）：说明型图标，辅助标签文字表达输入框信息。

4. **输入文字**

5. **后置图标**（可选）：操作型图标，示意清晰且可点击操作。

6. **辅助文字**（可选）：对输入框的录入内容进行反馈、校验、提示说明。包含：校验录入内容正确/错误文案、提醒文案、辅助说明文案。)
:::
::::

## 类型汇总
<br />

|名称&编号|样式|使用场景|
|:--|:--|:--|:--|
|<div style="width:140px">**基本输入<br />DE-Input-1**</div>|![123](https://drive.google.com/thumbnail?sz=w3000&id=1JgLrI7PQwhUwdnDQtGnBIAguBwKkgvnO =220x)|- 适用于通用场景。|
|**带Icon输入<br />DE-Input-2**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1i3aT5T__n28FXmEm2y7WTAxUKqQJFZOi =460x)|- 特殊需要搜索需求时|
|**带指引的输入<br />DE-Input-3**|![123](https://drive.google.com/thumbnail?sz=w3000&id=118hzv9wAnhMGevHqoIBRE66LLp0AIOxX =220x)|- 当在某些特有的业务场景下，需要重点教育用户输入的字符信息时。|
|**数字输入<br />DE-Input-4**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1DYzOBGt0pP1njghPfrY_wS4Wg9HCagSb =140x)|- 度量、金额等数值相关的输入框性质，需要使用数值输入框。|
|**步进器<br />DE-Input-5**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1X8xNFiU8GGntXV-kXdm3mFyMQW8BKmEw =140x)|- 用于数字输入框，需要小范围精确调整数值时。|
|**文本框输入<br />DE-Input-6**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1THwO_LtIt-BGLzpuxm50m4Jgu1Z0fvxe =440x)|- 用于数字输入框，需要小范围精确调整数值时。|
|**有选项的输入<br />DE-Input-7**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1MHKHGN0nGg_Z1Cc79kJu8aLNx5QucCWH =361x)|- 输入内容范围由左侧选项限制。|

## 使用用法
**【位置规则】**：获焦时，自动默认从左往右依次填充内容。

**【交互规则】**：
- 获焦：鼠标点击输入框区域即获焦，获焦时暗文消失（特殊业务可以使用获焦暗文保留的交互）；
- 离焦：鼠标点击输入框外的区域即离焦；
- 离焦校验：输入值的准确性/输入内容的校验场景。输入框离焦时，输入值不消失，校验结果保留（部分业务场景，可将离焦条件放在某个按钮上面，进行输入值的校验）直到再次修改正确后校验结果消失，输入框恢复正常；
- 实时校验：实时校验输入值的准确性，适合一些沉浸式填写的表单结构。从鼠标获焦开始，前台实时的对变更输入值进行校核反馈。输入框离焦之后，输入值不在范围内，则清空输入值，同时校验文案取消；反之，则文案显示。

**【清除内容规则】**：
- 手动清除：获焦，直接删除录入数据；
- 快速清除：获焦显示快速清除icon，点击icon直接清除全录入内容，不可恢复操作。

### 1. 数值输入框
数值输入框支持平台各种数值相关信息的录入。
<br />

#### 1.1 基本数值输入框
:::: row
::: col :span="5"
**【交互规则】**
- 弱文案：默认为0/0.00数值(根据业务形态规定的小数点后面的位数显示)，若有业务要求弱提示文案，则优先显示；
**【输入内容规则】** 默认只支持录入数值，其它字符串无法写入。

:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1Z7Ak2wIR1HXPRTbEQQRDhoILdGFu4GTN =100%x)
:::
::::
<br />

#### 1.2 步进器
:::: row
::: col :span="5"

**【交互规则】**
- 获焦：Hover/Focus状态下显示增减按钮。失焦时增减按钮消失；若输入框右端有固定占位区，增减按钮会覆盖原占位内容；

**【输入内容规则】**

- 步进精度：默认为可允许输入数值的最小单位数；
- 范围：若输入的数值超出范围，离焦时输入框自动显示上限/下限值；增/减后的数值若超出范围则展示上限/下限值；对于还未录入的输入框，点击增减按钮时从0开始计算。例如，点击增加按钮显示1，点击减少按钮显示-1；若下限值为0，点击减按钮则显示0。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1rknd2SUBbWCwOAfXxPDzfsQJrXYACtsC =100%x)
:::
::::
<br />

#### 1.3 巴西邮编输入框
:::: row
::: col :span="5"
**【使用规则】**
- 位置：Tooltips跟随触点位置。
- 交互规则：
· 输入：自动帮助用户加分割，超过5位加“-”；
当用户输入第九个数值时，无法写入数值；
· 校验：输入框校验满足8位数值时，就开始对邮编进行分析以及得出地址结果；
· 获焦：输入框重新获焦，保留前面的状态，离焦之后状态继续循环，当在删除信息时，位数要低于或删除完毕等于一五位数值时，跟随的“-”连同一起清除。

:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1tm5UD1ngBQ9kYpU3SuboC2bCO2dhdAJy =100%x)
:::
::::
<br />

### 2. 输入框的指引与提示
输入框作为最基本的操作控件，在每一种状态下都需要给予用户清晰的指引与反馈，同样根据不同的使用场景，有不同的使用类型，具体如下：

<br />

#### 2.1. 文字提示
最基本的提示形态，可用暗文或输入框下面的提示文案进行引导，在SC设计中应优先选用该种提示类型。

<br />

**暗文提示** 
:::: row
::: col :span="5"

	

**【使用规则】** 为用户输入什么内容提供快速引导，在输入正式内容时被覆盖。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1TLd-wJ3_4CvlGrE4OHCozq21pOIHP7lC =100%x)
:::
::::
<br />

**明文提示**
:::: row
::: col :span="5"

**【使用规则】** 需对输入框信息进行特殊提示，并方便用户在输入过程中进行对照时使用，该提示为常驻信息。
 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=12dPonawkNgPBZE9raiRpVsWKk94-9Y0x =100%x)
:::
::::
<br />

**计数器**

:::: row
::: col :span="5"

**【使用规则】** 输入框有限定字符数时，显示当前已输入字符数/字符数上限；输入内容达到字符数上限，计数器文字高亮提示：

- 建议在有计数器时，使用固定文本框或文本域，尽量能完整展示文本内容；
- 不建议输入的文本高度自适应增高；
- 特使情况，可使用可拉伸文本域。

 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1txDBV19s-MPk7_vXmtH8RG2nWu-9pTHl =100%x)
:::
::::
<br />

**附加单位提示**
:::: row
::: col :span="5"
**【使用规则】** 适用于有数值、金额、或者是计量单位输入的场景。

 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=15UubSS7Jy-iAps4LcS-FQFvaKIArDbLg =100%x)
:::
::::
<br />

#### 2.2. 气泡提示
:::: row
::: col :span="5"
**【使用规则】** 在某些特殊场景下，比如表格，由于对布局的控制更加严格，为了更好的输入和反馈体验，提示文字可以以气泡形式出现，详细气泡提示规范请参考 Popover。

 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1q66a3OB_1APlkogLfQ6ZgLlQQRrrtcKT =100%x)
:::
::::
<br />


#### 2.3. 图标提示
在某些场景下，icon能帮助用户快速理解相关输入信息或反馈结果。

<br />

**校验图标提示**
:::: row
::: col :span="5"

**【使用规则】** 需要对输入框内容进行及时判断并强调验证结果正确与错误时使用，常用于校验密码或条件判断。

 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1lgZcshmehSGYU2U-fd-TufsLk8GEGMa2 =100%x)
:::
::::


**辅助说明型图标提示**
:::: row
::: col :span="5"
**【使用规则】** 前置icon，对于icon无法表意明确的，不要使用；常用于登录用户名、密码、时间选择。

 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1gKtM2GRn254VKXb9U3vLDOF4Muv307nD =100%x)
:::
::::
<br />

### 3. 文本框输入

**【使用规则】** 支持大量纯文本输入时，使用文本框。
- 扩展规则：根据输入内容的高度自适应扩展输入框的高度。

![123](https://drive.google.com/thumbnail?sz=w3000&id=106gkldxcesAcNOrhPQk4NkzMTk0qneAW =100%x)
<br />

## 视觉样式

### 1.尺寸
**border**：1px；**border-radius**: 4px; **font-size**: 14px（输入框内文字），12px（指引文字+反馈文字）; **font-color**：#B7B7B7（输入前），#333333（输入后）

:::: row
::: col :span="4"
#### 1.1 Large
- 匹配页面其他元素尺寸较大时才使用；
- 结构：Text, Icon+Text，单位+Text
:::

::: col :span="4"
#### 1.2 Normal
- 正常大小输入框，默认下使用该尺寸；
- 结构：Text, Icon+Text，单位+Text。
:::

::: col :span="4"
#### 1.3 Small
- 在内容承载区域有限时使用，一般不使用；
- 结构：Text
:::
::::

:::: row
::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1XF7Brb_XKfpny2UCEwlgKYbqNyOuhdTp =100%x)
:::

::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1fub-069Zk6ftv61GPP9JIE-fCijs_kbM =100%x)
:::

::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=19sfM16Bkk8dhz8CfH9CZVlF4fDRnMRZ- =100%x)
:::
::::
<br />

:::: row
::: col :span="6"

### 2. 长度区间

- 输入框默认宽度为240px；
- 往下可以按80px递减为160px，120px，最小为80px；
- 往上可以按80px、120px、160px递增为320px，600px；
- 如果以上规则无法满足，可以选择按照当前页面内容100%确定宽度。
 :::
::: col :span="6"
### 3.有选项的输入长度区间

-建议右侧输入框的宽度不小于左侧选择框宽度的1.5倍。
 
:::
::::

:::: row
::: col :span="6"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1JwX9tWY55eDjR6b3untyFEe-f1DvdFVB =100%x)
:::
::: col :span="6"
![123](https://drive.google.com/thumbnail?sz=w3000&id=15R3enPNIcmaVrxCWT_EVguyX4kQbTp-7 =100%x)
 
:::
::::


:::: row
::: col :span="6"	
### 4. 点击热区

- 输入框主操作热区或扩大，方便点击；步进器热区icon左右扩4px。

![123](https://drive.google.com/thumbnail?sz=w3000&id=1RLyIGsy3_DH5U0iysOk2U_pv1JXyOdZk =100%x)
:::
::: col :span="6"
<br />
:::
::::

<br />

### 5. 基本状态

| 状态名称 |状态样式|描述|
|:--|:--|:--|
|**Normal**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1M4mVN8Cp-787L9kWHqZCImoAXbIX8Idb =220x)|**background**: #FFFFFF;<br />**border**: 1px solid #E5E5E5;<br />**border-radius**: 4px;|
|**Hover**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1uQtNtq02-89drtvwVXT_rJc0149sO7vm =220x)|**background**: #FFFFFF;<br />**border**: 1px solid #B7B7B7;<br />**border-radius**: 4px;<br />**icon-color**：#B7B7B7 + {#000000, 0.40} |
|**Focus**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1zqLF2u5Mv19i7tAbnO_s5ShbN7GlNypB =220x)|光标颜色：#000000|
|**Disabled**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1euYcKX-ZY3YuRm3czvsPROf9YFZVylYC =220x)|**background**: #F6F6F6;<br />**border**: 1px solid #E5E5E5;<br />**border-radius**: 4px;<br />**icon-color**：#B7B7B7 + {#000000, 0.40} |
|**Verify**|![123](https://drive.google.com/thumbnail?sz=w3000&id=18fkZ_b6He8MqexQ9183f9R3ewsMe1TZg =480x)|**background**: #FFFFFF;<br />**border**: 1px solid #FF4742;<br />**border-radius**: 4px;|

<br />

### 6. 其他标注


![123](https://drive.google.com/thumbnail?sz=w3000&id=1jA93ah8B1pA85Byqr_wfMc6ef1dTz3Jr =100%x)

## 场景示例
输入框和文字说明为左右关系（常规表单）


![123](https://drive.google.com/thumbnail?sz=w3000&id=1GSaml2SZIzD1l13JU0OlXFxhc6BAgjUW =100%x)		
