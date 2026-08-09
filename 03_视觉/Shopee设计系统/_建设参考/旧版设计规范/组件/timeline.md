---
extend: /zh/components/timeline
---
## 组件元素
<br />

:::: row
::: col :span="5"
![1_1](https://drive.google.com/thumbnail?sz=w3000&id=1ZKyNXV_87bQepHqSnU8i13CdAOVSAxAz =100%x)
:::
::: col :span="7"
<br />

1. **有节点的轴线**：连接事件的轴线，每个节点对应一个事件。
2. **事件标题**：事件的名称或概括。
3. **时间**：事件发生的时间点。
4. **辅助信息（可选）**：事件相关的说明，可包括文字、图片。
:::
::::


## 类型汇总 
:::: row
::: col :span="6"
### 1. 基础时间轴
【使用场景】
- 用于将事件按时间顺序展示，例如物流状态、订单状态、审核状态的跟踪等。
:::
::: col :span="6"
### 2. 自定义图标节点的时间轴
【使用场景】
- 用于节点事件名称简洁易懂场景；
- 用于流程固定的场景。例如交易流程、退换货流程、审核流程等；
- 用于需要视觉化表现每个节点事件的特点的场景。
:::
::::

:::: row
::: col :span="6"
![2_1](https://drive.google.com/thumbnail?sz=w3000&id=10dXHeFePP6fIDGL7XlwQgR5qk4MJM9-8 =100%x)
:::
::: col :span="6"
![2_2](https://drive.google.com/thumbnail?sz=w3000&id=1-fcJxEc034gNzLZcYBpjPu-XXo5wMaIr =100%x)
:::
::::


## 使用用法
:::: row
::: col :span="4"


【使用规则】
- 基础时间轴与自定义图标节点的时间轴在交互逻辑上一致；
- 排序规则：事件按照时间由近及远，从高到低垂直排列；
- 布局：靠左对齐，事件内容处于时间轴右侧；
- 数量：辅助信息图片数量不超过1张；
- 轴线节点不可点击，且不允许用户跳转到除当前步骤之外的其他步骤。
:::
::: col :span="8"
![3_1](https://drive.google.com/thumbnail?sz=w3000&id=17zPFVxaJuu0qbewJSUwH1DYf3Gah3tTa =100%x)
:::
::::

## 视觉样式
### 1. 颜色、尺寸
- 事件标题：font-size: 14px；font-weight: Medium；
- 辅助信息文本：font-size: 12px；color: #666666；
- 辅助信息图片：尺寸：56*56px；border-radius: 4px；
- 时间文本：font-size: 12px；color: #999999；
- 轴线样式：border: 1px solid #E5E5E5。

![4_1](https://drive.google.com/thumbnail?sz=w3000&id=1O8aC3CaEJI16viXRdVrI6g6kpCiZ26Vn =100%x)

### 2. 间距定义
- 描述文本折行宽度为220px，当文本折行后行数 ≦7 时，展示全部内容，当文本折行后行数 >7 时，则出现展开/收起按钮，并收至5行；
- 调整排版与折行不应当作为步骤或内容不合理安排的后备方案。设计者应当综合考虑场景和页面空间，并且合理分解任务、斟酌文案，进而设计出合理的步骤条。

![4_2](https://drive.google.com/thumbnail?sz=w3000&id=1GW1g2uofW9t8qMzD-lrJKJW8hqP_AEzW =100%x)

## 场景示例
在页面上时，左右至少保持24px的间距。

![5_1](https://drive.google.com/thumbnail?sz=w3000&id=1-tJaoO6rtpFLVw4xW9mFHAw0JyPNQ4Fu =100%x)
    