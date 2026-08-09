---
extend: /zh/components/progress
---

## 组件元素
<br>

:::: row
::: col :span="6"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1uZ8hRnS3QLloIrzPnW7-dOCud11spvKD =90%x)
 :::
::: col :span="6"

1. **进度条:** 动态实时变化，展示当前加载的过程。
2. **进度轨道**：一般为线性形状或环形，承载进度的容器。
3. **数字提示/状态标识**：现实进度过程的数字或百分比，成功或失败的展示。

:::
::::

## 类型汇总

|名称|基础样式|使用场景|
|:--|:--|:--|
|<div style="width:140px">**百分比**</div>|![123](https://drive.google.com/thumbnail?sz=w3000&id=1hJU2LxK8hAugjchj_fpY-tqUdciKJdfK =440x)|- 适用于进度条的状态随时间从0%向100%正向变化。|
|**比例数值**|![123](https://drive.google.com/thumbnail?sz=w3000&id=18j1SVr4Qmkg6vFnYBlNJEK6Wpj3qvW_U =440x)|- 适用于进度条的状态随时间按百分比正向变化。|
|**辅助文字**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1dOvzRao_NaAr-KcMUHMT82VCeW3_jv8Z =440x)|- 当目标元素的表意不够明确，或因空间有限内容无法展示完整时使用。|
|**加载失败**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1MA68wpdz1zofgszJaidzwtQzOPm0dwQ0 =440x)|- 适用于进度条加载失败后。|

## 使用用法

1. 场景：适用于可以检测到活动时长和进度的操作场景。
2. 触发方式：
	- 适用于操作需要较长时间才能完成时，为用户显示该操作的当前进度和状态，如上传、下载等场景；
	- 适用于当一个操作会打断当前界面，或者需要在后台运行，且耗时可能超过 2 秒时等场景。


### 进度条


:::: row
::: col :span="6"

**【位置】**
- 页面级别的进度条出现在页面正中央；
- 组件级别的进度条位于组件内中间位置；
- 在列表中的进度条位于行最右侧。

**【使用规则】**
- 交互规则：通过沿固定的可见轨道长度设置指示器的动画来显示进度；
- 交互规则：显示的状态信息必须准确，如一个100秒钟的任务，1%的进度为1秒；
- 消失规则：当进度完成后，该进度条消失，在进度条原位展示操作后的状态反馈，如“完成”、“成功”、“失败”、“重试”等。

**【异常流】**
- 状态信息可根据具体场景自定义展示百分比/数值/文案，也可不出现；
- 在上传/下载场景中，需提供给用户取消或暂停上传/下载的操作，具体功能视当前场景而定。
 :::
::: col :span="6"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1syCwMti37-AtQn-mDUjBYRY7LKXfcIJD =100%x)
:::
::::

## 视觉样式
### 尺寸
- 进度条宽度默认按当前页面内容100%确定宽度，若无法满足，可按此宽度：大尺寸=480px；小尺寸=240px。<br>

:::: row
::: col :span="6"

![123](https://drive.google.com/thumbnail?sz=w3000&id=1cQ-ui8GuC9_sppFe93uR4GH0xkIHJ6eq =100%x)
 :::
::: col :span="6"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1xn-E0tOqkwXWQ2kPWaLh-LB_X5jESjnl =100%x)
:::
::::

## 基本样式

|名称|基础样式|使用场景|
|:--|:--|:--|
|**Normal**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1hJU2LxK8hAugjchj_fpY-tqUdciKJdfK =440x)|Label_front:（Normal/Small）14px，#999999；<br>background: #F6F6F6；<br>progress: #55CC77；|
|**Failed**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1MA68wpdz1zofgszJaidzwtQzOPm0dwQ0 =440x)|background: #F6F6F6；<br>progress: #FF4742；|
<br>

## 其他标注

![123](https://drive.google.com/thumbnail?sz=w3000&id=1uguYJVHA8yZJuEwI4WlrWZu_wP_jGCgv =100%x)

## 场景示例
![123](https://drive.google.com/thumbnail?sz=w3000&id=1ggGwRPp6_Q4G0m7At3diSX4xbp3Nrb8V =100%x)


