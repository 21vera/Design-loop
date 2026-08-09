---
title: Motion Rules 动效规则
description: 动效是自然高效且有意义的
designer: Ying Yi
tabs:
  - title: 设计文档
    href: /zh/design/motion
  - title: 更新记录
    href: /zh/design/motion/records
---

## 原则
设计师必须做有意义的动效，是带有目的性且助力交互体验，动画易用性的优先级要高于增加设计创意形式，不去做太多的修饰动画增加阅读难度。
## 时间
持续时间正确组合会产生流畅而清晰的过渡。最快时间: 100ms, 基本时间: 200ms, 较大时间：400ms.以100 的倍增方式。
<br /><br />

![test](https://drive.google.com/thumbnail?sz=w3000&id=1ke77di5aW62hRI4SwhR5jXoXa_pIU89Q =80%x)
## 缓动
速度的快或慢取决于时间与缓动，相同的距离，时间越短速度则越快，而缓动则是能将同一段时间划分快与慢的区域，时效事件发生时，元素的行为应与用户预期相符。
:::: row
::: col :span="4"
### 1. 缓出
交互性操作时尽量使用out类公式，这类公式初始速度快，会有效反馈用户操作，公式代码：bezier(0; 0; 0.58; 1)
:::
::: col :span="4"
### 2. 缓入
通常元素飞入时用减速运动，飞出时用加速运动，通常这类公式使用于组件渐隐或消失，公式
代码：bezier(0.42; 0; 1; 1)
:::
::: col :span="4"
### 3. 缓入缓出
先快后慢，两端速度都趋近0，过程中达到最大值，公式比较适用于组件展开收起类可视范围内点到点之间的运动，公式代码：bezier(0.42; 0; 0.58; 1)
:::
::::
:::: row
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1fZH3TMAVZcsHqy9_VPUrxqVLquYIHg2N =100%x)
:::
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1qoO0bgLzkDNW2TGdAmV9hm8_EHJekBwt =100%x)
:::
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1geQ7pMeB_mVoayeKdIQ-P4f3XVZ4xcGZ =100%x)
:::
::::
## 过渡
适当的加入一些过渡效果，能让界面保持生动，同时也能增强用户和界面的沟通。
## 使用方法
适当的加入一些过渡效果，能让界面保持生动，同时也能增强用户和界面的沟通。
### 1. 表单加载过渡
- 表单内容加载，应当适用加载过渡动效；
- 缓动：使用easyinout,bezier(0.42; 0; 0.58; 1) 持续时间300ms;

![test](https://drive.google.com/thumbnail?sz=w3000&id=1vhdJPKof3FXYjyPOoUaa_SySkXieKYmE =100%x)
### 2. 表单信息新增
- 表单内容新增时，应当使用加载过渡动效；
- 缓动：使用easyinout,bezier(0.42; 0; 0.58; 1) 持续时间300ms;

<br />

![test](https://drive.google.com/thumbnail?sz=w3000&id=1dgxq9yktzNb-L1YKlCobs8g4YYHvdENZ =100%x)
### 3. 选项框动画
- 选项框动画持续的动画时间是最快的；
- 缓动：使用easyout,bezier(0; 0; 0.58; 1)持续时间100ms。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1jIf4Vk46g6JSUDjpKqaH6ezqRMCLCOQ_ =100%x)
### 4. 下拉选择
- 下拉选择类动画持续时间为默认持续时长；
- 缓动：使用easyinout,bezier(0.42; 0; 0.58; 1) 持续时间200ms。

<br />

![test](https://drive.google.com/thumbnail?sz=w3000&id=1PLHjegSxaegy7rhygqcwzkNpLC3726t_ =100%x)
### 5. 页面弹窗
- 弹窗动画需要较长的持续时间；
- 进场：从下往上渐显，缓动使用easyin,bezier(0.42; 0; 1; 1) 持续时间300ms；
- 关闭：往上渐隐消失，缓动使用easyinout,bezier(0.42; 0; 0.58; 1) 持续时间200ms。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1-Ni02Fh3Qj4OyHQV7m-nnnlrHc_pZwQO =100%x)