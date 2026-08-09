---
extend: /zh/components/breadcrumb
---

## 组件元素 
<br />

:::: row
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1amSKkshKC-5z2P972QME49J5rrcJrZTn =100%x)
:::
::: col :span="6"
1. **分隔符**：分隔每个路径的节点。
2. **节点**：
   - 上层页面：在浏览路径或者层级之前的页面；
   - 当前页面：当前用户选择与停留的页面。
:::
::::

## 类型汇总 
1. 基础面包屑，如果 ≤ 4层，则展示完整的面包屑（最多4个坑位）。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1CJy71M7FaVNKt4Uq9RaBGMey-0EhjBMU =100%x)

2. 多层级面包屑，如果超出4层则在第二个坑位省略，点击「 ··· 」展开省略层级。

![test](https://drive.google.com/thumbnail?sz=w3000&id=155mNjoX7jCr2OPLrdtv2ucfp9KS9XLWb =100%x)


## 使用用法 
一种辅助和补充的导航方式，适用于平台结构层级多的场景。

### 1. 基础面包屑
:::: row
::: col :span="6"

- 位于页面头部下方、内容区块上方；
- 点击上层坑位后切换页面，点击当前页面坑位不响应。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1XC5jdvjIZwLWLouppU0VJGX41Uvf8h_i =100%x)
:::
::::

### 2. 带层级关系的侧边栏
:::: row 
::: col :span="6"

- 若当前层级超过4层，则在第二坑位展示省略，第三、四坑位展示最后二个层级；
- 点击“···”展开省略层级，呈现选中态，再次点击“···”或该区块之外地方进行收起；
- 点击上层坑位后切换页面，点击当前页面坑位不响应。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1fbg9YaKF7c3vscw6lhHWtXHtgJd5m8QZ =100%x)
:::
::::


## 视觉样式
### 1. 基础面包屑
- 阴影：**background**：#FFFFFF；**box-shadow**：0 1px 4px 0 rgba(0,0,0,0.12)；
- Normal：**font-size**: 16px； **color**: #999999；
- Selected：**font-size**：16px；**color**：#333333；
- Hover：**color**：#333333。

![test](https://drive.google.com/thumbnail?sz=w3000&id=16uzDqsV7OnNZGJj-hQdiY0IuyuZNaxWR =100%x)

### 2. 多层级面包屑
- 省略符点击展开收起的面包屑,省略符字体粗细为中粗；
- 阴影：**background**：#FFFFFF；**box-shadow**：0 2px 6px 0 rgba(0,0,0,0.12)；**border-radius**：4px；
- Normal：**font-size**：16px；**color**：#999999；
- Selected：**font-size**：16px；**color**：#333333。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1KQVFI-SvNbUOIXq8df1AEQI1I-kbO_FI =100%x)


## 场景示例 #

![test](https://drive.google.com/thumbnail?sz=w3000&id=18jyZEBPKsWRscT6hNyJo6bQEcYUEMW2N =100%x)

