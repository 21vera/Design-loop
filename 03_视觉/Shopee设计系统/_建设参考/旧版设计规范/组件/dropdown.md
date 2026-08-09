---
extend: /zh/components/dropdown
---

## 组件元素
<br>

:::: row
::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=18L8ivh7Bc2hGSQfrzktCVRHye3S6EXpo =100%x)
:::
::: col :span="1"
<br />
:::
::: col :span="7"
**1. 下拉按钮**：触发下拉菜单出现的操作按钮，遵循GP-Button-下拉按钮规范。

**2. 下拉菜单**：容纳所有菜单选项的矩形浮层。

**3. 菜单选项**：点击菜单选项后，收起下拉菜单，执行相应的命令。

:::
::::

## 类型汇总
<br>

|名称|样式|使用场景|
|:--|:--|:--|
|**下拉菜单**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1ThHdYlAgTGt2eh3kbnrDyycVaNDGzo8t =200x)|- 适用于通用场景。|

## 使用用法

1. 下拉按钮遵循GP-Button-下拉按钮规范，也支持用单个icon或Link Button作为下拉按钮。
2. 下拉菜单弹出位置会根据触发项所处页面位置而变。
3. 点击菜单选项后，收起下拉菜单，执行相应的命令。


### 1. 元素位置关系
:::: row
::: col :span="5"


**【使用规则】** 如右，下拉菜单支持4个弹出位置，下拉菜单弹出位置会根据下拉按钮所处页面位置而变：

- 默认情况下，下拉菜单位于下拉按钮下方，与下拉按钮左对齐；
- 当下拉按钮靠近页面右侧边缘时，下拉菜单与下拉按钮右对齐；
- 当触发项靠近页面底部边缘时，下拉菜单位于下拉按钮上方。

 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1qNz90g9YrM0O5O20Wk09F85Gf8qMC6zs =100%x)
:::
::::
<br>

### 2. 触发方式

#### 2.1 Hover

**【使用规则】**

- 出现规则：鼠标Hover下拉按钮时，弹出下拉菜单。
- 消失规则：鼠标离开下拉菜单，下拉菜单收起。
- 适用于大部分场景。

#### 2.2 Click

**【使用规则】**

- 出现规则：鼠标点击下拉按钮后，弹出下拉菜单。
- 消失规则：鼠标点击下拉菜单或者页面其他区域，下拉菜单收起。
- 适用于下拉操作低频的场景。



### 3. 常规下拉菜单
:::: row
::: col :span="5"


**【使用规则】**

- 下拉按钮遵循GP-Button-下拉按钮规范，也支持用单个icon或Link Button作为下拉按钮。
- 当下拉菜单处于展开状态时，下拉按钮保持触发状态（Hover或Press）；
- 点击菜单选项后，收起下拉菜单，执行相应的命令。


 :::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1liOhMTxK1RS2841knKmtexLTxWq6d4MN =100%x)
:::
::::

## 视觉样式

### 1. 尺寸

- 下拉菜单宽度以最长的菜单选项长度计算；
- 单行菜单选项高度为32px；
- 下拉菜单与下拉按钮上下间隔4px。

:::: row
::: col :span="4"
#### 1.1 常规下拉菜单
- 通用；
:::

::: col :span="4"
#### 1.2 菜单选项热区
- 单行菜单选项热区高度为32px，宽度为下拉菜单宽度；
:::

::: col :span="4"
#### 1.3 最小宽度
- 下拉菜单最小宽度为下拉按钮的宽度；
:::
::::

:::: row
::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1oIpL2jGx4WJu4-lxCS65D6qacvC0Is0f =100%x)
:::

::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=133sObIRUbw7fnmQR8g5H3kKHj3-4VRCt =100%x)
:::

::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1h9nA-3C3pUe_sgQmZB4WX7IQShs-evOX =100%x)
:::
::::

#### 1.4 最大宽度（折行）

- 下拉菜单最大宽度为440px, 若选项长度超过最大宽度，则对该项进行换行（如实际场景有需要，可由业务前端修改调整最大宽度）。

![123](https://drive.google.com/thumbnail?sz=w3000&id=1tIFIic030e5En1KYhEZVhAP5lijNOyBU =100%x)

### 2. 基本样式

| 状态 |展示样式|元件属性|
|:--|:--|:--|
|**Normal**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1V1noW7FQU5IZNjtVTK6awq7Bl-GdfJ6A =150x)|background: #FFFFFF；<br>box-shadow: 0 6px 16px 0 #000000 12%；<br>border-radius:  4px；<br>font-size: 14px; <br>color: #333333; |
|**Hover**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1XCdmGp0KcA51B345EShPnlTWZgyltonY =150x)|background: #FFFFFF；<br>box-shadow: 0 6px 16px 0 #000000 12%；<br>border-radius:  4px；<br>font-size: 14px;<br> color: #333333; <br>遮罩颜色：#000000 4%|
|**Disabled**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1b96mHInnCs1MXE4JN84-EwGqexc1jev4 =150x)|基于Normal整体opacity: 0.5|

## 场景示例

![123](https://drive.google.com/thumbnail?sz=w3000&id=1jA8i_LoUQyqBDW4xRzf1__GUXVDuZ6Os =100%x)
