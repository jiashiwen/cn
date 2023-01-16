# describeOperationRecords


## 描述
查询操作日志

## 请求方式
GET

## 请求地址
https://antipro.jdcloud-api.com/v1/operationRecords


## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**pageNumber**|Integer|False|1|页码|
|**pageSize**|Integer|False|10|分页大小|
|**startTime**|String|True| |开始时间, UTC 时间, 格式：yyyy-MM-dd'T'HH:mm:ssZ|
|**endTime**|String|True| |结束时间, UTC 时间, 格式：yyyy-MM-dd'T'HH:mm:ssZ|
|**action**|Integer|False| |操作类型, 默认查全部. <br>- 0: 全部<br>- 1: 套餐变更<br>- 2: 防护规则变更<br>- 3: 防护对象变更<br>- 4: IP 地址变更<br>- 5: 防护包名称变更<br>- 6: IP地址库变更<br>- 7: 端口库变更<br>- 8: 访问控制规则变更|
|**name**|String|False| |防护包名称, 支持模糊匹配|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](describeoperationrecords#result)| |
|**requestId**|String| |
|**error**|[Error](describeoperationrecords#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](describeoperationrecords#err)| |
### <div id="err">Err</div>
|名称|类型|描述|
|---|---|---|
|**code**|Long|同http code|
|**details**|Object| |
|**message**|String| |
|**status**|String|具体错误|
### <div id="result">Result</div>
|名称|类型|描述|
|---|---|---|
|**dataList**|[OperationRecord[]](describeoperationrecords#operationrecord)| |
|**currentCount**|Integer|当前页数量|
|**totalCount**|Integer|实例总数|
|**totalPage**|Integer|总页数|
### <div id="operationrecord">OperationRecord</div>
|名称|类型|描述|
|---|---|---|
|**time**|String|操作时间|
|**name**|String|防护包名称|
|**action**|Integer|操作类型.<br>- 1: 套餐变更<br>- 2: 防护规则变更<br>- 3: 防护对象变更<br>- 4: IP 地址变更<br>- 5: 防护包名称变更<br>- 6: IP地址库变更<br>- 7: 端口库变更<br>- 8: 访问控制规则变更|
|**info**|String|操作详情|
|**operator**|String|操作人|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
