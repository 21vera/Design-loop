---
extend: /zh/components/sidebar
---
## 组件元素 
<br />

:::: row
::: col :span="4"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Cs-xqA_0_-4Nq0ARzkp5J5ITbS7sbKr- =100%x)
:::
::: col :span="8"
<br /><br />

1. **表**：指装载侧边栏内容的容器。
2. **导航项**：导航层级内容。
:::
::::

## 类型汇总 
| 名称 | 组件类型 | 使用场景 |
| :--  | :-- | :-- |
| **基础侧边栏** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1SDOveMMTE9Mln9RMJIlktn7ysXXgngNo =157x) | - 用于只存在一个层级内容的侧边导航，一般置于内容容器的左方，或者主导航的左下方。 |
| **带层级关系的侧边栏** | ![test](https://drive.google.com/thumbnail?sz=w3000&id=1NbQXllbEmjnBDApSBmIzjGYnotzAMOMv =174x) | - 适用于具有层级关系的情况下，一般置于内容容器的左方，或者主导航的左下方。 |

## 使用用法 
适用于存在层级关系或分类关系的场景。

### 1. 基础侧边栏
:::: row
::: col :span="6"
- 位于内容容器的左方，或主导航的左下方；
- 导航项完整展示，过长可折行；
- 若侧边导航作为主导航且无首页，则默认选中侧边导航第一个导航项；点击导航项，直接刷新/跳转该导航内容的页面。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1nHUWfxuic5ANH-K8VW64V2uQR-h3hxgJ =100%x)
:::
::::

### 2. 带层级关系的侧边栏
:::: row 
::: col :span="6"
- 当子层级数量不过4个时，直接展开所有导航项；
- 当子层级数量超过4个时，提供收起按钮，点击后，收起该导航项下的所有子层级，导航项之间的展开/收起不互斥；
- 其他用法同基础侧边栏。
:::
::: col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1bJ2wspEl5ZZK4DDvJPETPhavlyzWNDjW =100%x)
:::
::::


## 视觉样式
- 最大字符宽度148px, 超出宽度则换行；

:::: row 
::: col :span="6"
### 1. 基础侧边栏
- Normal：**font-size**: 14px；**color**: #333333；
- Hover ：**font-size**: 14px；**color**: #EE4D2D；
- Selected：**font-size**: 14px；**color**: #EE4D2D 字重：600；
- 类别：与Normal状态一致；
- 结构：Margin left + Text + Margin right 整体宽度不超出220px。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1noOsSaxP8uBrknr3D-GvBzEbByz6TbyJ =100%x)
:::
::: col :span="6"
###  2. 带层级关系的侧边栏
- Normal：**font-size**: 13px；**color**: #333333；
- Hover ：**font-size**: 13px；**color**: #EE4D2D；
- Selected：**font-size**: 13px；**color**: #EE4D2D 字重：600；
- 类别：**font-size**: 14px；**color**: #B7B7B7；
- 结构：Margin left + Icon+ Text + Margin right 宽度不超出220px 

![test](https://drive.google.com/thumbnail?sz=w3000&id=10GoEdtQOzLGulQvisfNF9arwke_ukCXj =100%x)
:::


:::: row 
::: col :span="6"
### 3. 展开收起的带层级关系侧边栏
- Normal：**font-size**: 13px；**color**: #333333；
- Hover ：**font-size**: 13px；**color**: #EE4D2D；
- Selected：**font-size**: 13px；**color**: #EE4D2D 字重：600；
- 类别：**font-size**: 14px；**color**: #B7B7B7；
- 结构：Margin left + Icon+ Text + Margin right 宽度不超出220px。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1n-mSMjvQrHX0tTgMbjWNIo4Wh-2s3-fH =100%x)
:::
::::

## 场景示例 
### 1. 带图标的侧边栏
适用于层级内容具有分类关系或者具有二级层级关系，一般置于内容容器的左方，或者主导航的左下方。

![test](https://drive.google.com/thumbnail?sz=w3000&id=118grDxBTvaaQb2wntV7hRahd-LYfUQC0 =100%x)

### 2. 展开收起的层级关系侧边栏
 于层级内容具有层级关系的情况下，一般置于内容容器的左方，或者主导航的左下方。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1cCFliwMd0rLiMER6GkTWPv6JvkRWrx4i =100%x)
    