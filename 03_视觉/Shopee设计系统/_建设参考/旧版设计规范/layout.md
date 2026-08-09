---
title: Layout & Grid 布局
description: 页面布局是将页面各要素进行合理、有效、统一地排布，由页面头部、侧边栏、内容区、底部组成，用于确定页面的主线与支线，以此保障平台结构主次分明、结构清晰、引导明确以及操作方便
designer: Gewei Feng
tabs:
  - title: 设计文档
    href: /zh/design/layout
  - title: 更新记录
    href: /zh/design/layout/records
---

## 栅格规则
设计师进行 Shopee 旗下项目首选 “Roboto” 为设计字体；

### 1. 侧边栏栅格
在 Seller Centre 的栅格系统中，我们需要对左边侧边栏保留固定空间，因此栅格规则仅存在于内容区（即 1104px），其中：
- 侧边栏：固定与视图左侧，最小宽度为 156px；最大宽度 220px；
- 内容区：宽度固定为 1104px；并居中「不包括侧边栏的视图」里；
- 列宽为 64px，共 14 列；列间距宽度为 16px。

<br />

![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1t4K_3D9HRKyBGC1JzVjIfBfEqvPSkCww =100%x)


### 2. 无侧边栏栅格
- 内容区：主内容宽度为 1104px，辅内容宽度为 304px；
- 列宽为 64px，共 18 列；列间距宽度为 16px。

<br />

![1-2](https://drive.google.com/thumbnail?sz=w3000&id=1Q38SrZg3WsWJ5OqJM6c6GV4fvWAZ3SXC =100%x)



## 布局类型汇总
### 1. 不包含侧边栏
【使用场景】
- 用户与产品目标明确/单一的情况下，采用此布局；
- 适合聚焦在主工作区域信息内容的情况；
- 层级结构操作上较为单一，聚焦在内容区块的操作的情况。

![1-3](https://drive.google.com/thumbnail?sz=w3000&id=15ioFuXL7JnlO1bS8753WBEmLVS_XeOH2 =100%x)


### 2. 包含侧边栏
【使用场景】
- 适用于导航内容与信息层级较为多且复杂的情况下，该布局具备较好的扩展性；
- 在侧边固定的情况下，横向页面内容的空间会受到一定限制。

![1-4](https://drive.google.com/thumbnail?sz=w3000&id=1WBsDiKG0inv0HxtPOr7tnGCaWTvwCsUA =100%x)
