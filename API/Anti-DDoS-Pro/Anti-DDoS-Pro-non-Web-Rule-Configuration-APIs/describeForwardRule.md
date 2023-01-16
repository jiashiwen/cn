# describeForwardRule


## 描述
查询非网站类规则

## 请求方式
GET

## 请求地址
https://ipanti.jdcloud-api.com/v1/regions/{regionId}/instances/{instanceId}/forwardRules/{forwardRuleId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |区域 ID, 高防不区分区域, 传 cn-north-1 即可|
|**instanceId**|String|True| |高防实例 Id|
|**forwardRuleId**|String|True| |转发规则 Id|

## 请求参数
无


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](describeforwardrule#result)| |
|**requestId**|String| |
|**error**|[Error](describeforwardrule#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](describeforwardrule#err)| |
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
|**data**|[ForwardRule](describeforwardrule#forwardrule)| |
### <div id="forwardrule">ForwardRule</div>
|名称|类型|描述|
|---|---|---|
|**id**|String|规则 Id|
|**instanceId**|String|实例 Id|
|**protocol**|String|TCP 或 UDP|
|**cname**|String|规则的 CNAME|
|**originType**|String|回源类型: ip 或者 domain|
|**serviceIp**|String|该规则使用中的高防 IP|
|**serviceIpConfig**|[ServiceIpConfig](describeforwardrule#serviceipconfig)|已配置的高防 IP 列表|
|**port**|Integer|端口号|
|**algorithm**|String|转发规则. <br>- wrr: 带权重的轮询<br>- rr:  不带权重的轮询<br>- sh:  源地址hash|
|**originAddr**|[OriginAddrItem[]](describeforwardrule#originaddritem)| |
|**onlineAddr**|String[]|备用的回源地址列表|
|**originDomain**|String|回源域名|
|**originPort**|Integer|回源端口号|
|**status**|Integer|0: 防御状态<br>1: 回源状态|
### <div id="originaddritem">OriginAddrItem</div>
|名称|类型|描述|
|---|---|---|
|**ip**|String|回源ip|
|**weight**|Integer|权重|
|**inJdCloud**|Boolean|是否为京东云内公网ip|
### <div id="serviceipconfig">ServiceIpConfig</div>
|名称|类型|描述|
|---|---|---|
|**serviceIps**|[ServiceIpConfigItem[]](describeforwardrule#serviceipconfigitem)|已配置的高防IP列表|
### <div id="serviceipconfigitem">ServiceIpConfigItem</div>
|名称|类型|描述|
|---|---|---|
|**serviceIp**|String|高防IP|
|**securityStatus**|String|安全状态. <br>- SAFE: 安全<br>- CLEANING: 清洗中<br>- BLOCKING: 封禁中|
|**useStatus**|Integer|使用状态, 1: 使用中, 0: 备用候选|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**404**|NOT_FOUND|
