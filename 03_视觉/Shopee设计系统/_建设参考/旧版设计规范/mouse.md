---
title: Mouse Interaction Rules 鼠标交互规则
description: 鼠标是PC端人机交互最主要的方式，它提供一种激活界面元素并使用流畅、直观的指针来补充键盘输入动作
designer: Rokin Qiu
tabs:
  - title: 设计文档
    href: /zh/design/mouse
  - title: 更新记录
    href: /zh/design/mouse/records
---

## 使用用法 


### 1. 动作

| 操作 | 交互操作 | 适用场景 |
| :--  | :-- | :-- |
| <div style="width:100">**悬停**</div> | 鼠标移入目标元素 | - 为目标元素显示更详细的信息或指导性内容，无需提交操作，如工具提示、信息提示、操作提示等；|
| **单击** | 按下鼠标左键然后松开，不移动鼠标 | - 选择激活一个目标元素，并响应该元素的主操作，如跳转页面、弹出菜单等； |
| **单击并按住** | 按下鼠标左键，不松开 | - 通常伴随移动鼠标，动态选择页面元素，如选择一段文字； |
| **右键单击** | 按下⿏标右键然后松开，但不移动⿏标 | - 使用全局命令，或与选定目标元素关联的应用栏（浏览器中不建议自定义）； |
| **双击** | 连续两次快速按下然后松开鼠标左键，但不移动鼠标 | - 第一次点击作为选择，第二次点击作为确认时（浏览器页面中不建议使用该动作）； |
| **滚动** | 滚动鼠标滚轮，或单击并按住滚动条滑动 | - 窗口或指定区域内进行向上、向下、向左、向右的移动，如浏览页面上下文、查看下一页/上一页等； |
| **拖动** | 单击并按住鼠标左/中键，然后移动对象 | - 可拖动窗口/图标/图片等，如图片编辑器中的拖动图片； |
| **拖放** | 单击并按住鼠标左/中键，然后移动对象后在目标位置放下 | - 拖动窗口/图片/图标等，松开鼠标键后，将对象放在新位置上，如拖入文件后直接上传。 |
<br />

### 2. 指针操作
| 操作 | 交互操作 | 适用场景 | 使用场景|
| :--  | :-- | :-- | :-- |
|![test](https://drive.google.com/thumbnail?sz=w3000&id=1C7MFOqLrHBnC76NlHdn2S8ZIuSYoJJ8k =24x)  | **箭头** | ⽤于选择内容和界⾯元素并与之交互的标准指针 | - 通用； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1cqmmQOHBlIBaH5erW8iLGuKahFPf2OSZ =24x)   | **抓⼿** | 拖动以重新定位视图中内容的显示位置 | - 使用拖动操作，鼠标按下时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1oZ3lHgmJrcPPLovFudra2E0dH3LCz1zy =24x)   | **张⼿** | 可以拖动以在视图中重新定位内容 | - 使用拖动操作，鼠标松开时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=15LZQn7ZvfLEcDCyl7wAUWnqI9zvqaX62 =24x)   | **⼗字准线** | 可以进⾏精确的定位 | - 使用预览功能或截图时（本平台暂无场景）； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=11_02-CyZHaCwMXES9zpWXLeq5gboe3Hu =24x)   | **不可操作** | 拖动的项⽬不能放置在当前位置 | - 拖入的文件格式不匹配时;<br />- 包含交互操作的文字链、按钮等不可操作时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=15LgyFWXvuyGc6t6z2ut2lDk-rZxh6Pg4 =28x)   | **新增副本** | 当拖放到⽬标中时，复制已拖动单位移动的项⽬ | - 直接复制目标元素的副本，通常结合键盘使用才会出现； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1A7BNqYwUtcH_Xc6a8WEgBnRzIy7J0AgA =24x)   | **指向** | 指针下⾯的内容是指向⽹⻚，⽂档或者其他项⽬的url链接 | - 指向一个可交互的元素时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1DLsDWrrzZcgLmBO-1-NbFrfOops8sDya =24x)   | **左右调整⼤⼩** | 在水平方向上，调整可改变窗口内活动区域的范围和⼤⼩，或向左/向右移动 | - 窗口大小有限的情况下，需调整垂直布局满足当前场景需求，如调整左侧边栏宽度； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1qvCHTZ9kRMN1edo_WdzL_qQ2e3ZPP9SJ =24x)   | **向左调整⼤⼩** | 在水平方向上，调整可改变窗口内活动区域的范围和⼤⼩，或向右移动 | - 无法向左调整或向左调整达到极限时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1Yq5Sw9H9T5jQi1bvnzzEGlyDWqYEL1nS =24x)   | **向右调整⼤⼩** |  在水平方向上，调整可改变窗口内活动区域的范围和⼤⼩，或向左移动  | - 无法向右调整或向右调整达到极限时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1OgL5An3XUwDDojgRFpN2gdQNQRynlGs7 =24x)   | **调整⼤⼩** | 在垂直方向上，调整可改变窗口内活动区域的范围和⼤⼩，或向上/向下移动 | - 窗口大小有限的情况下，需调整横向布局满足当前场景需求，如调整左侧边栏宽度； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1mWpH8zbt1u7JMjqzlPf3fg6fi9RKjwiz =24x)   | **向上调整⼤⼩** | 在垂直方向上，调整可改变窗口内活动区域的范围和⼤⼩，或向上移动 | - 无法向下调整或向下调整达到极限时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1viJAz0uPs1gHdYIXQnEoTfzFaDjhgAC9 =24x)   | **向下调整⼤⼩** | 在垂直方向上，调整可改变窗口内活动区域的范围和⼤⼩，或向下移动 | - 无法向上调整或向上调整达到极限时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=12FdeIrjXLtjYWHe6nNUdyQ24Sk17sv8k =24x)   | **水平缩放大小** | 水平方向上调整窗口或元素的大小或范围 | - 目标窗口的大小和范围可调整时，如改变活动窗口大小、图片裁剪等； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1pxTbi2GHeVgfEyQCiqeoYU9FxK8QsfZw =24x)   | **斜向缩放大小** | 左上/右下方向上调整窗口或元素的大小或范围 | - 目标窗口的大小和范围可调整时，如改变活动窗口大小、图片裁剪等； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1JJtpT3i0_vWk2pbsdszgYRsmTVE_ewUG =24x)   | **斜向缩放大小** | 左下/右上方向上调整窗口或元素的大小或范围 | - 目标窗口的大小和范围可调整时，如改变活动窗口大小、图片裁剪等； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1oXjCTfIf-Uhc7pYaSShPl8HRk4g_SE3U =24x)   | **垂直缩放大小** | 垂直方向上调整窗口或元素的大小或范围 | - 目标窗口的大小和范围可调整时，如改变活动窗口大小、图片裁剪等； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1LcfU6NBcVeHOJUEElJw_jPEX2yoddDG9 =24x)   | **⽔平输⼊⽂字** | 在⽔平布局中，对可选择文本使用该光标，可以选择和插⼊⽂本 | - 横向文本输入框中获取光标时； |
| ![test](https://drive.google.com/thumbnail?sz=w3000&id=1a8-lchmwNeyhUiRW9OkBcAGcAKQ2HImA =24x)   | **垂直输⼊⽂字** | 在垂直布局中可以选择和插⼊⽂本 | - 纵向文本输入框中获取光标时。 |



