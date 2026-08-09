---
extend: /zh/components/upload
---
## 组件元素 
<br />

:::: row
::: col :span="6"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1jWYRryNi80LUb6dcHdvaqp2DWh8HKMLj =100%x)
:::
::: col :span="6"
1. **上传触发区域**：承载拖拽文件上传的区域。
2. **上传触发按钮**：点击触发文件选择的按钮。
3. **说明文案**（可选）：上传操作的文案说明。
4. **辅助文案**（可选）：辅助解释上传要求的说明。
5. **上传图标**（可选）：直观表达上传含义，辅助解释。
:::
::::

## 类型汇总 
| 名称 | 基础样式 | 使用场景 |
| :--  | :-- | :-- |
| **拖拽式上传** | ![2_1](https://drive.google.com/thumbnail?sz=w3000&id=11jD8JIvD8oyY_jx9uOCqlyyL6uOdLbNn =306x) | - 用于展示用户需要特别关注的重要功能、系统提示。 |
| **图片上传** | ![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1nuJeI6wstIwzoQZb4jA1MHGjk8JXMuf- =96x) | - 用于展示用户需要关注的重要功能、系统提示。 |

## 使用用法 
### 1.通用用法 
#### 1.1 上传触发行为 

【点选上传】点击上传触发区域，弹出系统文件选择弹窗，选择格式和大小正确的文件后(大小和格式不符的文件为禁选状态)，自动退出文件选择，开始内容上传；
【拖拽上传】将格式/大小/数量正确的文件拖拽至上传控件框中，开始内容上传。

![3_1](https://drive.google.com/thumbnail?sz=w3000&id=1L_Gz5y5vaubADNPt8snS0BdawmHHKfRW =100%x)


#### 1.2 上传结果反馈
【使用规则】
- 形式：可根据业务需要选择Toast或Modal展示反馈结果，若需提供结果说明文案及操作按钮时可使用Modal；
- 类型：上传成功 、 上传失败、上传部分成功。


【异常流】
-文件出错：当「上传文件损坏」或「上传对象出错」时，需要弹出报错信息，提示上传对象异常；
-上传失败：在上传过程中，发生网络异常、后台卡顿等问题，导致此次上传行为阻断，需要弹出toast提示上传失败，并回到初始上传状态。

:::: row
::: col :span="6"
<br />

**上传成功**
- 直接提示用户成功的结果即可；

![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1f--wXXZgpessEaRZvHv-S451HGWBIDSK =100%x)
:::
::: col :span="6"
<br />

**上传失败**
- 可直接提示用户失败的结果或解释用户失败的具体原因；

![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1f0kgXbzrSrvyDy6MSfF45cIXxK-V3moq =100%x)
:::
::::

:::: row
::: col :span="6"
<br />

**上传部分成功**
- 提示用户成功上传数量和全量上传数量之间的关系，如xx/xxx.

![4_3](https://drive.google.com/thumbnail?sz=w3000&id=1lSQnqz8GcFni5aOZKtOcbR99Yl_XwiDc =100%x)
:::
::: col :span="6"
:::
::::

### 2. 同步上传基本使用
**【使用规则】**
- 场景：用于非批量上传、无多线程操作的简单上传场景；
- 触发：通过「点选上传」或「拖拽上传」的方式将格式、大小和数量正确的文件上传；
- 反馈：弹出遮罩加载进度反馈，除取消上传操作外，不可进行其他操作；最后根据上传结果给予相应的结果反馈。

![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1u94INLAHg7-ZUaJvTXgKO4NKLchmNXUh =100%x)

### 3. 异步上传基本使用
**【使用规则】**
- 场景：需要多线程操作、批量上传等场景；
- 触发：通过「点选上传」或「拖拽上传」的方式将格式、大小和数量正确的文件上传；
- 反馈：给予上传进度反馈，可支持多个批次上传和多进程操作；最后根据上传结果给予相应的结果反馈。

**【异常流】**
异步上传时，展示文件的上传进度，在上传的同时可进行其他操作，若上传时间较长，需要提供“取消上传”的操作按钮。

![6_1](https://drive.google.com/thumbnail?sz=w3000&id=1Fmk_5Fq-5Gk0xkmEWFxLGsT1UlhkbD4e =100%x)

### 4. 异步图片上传基本使用
:::: row
::: col :span="6"
**【使用规则】**
- 场景：图片上传通用；
- 触发：点击上传，触发选择文件操作，选择正确格式大小的文件后，后台异步分流上传；
- 反馈：可以支持多图片同时上传。上传成功后直接填充图片。 
:::

::: col :span="6"
![7_1](https://drive.google.com/thumbnail?sz=w3000&id=1T5xXmrV5Xl7RIrghJxAU72FNE6AkJzhg =100%x)
:::
::::

## 视觉样式
### 1. 尺寸
:::: row
::: col :span="6"
#### 1.1 拖拽式上传
- 说明文案样式：font-size: 16px；color: #333333；text-align: center；
- 辅助说明文案样式：font-size: 14px；color: #999999；
- 内容与边框的位置关系为上下、左右居中，四周最小边距为32px。
:::

::: col :span="6"
#### 1.2 拖拽式上传
- 图片上传框默认尺寸为：96px，一般表单场景下可使用此尺寸；
- 根据具体场景，可自定义上传框大小，但需注意，图片上传框最小宽度为56px
:::
::::

:::: row
::: col :span="6"
![8_1](https://drive.google.com/thumbnail?sz=w3000&id=1klWz9_iaqESxI2YbyxFin6T7m51AHvov =100%x) 
:::
::: col :span="6"
![8_2](https://drive.google.com/thumbnail?sz=w3000&id=1Ty51oL0u8zmkwRA4qGgnKYejPG3q7zUI =100%x)
:::
::::

### 2. 基本样式
#### 2.1 拖拽式上传
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **Normal** | ![9_1](https://drive.google.com/thumbnail?sz=w3000&id=1AA9zzoBi9E-MTPF8KoyA3UkmplPhY7JX =354x) | - background: #FAFAFA; <br />- border: 1px solid #D8D8D8; <br />- border-radius: 4px; |
| **Hover** | ![9_2](https://drive.google.com/thumbnail?sz=w3000&id=19t7kuY4EVt7xnPJXv2Bi_NyDQmGTKVth =354x) | - background: #FAFAFA; <br />- border: 1px solid #EE4D2D; <br />- border-radius: 4px; |
| **Drop** | ![9_3](https://drive.google.com/thumbnail?sz=w3000&id=1YBWPP8xq2ujni9v4dnaIltZ2pByKdpT1 =389x) | - background: #EE4D2D, 0.04; <br />- border: 1px solid #EE4D2D; <br />- border-radius: 4px; |
<br />

#### 2.2 图片上传
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **Normal** | ![10_1](https://drive.google.com/thumbnail?sz=w3000&id=1dkcy1sv2-elEgNgiTLkEoepje2isN3QZ =96x) | - background: #FFFFFF; <br />- border: 1px solid #CDCDCD; <br />- border-radius: 4px; |
| **Hover/Pressed** | ![10_2](https://drive.google.com/thumbnail?sz=w3000&id=1zYLq5dyZk1LDpOIxXgZujRpPwYL9odQB =103x) | - background: #FFFFFF;<br />- border: 1px solid #EE4D2D;<br />- border-radius: 4px; |
| **Disabled** | ![10_3](https://drive.google.com/thumbnail?sz=w3000&id=14vsUsvOWmC4Io_eeFbfCHp52Rw-_u-w5 =104x) | - 50% opacity  |
<br />

#### 2.3 已上传图片预览
| 状态 | 展示样式 | 元件属性 |
| :--  | :-- | :-- |
| **Normal** | ![11_1](https://drive.google.com/thumbnail?sz=w3000&id=18LV3PDWasuVaizn3KLsJ81PeIv7y4djZ =96x) | - 预览图遮罩：background: #000000, 0.04; <br />- 预览图圆角：4px。 |
| **Hover** | ![11_2](https://drive.google.com/thumbnail?sz=w3000&id=1jMn2FBz1dTQ1VHnNhmzQjD0xnsZsZVqw =290x) | -- hover遮罩属性：background: #000000, 0.50; <br />- 遮罩高度：默认情况为24px，在图片尺寸较大的场景可调整为32px； <br />- 图标位置说明： <br /> · 当只有一个icon时，icon在遮罩区域水平居中；   <br />· 当有两个icon时，每个icon各占遮罩宽度的1/2，位于该区域中心；   <br />· 当有三个icon时，每个icon各占遮罩宽度的1/3，位于该区域中心；  <br />· 当有四个icon时，每个icon各占遮罩宽度的1/4，位于该区域中心。。 |
| **Dragged** | ![11_3](https://drive.google.com/thumbnail?sz=w3000&id=17GKPsljatwpJrZmlbkABrwokdfBb0DgO =96x) | - box-shadow: 0 2px 8px 2px rgba(0,0,0,0.12) |
    