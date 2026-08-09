---
extend: /zh/components/search
---

## 组件元素
<br />

::::row 
::: col :span="5" 
![1-1](https://drive.google.com/thumbnail?sz=w3000&id=1uaUVboVkThhmFrblf-a7kNG9c4-3kX9G =100%x)
:::
::: col :span="1" 
<br />
:::
::: col :span="6" 
1. **输入框:** hover即触发边框。
2. **输入文字**
3. **后置图标（可选）:** 操作型图标。
4. **搜索图标**
5. **搜索结果:** 触发搜索后即显示多条搜索结果。
6. **选项面板:** 白色带投影的背景框。
:::
::::

## 类型汇总

| 名称 | 类型 | 使用场景 |
| :--  | :-- | :-- |
|<div style="width:240px">**简单搜索**</div>|![2-1](https://drive.google.com/thumbnail?sz=w3000&id=13YqYh7FAnjUFf_ao-qkkKGO7YFcVPGiq =240x)| - 适用于通用场景，轻量搜索时采用。|
|**模糊搜索**|![2-2](https://drive.google.com/thumbnail?sz=w3000&id=18fTXQ_wVrBojNQyDVKb1Z4qvcJgXaAo4 =240x)|- 适用于通用场景，搜索数据量较大的内容时采用。|
|**分项搜索**|![2-3](https://drive.google.com/thumbnail?sz=w3000&id=1oBJ5srz08ab6fItNW3kzf4miL33XPzs_ =343x)| - 适用于多个不同维度的搜索场景。|

## 使用用法
### 1. 简单搜索
【使用规则】
- 搜索交互：点击输出框输入搜索文本，按键盘「Enter」或点击「Search」按钮，进行搜索；
- 点击「X」清除文案，且回到初始全量内容页；或删除已输入文案后，输入框为空，且按键盘「Enter」或点击「搜索按钮」，回到初始全量内容页。

![3-1](https://drive.google.com/thumbnail?sz=w3000&id=1jcAGHznsEFNBTv9vavjDvjmHwu8stvUE =100%x)


### 2.模糊搜索
【使用规则】
- 输入搜索文本，自动匹配文本的建议结果，具体推荐结果由具体业务决定；
- 点击推荐结果中的一项，直接跳转该结果内容；
- 点击「搜索按钮」与键盘「Enter」，触发搜索；
- 点击「X」清除文案，回到初始全量内容页；或删除已输入文案后，输入框为空，且按键盘「Enter」或点击搜索按，回到初始全量内容页。

![3-2](https://drive.google.com/thumbnail?sz=w3000&id=1Ayfh1vsIKw5gu5dHjXMdvAEY_DKEIixU =100%x)


### 3.分项搜索
【使用规则】
- 除了增加多维度类型搜索选项外，其它交互逻辑基本与「模糊搜索」一致。

![3-3](https://drive.google.com/thumbnail?sz=w3000&id=13nSZYYTozo9T0GLWZu7V9hWeBkM9wIJK =100%x)


## 视觉样式
搜索公共模组是基于「[Select 下拉选择](#/select/design)」&「[Input 组件](#/input/design)」组件的样式逻辑进行定义，具体样式规则请查看该组件。
    