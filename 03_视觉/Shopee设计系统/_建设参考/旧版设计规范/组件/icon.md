---
extend: /zh/components/icon
---

## 设计规范
### 1. 图标栅格
图标默认以 **16x16** 的画板创建，并在其中 **14x14** 的区域内进行图标绘制。
<br /><br />

![test](https://drive.google.com/thumbnail?sz=w3000&id=1IBa4t6nNUhJ_pcCKuNlHxiV_oTKPhd0q =50%x)
### 2. 基本形状
使用以下的基本形状进行图标绘制，尽可能确保单个图标在与整个图标库中保持视觉平衡。
<br />

![test](https://drive.google.com/thumbnail?sz=w3000&id=1Lv89Wb3OjozdcfR9oh-pXuB4aPVRsLCM =70%x)
### 3. 尺寸汇总
- 图标默认为 16px，在设计中如需进行其它尺寸的定义，可基于默认尺寸进行图标缩放。
- 图标可缩放尺寸有：**Small (Normal)**: 16px；**Medium:** 24px；**Large**: 32px；**X-large**: 48px。

## 样式设计原则
### 1. 填充与线性型的选择
平台允许填充型与线性型的图标，根据不同业务设计需求选择使用即可。
|类型|说明|示例|
|:--|:--|:--|
|<div style="width:120px">**1px 线性型图标**</div>|默认情况下使用 1px 粗细的宽度。|![test](https://drive.google.com/thumbnail?sz=w3000&id=1aCvSgA8lAbQVmEqojs4mmhiK3lykU32_ =300x)|
|**1.5px 线性型图标**|当按钮文字 font-weight: 500/600/700 时，对应 icon 为 1.5px 粗细。|![test](https://drive.google.com/thumbnail?sz=w3000&id=1iZ3bv7TIg1Qp2dSjKSs5FVxnLrBBHlLV =300x)|
|**填充型图标**|适用于场景下对于「状态」的展示。|![test](https://drive.google.com/thumbnail?sz=w3000&id=19Ng74igJMeBNXAN606IFdG9cbkO314J8 =300x)|

:::: row
:::col :span="6"
### 2. 使用 1 px 圆角
尽可能用 1px 圆角，而非全直角。
:::
:::col :span="6"
### 3. 尽可能少锚点
以最少的锚点达到想要的造型，这样可一定程度减少 SVG 的代码，更简洁。
:::
::::
:::: row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1SlyP_Ro0xmgUjmXtbjpGvEnCPvo7092X =100%x)
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1Dr2xGd5Ua2bo4NcJoDw7t3yhDmy9zJZm =100%x)
:::
::::
## 输出规范
### 1. 命名规则
- 默认情况下图标的基本名称为功能的英文；
- 当图标为填充型，则以「-s」后缀。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1wqCS-l6WkWdB-YDL-vjuNoiutS2w4-_M =100%x)
### 2. SVG 导出
- 步骤1. 确保 Sketch 安装了 SVGO Compressor 插件（该插件为后台插件，压缩 SVG，只保留对前端必要的代码部分）；
- 步骤2. 选择设计好的 icon 图层使用轮廓化 (Convert to outlines)功能，将 icon 转换为填充图形；
- 步骤3. 选择所有 图层后使用联集（Union）合并为 1 个图层；
- 步骤4. 选择合并好的图层，使用路径合并 (Flatten) 功能简化图层的复杂性；
- 步骤5. icon 其颜色设置为 #000000； 
- 步骤6. 以 16* 16 的方式导出 SVG。
<br /><br />

#### 2.1 导出对比
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1cfjo_5s8ooJMvnfylnjCThbHRxzP3gjk =100%x)
【错误方式】
- 图层样式复杂，其中「Oval」图层为描边图层，影响 SVG 在前端页面的渲染效果；
- 多个图层，增加 SVG 体积；
- icon 颜色不是 #000000，影响前端对颜色的控制。
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1IIIwL_8pMh_EZMQChVDwHeyEyEiKLatU =100%x)
【正确方式】
- 使用轮廓转换 (convert to outlines)将「Oval」图层转换为轮廓化图形；
- 通过联集联机合并为 1 个图层；
- icon 颜色为 #000000。
:::
::::
<br />

### 3. 关于 SVG 的扩展阅读
#### 3.1 SVG 结构
以下代码为 SVG 最精简的结构内容。

![test](https://drive.google.com/thumbnail?sz=w3000&id=1OLS_MMvuL1MGSrWD99YIaE3EufRzfk0z =100%x)
#### 3.2 未压缩与已压缩的对比
::::row
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=112hGSYHZfS3WrVflFyBlkONBwNtjpEVY =100%x)
【未压缩的 SVG】大小为 1,094 字节；并且存在大量与前端渲染无用的代码。
:::
:::col :span="6"
![test](https://drive.google.com/thumbnail?sz=w3000&id=1FRG2wW8EP4kQEHhyKb--_QrJFx_oveX3 =100%x)
【已压缩的 SVG（使用 SVGO Compressor 插件）】大小为 770 字节，减少近 30% 的体积；清除多余代码，只保留对前端必要的代码部分。
:::
::::
