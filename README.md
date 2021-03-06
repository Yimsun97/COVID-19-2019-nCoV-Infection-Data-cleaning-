# COVID-19-2019-nCoV-Infection-Data-cleaning-
针对新冠病毒疫情数据的清洗脚本和清洗后的数据，

# 源数据说明
源数据使用 https://github.com/BlankerL 的 https://github.com/BlankerL/DXY-COVID-19-Data/blob/master/csv/DXYArea.csv
其定时从丁香园网站抓取的原始各地区上报数据

##### 感谢 BlankerL 的工作

原始数据格式如下

provinceName | provinceEnglishName | cityName | cityEnglishName | province_confirmedCount | province_suspectedCount | province_curedCount | province_deadCount | city_confirmedCount | city_suspectedCount | city_curedCount | city_deadCount | updateTime
:-: | :-: | :-: | :-: | :-:| :-: | :-: | :-: | :-:| :-: | :-: | :-: | :-:
河南省 | Henan | 信阳 | Xinyang | 1231 | 0 | 415 | 13 | 261 | 0 | 74 | 2 | 2020-02-16 11:48:34.832|

原始数据有两个不足
1. 原始数据每天都会多次抓取数据，同一个地区每天存在多条记录，因为原始统计数据并不是连续时效性的，各地区并不是按小时的时间段发布，因此每天只需要一条数据
2. 原始数据仅统计省和市的累计数据

针对这两个问题，我做了两个脚本来对数据进行清洗

# 脚本说明
- data_step1.py  第一步处理 本脚本将各省市每天的数据进行去重处理，每个省市只保留最新的一条数据 （也可选择保留当天最大数值）
- data_step2.py  第二步处理 基于data_step1.py的输出文件， 计算每天的新增数据，通过当天数据减去前一天数据的方式，计算出每天新增数据

说明：各地区数据质量不同，同时存在后面修正前期数据，进行核销的处理，因此有时候当天数据会比前一天还少，新增数据为负

# Data说明
data 目录存放了我直接清洗出的数据，方便大家使用，免得大家再配Python环境，去下载数据运行脚本。 源数据不翻墙好像还不能直接下载

里面csv是直接使用脚本导出的数据，后续每天争取更新

excel文件，是对数据源使用了透视图并增加了一些图表分析的结果

![ ]( https://github.com/Avens666/COVID-19-2019-nCoV-Infection-Data-cleaning-/blob/master/img/Image1.jpg )


# 数据下载说明
由于raw.githubusercontent.com 被DNS污染，部分地区不能下载， 如果你的github的文件下载有问题，试试hosts文件加入如下内容

`199.232.28.133 raw.githubusercontent.com`

2020.2.16 cz

#  ------ 2020.02.18 22：00 更新脚本和数据 ---------

由于原始数据有一些缺陷，导致之前计算新增数据时存在不准确，新增数据和累计数据对不齐得问题

这两天修改脚本，增加了对原始数据不完整的问题进行动态修正，基本解决了数据的问题

同时这两天原始数据质量也在提升

今天更新了脚本，同时更新了我清洗后的数据，以及excel表格，excel表格现在调整为修改原始数据表单后，所有图表和数据可动态更新，数据表单更新后，只要对数据透视表的分析菜单手动操作一次全部刷新即可

#  ------ 2020.02.24 22：00 更新脚本和数据 ---------

excel文件增加了全国及湖北疑似病例的数据，这个数据是手动收集，原始数据没有

脚本增加了直接数据写入excel文件的代码，我设置了开关，但现在将其屏蔽了，因为发现用py库操作excel文件，数据是正确的，但有些图表样式会丢失

借这个项目也熟悉了PY的数据分析方法，后续可能考虑尝试透视图及图表也用python脚本来做

#  ------ 2020.02.29 22：00 更新数据 ---------

最近excel文件中增加了一些手动维护的数据，湖北省，武汉市，全国的疑似数据，武汉市内各区的数据。并做了预测模型
