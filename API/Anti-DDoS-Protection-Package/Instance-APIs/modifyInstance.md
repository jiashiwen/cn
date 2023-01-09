# modifyInstance


## 描述
升级防护包实例

## 请求方式
PATCH

## 请求地址
https://antipro.jdcloud-api.com/v1/regions/{regionId}/instances/{instanceId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域 Id, DDoS 防护包目前支持华北-北京, 华东-宿迁, 华东-上海|
|**instanceId**|String|True| |防护包实例 Id|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**modifyInstanceSpec**|[ModifyInstanceSpec](modifyinstance#modifyinstancespec)|True| |升级防护包实例请求参数|

### <div id="modifyinstancespec">ModifyInstanceSpec</div>
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**ipNum**|Integer|True| |可防护 IP 数量, 1, 5, 10, 50, 100, 1000(不限), 可升级, 不可降级|
|**bpGbps**|Integer|True| |保底带宽: 10, 20, 30, 50, 单位: Gbps, 可升级, 不可降级|
|**epGbps**|Integer|True| |弹性带宽: 0, 10, 20, 单位: Gbps, 可升级, 可降级|

## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](modifyinstance#result)| |
|**requestId**|String| |
|**error**|[Error](modifyinstance#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](modifyinstance#err)| |
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
|**instanceId**|String|升级的防护包实例 Id|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
