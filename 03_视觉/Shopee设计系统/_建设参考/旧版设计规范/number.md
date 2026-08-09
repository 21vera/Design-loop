---
title: Number Rules 数字规则
description: 数字规则为 Shopee Seller Centre 上各场景常用的数字使用方法
designer: Wei Huang
tabs:
  - title: 设计文档
    href: /zh/design/number
  - title: 更新记录
    href: /zh/design/number/records
---

## 数值类数字

1. 数值类数字指可以进行计算的数字；
2. 均采用阿拉伯数字；
3. 不可被省略。

### 1.1 位数缩减
【使用规则】 显示位数有限制时，可以使用K/M/B（千/百万/十亿）缩减长度；
- K/M/B前的数字可以保留整数或一位小数；
- 取整方式四舍五入。

|展示形式|数值范围|举例| |
|:--|:--|:--|:--|
|**$###.##**|0.00 – 999.99|90.02|90.02|
|**$###.#K**|1,000.00 – 999,999.99|15,000|15.0K|
|**$###.#M**|1,000,000.00 – 999,999,999.99|15,893,399.99|15.9M|
|**$###.#B**|1,000,000,000.00 – 999,999,999,999.99|15,023,893,399.99|15.0B|

### 1.2 金额
【使用规则】适用于展示金额相关的数据。例如价格、余额等。
- 必须带有货币符号；
- 超过3位时，使用千位分隔符；
- 小数点后至多保留两位；
- 各地区金额展示格式见右表；
- 印尼和越南使用「, 」作为小数点，使用「. 」作为千分符。
- 越南货币最小展示到₫1（K/M/B前面可以出现小数点，例如：₫12,9K）。
<br />

|正值|负值|零值|空值|数值范围|加减|
|:--|:--|:--|:--|:--|:--|
|**$129,999.99**|$-129,999.99|$0.00|$-|$99.99 – $199.99|± $12.99|
<br />

|SG|ID|MY|PH|TW|TH|VN|CN Mainlad|
|:--|:--|:--|:--|:--|:--|:--|:--|
|**$#,###.##**|Rp#.###,##|RM#,###.##|₱#,###.##|NT$#,###.##|฿#,###.##|₫#.###|¥#,###.##|

### 1.3 百分比
【使用规则】显示位数有限制时，可以使用K/M/B（千/百万/十亿）缩减长度。
- K/M/B前的数字可以保留整数或一位小数。
- 取整方式四舍五入。

|正值|负值|零值|空值|数值范围|上升/下降|
|:--|:--|:--|:--|:--|:--|
|**24.99%**|-24.99%|0.00%|-%|1.99% – 24.99%|±24.99%|

### 1.4 序数
【使用规则】适用于对事物进行排序。例如步骤、排行等。- 序数前可以使用名词。例如图片1，图片2。
- 排名中前3/5名可以使用不同的颜色或样式。

![123](https://drive.google.com/thumbnail?sz=w3000&id=1L3AgMTAYEvEWZotU-gvmC7fN1NuGEA51 =100%x)

### 1.5 单位
【使用规则】适用于区分多种数值类型时。
- 货币单位处于数字前
- 计量单位处于数字后
- 通常单位和数值间没有空格

![123](https://drive.google.com/thumbnail?sz=w3000&id=1iYFBoeTswZMpPnrlvLn9HnL_Vzrlqx5D =100%x)

## 非数值类数字
非数值类数字指不可以直接计算的数据，包括日期、时间、电话、邮编、账号等。

### 2.1 日期和时间
【使用规则】
- 自然周定义为周日到周六；
- 如无特殊必要，优先使用文字表示月份。若使用纯数字，必须确保该场景不会产生歧义；
- 不宜省略、折行；
- 不建议单独使用「日」，建议使用「月+日」或「年+月+日」来表达日期。

<table>
  <thead>
    <tr>
      <th>类别</th>
      <th>元素</th>	
      <th>中文示例</th>
      <th>英文示例</th>
      <th>数字示例</th>	
   </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="6" style="font-weight:500">日期</td>
      <td>年</td>
      <td>2019年</td>
      <td>2019</td>
      <td>2019</td>
    </tr>
    <tr>
      <td>月</td>
      <td>1月</td>
      <td>Jan </td>
      <td>01</td>
    </tr>
    <tr>
      <td>日</td>
      <td>6日</td>
      <td>6 </td>
      <td>06</td>
    </tr>
    <tr>
      <td>年+月</td>
      <td>2019年1月</td>
      <td>Jan 2019</td>
      <td>2019/01</td>
    </tr>
    <tr>
      <td>年+日</td>
      <td>1月6日</td>
      <td>6 Jan</td>
      <td>01/06</td>
    </tr>
    <tr>
      <td>年+月+日</td>
      <td>2019年1月6日</td>
      <td>6 Jan 2019</td>
      <td>2019/01/06</td>
    </tr>
     <tr>
      <td rowspan="2" style="font-weight:500">时间</td>
      <td>hh:mm</td>
      <td>19:20</td>
      <td>6 Jan 2019</td>
      <td>-</td>
    </tr>
    <tr>
      <td>hh:mm:ss</td>
      <td>14:20:36</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>  
</table>

### 2.2 不同站点和语言的时间日期格式
【使用规则】
- 注意越南语的月份表达为“thg+阿拉伯数字”，因此月份和年份有逗号区隔；
- 注意菲律宾的日期格式为月日年，因此英文显示时日期和年份之间有逗号区隔；
- 注意台湾和中国大陆的日期格式为年月日。但是在平台上切换为英文时，使用日/月/年的顺序。



| |SG|ID|MY|TH|VN|PH|TW|
|:--|:--|:--|:--|:--|:--|:--|:--|
|**日期格式**|dd/mm/yyyy|dd/mm/yyyy|dd/mm/yyyy|dd/mm/yyyy|dd/mm/yyyy|mm/dd/yyyy|yyyy/mm/dd|
|**本地语言**|6 Jan 2019|6 Okt 2019|6 Ogos 2019|6 มกราคม 2019|6 thg 1, 2019|暂未提供|2019年1月6日|
|**英文**|6 Jan 2019|6 Oct 2019|6 Aug 2019|6 Jan 2019|6 Jan 2019|Jan 6, 2019|6 Jan 2019|
|**数字**|06/01/2019|06/10/2019|06/08/2019|06/01/2019|06/01/2019|01/06/2019|2019/01/06|

### 2.3 时间日期组合使用
【使用规则】
- 越南和其他地区略有不同，时间在前，用逗号隔开。


| |TW、CN Mainland|SG/ID/MY/PH/TH|VN|
|:--|:--|:--|:--|
|**格式**|日期 星期 时间|日期 星期 时间|日期 星期 时间|
|**本地语言**|2019年09月05日 星期三 12:20:36|-|12:20:36, Th 2, 7 thg 1, 2019|
|**英文**|Wed, 5 Sep 2019 12:20:36|Mon, 07/01/2019 12:20:36|12:20:36, Mon, 7 Jan 2019|
|**数字**|2019/09/05 星期三 12:20:36|Mon, 07/01/2019 12:20:36|12:20:36, Mon, 07/01/2019|

### 2.4 时间跨度

【使用规则】
- 适用于展示一段时间跨度；
- 使用“–”连接起止时间，连接符前后有一个空格。（此处链接符号为Hyphen，详见文案规则-标点符号）

| 类型|中文示例|英文示例|数字示例|
|:--|:--|:--|:--|
|**基础**|2019年08月26日 – 2019年8月30日|26 Aug 2019 – 30 Aug 2020|2019/01/06 – 2019/02/12|
|**省略一个年份**|2019年08月26日 – 8月30日|26 Aug – 30 Aug, 2019|01/06 – 01/12, 2019|
|**不展示年份**|08月26日 – 8月30日|26 Aug – 30 Aug|01/06 – 01/12|
|**时间**|09:00 - 18:30| 

### 2.5 常用时间段表达
【使用规则】
- 适用于时间选择器；
- 适用于时间段对比；
- Day、Week、Month、Year的含义均为自然日/周/月/年。若表示非自然周/月/年，请使用具体天数，如 Previous 7 Days；
- Last表示从当前时间点往前推算，Previous表示从过去某一时间往前推算。

<table>
  <thead>
    <tr>
      <th style="width:180px;">类型</th>
      <th>中文示例</th>	
      <th>英文示例</th>
      <th style="width:300px;">使用说明</th>
   </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2" style="font-weight:500">时间点</td>
      <td >实时</td>
      <td>Real-time</td>
      <td>-</td>
    </tr>
    <tr>
      <td>昨天18:00</td>
      <td>Yesterday 18:00</td>
      <td>-</td>
    </tr>
    <tr>
      <td rowspan="13" style="font-weight:500">时间段</td>
      <td>今天</td>
      <td>Today</td>
      <td>-</td>
    </tr>
    <tr>
      <td>昨天</td>
      <td>Yesterday</td>
      <td>-</td>
    </tr>
    <tr>
      <td>今天直到18:00</td>
      <td>Today Until 18:00</td>
      <td>-</td>
    </tr>
    <tr>
      <td>昨天00:00 - 18:00</td>
      <td>Yesterday 00:00-18:00</td>
      <td>-</td>
    </tr>
    <tr>
      <td>过去7天</td>
      <td>Last 7 Days</td>
      <td rowspan="3">表示从昨天开始计算的X天。例如：今天为9月12日，“Last 7 Days”表示9月5日至9月11日。</td>
    </tr>
    <tr>
      <td>过去30天</td>
      <td>Last 30 Days</td>
    </tr>
    <tr>
      <td>过去 X 天</td>
      <td>Last X Days</td>
    </tr>
    <tr>
      <td>过去1周</td>
      <td>Last Week</td>
      <td rowspan="6">表示今天所在这周的上一个自然周/月/年。例如：今天为9月12日周四，“Last Week”表示9月1日至9月7日。（周日为每周起始）</td>
      <tr>
      <td>过去X周</td>
      <td>Last X Weeks</td>
    </tr><tr>
      <td>过去1个月</td>
      <td>Last Month</td>
    </tr><tr>
      <td>过去 X 个月</td>
      <td>Last X Months</td>
    </tr><tr>
      <td>过去1年</td>
      <td>Last Year</td>
    </tr><tr>
      <td>过去 X 年</td>
      <td>Last X Years</td>
    </tr>
    </tr>
    <tr>
      <td rowspan="12" style="font-weight:500">时间点</td>
      <td>实时</td>
      <td>Real-time</td>
      <td>-</td>
    </tr>
    <tr>
      <td>少于一天的时间段</td>
      <td>参照时间段表达</td>
      <td>-</td>
    </tr>
    <tr>
      <td>前1天</td>
      <td>Previous Days</td>
      <td rowspan="4">表示选中时间之前的X天。通常配合Yesterday或Last X Days使用。例如：今天为9月12日，选择查看Last 7 Days（9月5日至9月11日）的数据，则对比时间段为“Previous 7 Days”，表示9月4日至8月2</td>
    </tr>
    <tr>
      <td>前7天</td>
      <td>Previous 7 Days</td>
    </tr>
    <tr>
      <td>前30天</td>
      <td>Previous 30 Days</td>
    </tr>
    <tr>
      <td>前 X 天</td>
      <td>Previous X Days</td>
    </tr>
    <tr>
      <td>前1周</td>
      <td>Previous Week</td>
      <td rowspan="4">表示选中时间之前的X个自然周/月/年。通常配合Last Week/Month/Year使用。例如：日期选择Last Week，则对比时间段为Previous Week。</td>
    </tr>
    <tr>
      <td>前 X 周</td>
      <td>Previous X Weeks</td>
    </tr>
    <tr>
      <td>前1个月</td>
      <td>Previous Month</td>
    </tr>
    <tr>
      <td>前 X 个月</td>
      <td>Previous X Months</td>
    </tr>
    <tr>
      <td>前1年</td>
      <td>Previous Year</td>
    </tr>
    <tr>
      <td>前 X 年</td>
      <td>Previous X Years</td>
    </tr>
  </tbody>
</table>

### 2.6 相对时间

【使用规则】
- 适用于无明确日期或时刻的时间表达；
- 适用于消息、新闻推送等场景。通过相对时间表现事件与此刻的距离；
- 现提供两套模糊时间表达规则，按照倒计时和按照自然日划分；
- 向下取整。例如：2分30秒前表达为“2分钟之前”。

|时间段（按倒计时）|中文示例|英文示例|
|:--|:--|:--|
|<div style="width:150px">**1分钟内**</div>|<div style="width:150px">刚刚</div>|Just now|
|**1小时内**|X 分钟之前 （1≤X≤59）|X minutes ago|
|**24小时内**|X 小时前（1≤X≤23）|X hours ago|
|**7天内**|X 天前（1≤X≤7）|X days ago|
|**7天以上**|具体日期/时间|具体日期/时间|

|时间段（按自然日）|中文示例|英文示例|
|:--|:--|:--|
|<div style="width:160px">**当天内**</div>|<div style="width:160px">hh:mm</div>|hh:mm|
|**前一天**|昨天hh:mm|Yesterday hh:mm|
|**更早**|具体日期/时间|具体日期/时间|


### 2.7 时区
【使用规则】
- 适用于注明国家和地区所处的时区；- 使用GMT格林威治标准时间格式；- 目前ID统一使用GMT+7。


|格式|示例|空值|
|:--|:--|:--|
|**GMT+阿拉伯数字**|GMT+8|GMT-|
<br />

|SG|ID|MY|PH|TW|TH|VN|CN Mainland|
|:--|:--|:--|:--|:--|:--|:--|:--|
|**GMT+8**|GMT+7<br />GMT+8<br />GMT+9|GMT+8|GMT+8|GMT+8|GMT+7|GMT+7|GMT+8|

### 2.8 电话、账号、邮编
【使用规则】
- 不可折行；
- 遵循当地使用习惯；
- 过长的数据可以分段。具体规则遵循当地习惯。例如：银行卡号 #### #### #### ####，手机号### #### ####。

