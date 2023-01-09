# setIpCleanThreshold


## 描述
设置基础防护已防护公网 IP 的清洗阈值, 支持 ipv4 和 ipv6

## 请求方式
POST

## 请求地址
https://baseanti.jdcloud-api.com/v1/regions/{regionId}/setIpCleanThreshold

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域编码. 基础防护已支持华北-北京, 华东-宿迁, 华东-上海, 华南-广州|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**ipCleanThresholdSpec**|[IpCleanThresholdSpec](setipcleanthreshold#ipcleanthresholdspec)|True| |请求参数|

### <div id="ipcleanthresholdspec">IpCleanThresholdSpec</div>
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**ip**|String|True| |基础防护已防护公网 IP, 支持 ipv4 和 ipv6. <br><br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describeelasticipresources'>describeElasticIpResources</a> 接口查询基础防护已防护的私有网络弹性公网 IP<br><br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describecpsipresources'>describeCpsIpResources</a> 接口查询基础防护已防护的云物理服务器公网IP 和 弹性公网 IP<br><br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describewafipresources'>describeWafIpResources</a> 接口查询基础防护已防护的Web应用防火墙 IP<br><br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describeccsipresources'>describeCcsIpResources</a> 接口查询基础防护已防护的托管区公网 IP<br>|
|**cleanThresholdBps**|Long|True| |触发清洗的流量速率, 单位 bps. 取值范围由 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describeipcleanthresholdrange'>describeIpCleanThresholdRange</a> 接口查询可知|
|**cleanThresholdPps**|Long|True| |触发清洗的报文流量速率, 单位 pps. 取值范围由 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describeipcleanthresholdrange'>describeIpCleanThresholdRange</a> 接口查询可知|

## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](setipcleanthreshold#result)| |
|**requestId**|String| |
|**error**|[Error](setipcleanthreshold#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](setipcleanthreshold#err)| |
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
|**code**|Integer|修改结果, 0: 修改失败, 1: 修改成功|
|**message**|String|修改失败时给出具体原因|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
