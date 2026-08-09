---
extend: /zh/components/popover
---

## 组件元素
<br>

:::: row
::: col :span="5"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1U3REZwJanXTpIt1tEUmarV9F99sYno7M =100%x)
:::
::: col :span="1"
<br />
:::
::: col :span="6"

1. **容器**: 承载标签内容的图形元素;
2. **文案**: 对象的属性、类别或状态描述;
3. **图标(可选)**: 增加标签视觉表现的图标；

:::
::::

## 类型汇总

|名称|基础样式|使用场景|
|:--|:--|:--|
|**常规气泡框**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1AVrGz-v2rwSvmblftkyag6fqmpGPVX55 =180x)|- 需要对目标元素有进一步解释，或引导用户查看更多信息；<br>- 如目标元素的使用方法或说明提示。|
|**嵌套操作气泡框**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1U9YOLX7tXfQJjjzPyYNNwDquiyR1YRQB =320x)|- 需要用户进一步操作时使用。|
|**带图片的气泡框**|![123](https://drive.google.com/thumbnail?sz=w3000&id=19LtcVYSJ9KebpXYgZtMl5bHViC335jka =320x)|- 需要图示说明时使用。|

## 使用用法
### 1.常规气泡框
:::: row
::: col :span="4"

**【使用规则】**

- 出现：hover或点击目标元素后出现；
- 位置：默认出现在目标元素上方；
- 关系：始终跟随目标元素，不随页面滚动而与目标元素分离；
- 消失：鼠标点击Popover区域外任一处或再次点击目标元素时消失。

:::
::: col :span="8"
![123](https://drive.google.com/thumbnail?sz=w3000&id=13XTF1oFCioR5URitp0Ned4TuYNjzCspd =100%x)
:::
::::

### 2.嵌套操作气泡框
:::: row
::: col :span="4"
**【使用规则】**

- 出现：点击目标元素出现；
- 位置：默认出现在目标元素上方；
- 消失：用户进一步操作，页面给出对应反馈后消失，鼠标点击Popover区域外任一处或再次点击目标元素时消失。

:::
::: col :span="8"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1jtEvoNC_qXGcoxv3fNifc0y2vN6bnTfN =100%x)
:::
::::

### 3.不同方向气泡框
:::: row
::: col :span="4"
**【使用规则】**

- 位置：气泡框箭头有 12 个方向，箭头默认位置为Top；
- 建议：根据目标元素与其他界面元素的关系来确定位置，尽量不遮挡其他界面元素。

 :::
::: col :span="8"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1LDYA0b0ZAE6fgSvZ663lHJYWJyr-wHOr =100%x)

:::
::::

## 视觉样式
### 尺寸
- 默认两端预留16px，最大宽度320px；

![123](https://drive.google.com/thumbnail?sz=w3000&id=1Px3WT5-besz3Eebp3luwNPOmTThxs5LD =100%x)

## 基础样式

|名称|基础样式|元件属性|
|:--|:--|:--|
|**Normal**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1AVrGz-v2rwSvmblftkyag6fqmpGPVX55 =180x)|background: #FFFFFF；<br>box shadow：0.6px 16px #000000 0.12；<br>font-size: 14px，#333333；|
|**Normal**|![123](https://drive.google.com/thumbnail?sz=w3000&id=19LtcVYSJ9KebpXYgZtMl5bHViC335jka =320x)|background: #FFFFFF；<br>box shadow：0.6px 16px #000000 0.12；<br>title-font-family: Roboto-Medium，16px，#333333，center;<br>body-font-family: 14px，#666666，center;|

## 场景示例
页面滑动时，当目标元素与页面顶部的距离：小于Popover的高度时，Popover实时切换至目标元素下方展示；大于Popover的高度时，Popover返回默认位置，如下图。

![123](https://drive.google.com/thumbnail?sz=w3000&id=1aAth2_Gm2S2XUr5UcuIANig4pe26Z4Dx =100%x)