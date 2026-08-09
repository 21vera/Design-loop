---
title: Keyboard Interaction Rules 键盘交互规则
description: 键盘是为了帮助用户高效地访问平台的所有功能，而无需将其双手抬离键盘。旨在响应键盘输入时获得全面、一致的体验
designer: Rokin Qiu
tabs:
  - title: 设计文档
    href: /zh/design/keyboard
  - title: 更新记录
    href: /zh/design/keyboard/records
---

## 使用用法 


### 1. 键盘操作
常用键盘按钮包括Tab键、上/下/左/右键、空格键、Enter键、Home/End键、向下/向上翻页键等。

| 常用键盘按钮 | 使用规则 | 示例 |
| :--  | :-- | :-- |
| <img width=100/>**Tab键** | - 将可操作项识别为焦点，并且导航顺序符合逻辑且可预测；<br />- 所有的交互式控件都应该作为焦点，非交互式控件（如tag）则不需要；<br />- 根据布局、视觉、逻辑等顺序定义tab键顺序，具体情况据业务场景而定；<br />- 初始焦点一般设置为当前页面最有可能点击的第一个（或主要）操作的可交互元素上；<br />- 最好不要设置可能会带来负面结果的目标元素作为初始焦点，如“删除”、“否”等。 | ![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1BO23SVm37HBcyffcae6vv_zZiwFJ1WLz =500x) |
| **向上/向下/<br />向左/向右键** | - 若目标位于单列中，则使用向上/向下箭头键导航；<br />- 若目标位于单行中，则使用向右/向左箭头键导航；<br />- 若目标位于多个列中，则使用所有 4 个箭头键导航；<br />- 使用方向键时，只对一个窗口/页面产生作用；<br />- 在多个列中，与tab键一起使用，可以更快速地在所有目标中进行切换。 | ![1_2](https://drive.google.com/thumbnail?sz=w3000&id=1brqYbfSCAX9qcEh0CawM1S2d7S_L3ij_ =500x) |
| **空格键** | - 在文本输入模式下，按下一次空格键，将出现一个字符的空白占位；<br />- 在非文本输入模式下，空格键的作用为“滑动到下一屏”，与pagedown键相同。 | ![1_3](https://drive.google.com/thumbnail?sz=w3000&id=1dve2SyGwqOKqq9_Gz-0EdsGwS1fAs_j2 =500x) |
| **Enter键** | 可执行多种常见的交互，具体取决于具有焦点或者与焦点相关联的控件：<br />- 若为命令控件，如按钮、url链等，则执行该按钮或链接的操作；<br />- 若为显示控件，如时间选择器，则执行打开/关闭该控件的操作；<br />- 若为其他控件，则根据业务执行符合用户习惯的操作。 | ![1_4](https://drive.google.com/thumbnail?sz=w3000&id=1peGrydxKPCByRRL31Od2R8oBVPvTsjGg =500x) |
| **ESC键** | - 让用户退出当前操作状态，如退出一个弹窗、激活的输入框失焦等。 | ![1_5](https://drive.google.com/thumbnail?sz=w3000&id=1styRbQ4iPp7qPm6gWZ5_0TjylH4q1gjj =500x) |
| **Home/End键** | - 可以将页面/活动区域滚动到开头或结尾；<br />- 活动区域内无列表或网格等控件时，Home键用于滚动至区域的顶部，End 键用于滚动至区域的底部（焦点不改变）；<br />- 在列表或网格选择控件中且有焦点时，Home键用于将焦点移至第一个元素并将其滚动至元素所在区域，End键用于将焦点移至最后一个元素并将其滚动至元素所在区域。 | ![1_6](https://drive.google.com/thumbnail?sz=w3000&id=1fFZU0azkhofCGIA4Z1OBUHYVEXxBTNZH =500x) |
| **向上/向下<br />翻页键** | - 翻页键让用户可以按照视区高度滚动页面；<br />- 向上翻页键用于按“页”（通常为视区高度）向上滚动区域直至区域顶部。向下翻页键用于按页向下滚动区域直至区域底部。 | ![1_7](https://drive.google.com/thumbnail?sz=w3000&id=1C8VBxcVd-CNWA-zQ69eQM8Z6bPJJ1ExH =500x) |
<br />

### 2. 快捷操作方式
| 类型 | 使用规则 | 示例 |
| :--  | :-- | :-- |
| **常用快捷方式**  | 全选<br />连续选择<br />保存<br />	查找<br />打印	<br />复制<br />剪切<br />粘帖<br />撤销<br />下一个选项卡<br />关闭选项卡<br />语义式缩放<br />恢复上一步操作 | Ctrl+A<br />Shift+箭头键<br />Ctrl+S<br />Ctrl+F<br />Ctrl+P<br />Ctrl+C<br />Ctrl+X<br />Ctrl+V<br />Ctrl+Z<br />Ctrl+Tab<br />Ctrl+F4 或 Ctrl+W<br />Ctrl++ 或 Ctrl+-<br />Ctrl + Y |
| **其他快捷方式** | 重命名项<br />删除所选项<br />Bold<br />Underline<br />刷新<br />缩放到默认视图<br />关闭	|F2<br />Del、Ctrl+D<br />Ctrl + B<br />Ctrl + U<br />F5 或 Ctrl + R<br />Ctrl + 0<br />Ctrl + W|



