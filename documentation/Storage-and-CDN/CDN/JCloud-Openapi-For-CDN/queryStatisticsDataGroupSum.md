# queryStatisticsDataGroupSum


## 描述
查询统计数据并进行汇总加和

## 请求方式
POST

## 请求地址
https://cdn.jdcloud-api.com/v1/vodStatistics:groupSum


## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**startTime**|String|True| |查询起始时间,UTC时间，格式为:yyyy-MM-dd'T'HH:mm:ss'Z'，示例:2018-10-21T10:00:00Z|
|**endTime**|String|True| |查询截止时间,UTC时间，格式为:yyyy-MM-dd'T'HH:mm:ss'Z'，示例:2018-10-21T10:00:00Z|
|**domain**|String|False| |需要查询的域名, 必须为用户pin下有权限的域名|
|**subDomain**|String|False| |待查询的子域名|
|**fields**|String|False| |需要查询的字段|
|**area**|String|False| | |
|**isp**|String|False| | |
|**origin**|String|False| | |
|**period**|String|False| |时间粒度，可选值:[oneMin,fiveMin,followTime],followTime只会返回一个汇总后的数据|
|**groupBy**|String|True| |分组依据，可选项为area,isp,domain|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](querystatisticsdatagroupsum#result)| |
|**requestId**|String| |

### <div id="result">Result</div>
|名称|类型|描述|
|---|---|---|
|**startTime**|String| |
|**endTime**|String| |
|**domain**|String| |
|**statistics**|[StatisticsGroupSumDataItem[]](querystatisticsdatagroupsum#statisticsgroupsumdataitem)| |
### <div id="statisticsgroupsumdataitem">StatisticsGroupSumDataItem</div>
|名称|类型|描述|
|---|---|---|
|**startTime**|String|UTC时间，格式为:yyyy-MM-dd'T'HH:mm:ss'Z'，示例:2018-10-21T10:00:00Z|
|**endTime**|String|UTC时间，格式为:yyyy-MM-dd'T'HH:mm:ss'Z'，示例:2018-10-21T10:00:00Z|
|**data**|Object|查询结果,类型为HashMap<String, Object>|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
