---
extend: /zh/components/skeleton
---

## 组件元素
<br />

:::: row
::: col :span="6"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1MldVYdzejzF7gr_0oXQ-D5MltekEUPUR =90%x)
 :::
::: col :span="6"
<br />

1. **图片类占位图形**: 通常为正方形或固定比例的图形。
2. **文字类占位图形**：通常都为文字段落的占位。
:::
::::

## 类型汇总

|名称|基础样式|使用场景|
|:--|:--|:--|
|**文字类占位图形**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1vz11kOrzGanMWCNn-KS5IzSmqmVu_drP =448x)|- 用于第一次文字加载的场景。 |
|**方形图片占位图形形**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1R8cGXVKRKuc_a8VurhufUSZ0rrCnuVG7 =48x)|- 用于第一次方形图片加载的场景。 |
|**圆形图片占位图形**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1B3JRSF_3IEMFLiNbYJdBJiMze4ehPT5C =48x)|- 用于第一次圆形图片加载的场景。  |

## 使用用法
### 1. 骨架屏
:::: row
::: col :span="5"
【使用规则】
- 在网络较慢，需要长时间等待时，页面有内容区域出现该加载样式；
- 加载过程中伴随呼吸态动效；
- 当内容已加载完成时，skeleton消失，内容覆盖在原skeleton处。
:::
::: col :span="7"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1799YBa0fdhWpn8NrjT5L85L13jw7hIGe =100%x)

:::
::::
<br />

## 视觉样式
### 1. 尺寸
- **background**：#F6F6F6；
- 长矩形、正方形、圆形为基础元素，可以自由组合。
<br />

:::: row
::: col :span="4"
#### 1.1 文字类占位图形
- 文字类条形占位图形为一长一短组合形态，短边长度为长边的80%；
- 文字类占位图形2条为一组；
- 文字类和表格组合一般不会超过两组。
:::

::: col :span="4"
#### 1.2 方形图片占位图形
- **border-radius**: 2px；
- 默认大小56px；
- 加载过程中伴随呼吸态动效。
:::

::: col :span="4"
#### 1.3 圆形图片占位图形
- 默认大小56px；
- 加载过程中伴随呼吸态动效。
:::
::::

:::: row
::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1s11YMnb3CK4oXJmlADTarTcEQxm6bTHO =100%x)
:::

::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=12e1-egBCbZ54HjFiVjj84xANcYbvhuXI =100%x)
:::

::: col :span="4"
![123](https://drive.google.com/thumbnail?sz=w3000&id=1xjURpCKS5X4eVR0ud1_-OByF0gScJIFO =100%x)
:::
::::
<br />

## 基本样式

|状态|展示样式|元件属性|
|:--|:--|:--|
|**Skeleton-1**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1bXmwXnIyFm9k5L1dSgAP1RNrzNwydU20 =448x)|**background**：#F6F6F6；<br />**border-radius**:  2px； |
|**Skeleton-2**|![123](https://drive.google.com/thumbnail?sz=w3000&id=18aGgwx2wVnN2QlgbUQdwrboMHvjSusax =448x)|**background**：#F6F6F6； |
|**Skeleton-3**|![123](https://drive.google.com/thumbnail?sz=w3000&id=1JY9v5tSf01A0DO_lv8tOvxkto3Qpe8rk =120x)|**background**：#F6F6F6；<br />**border-radius**:  2px；|

## 场景示例（可选）

目前骨架屏使用场景定义在表格、信息流、列表中使用。

![123](https://drive.google.com/thumbnail?sz=w3000&id=1MsWyySSU1BtfTRfhbzQSuYTTL66MwOfa =100%x)


