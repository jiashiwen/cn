# addProtectedIp


## 描述
添加防护包防护 IP. <br>- 防护包仅能防护防护包实例所在区域的公网 IP, 且该公网 IP 未被其他防护包防护, 如果已经被其他防护包防护, 请先调用删除防护包防护 IP 接口删除防护 IP<br>- 防护包可添加的防护 IP 个数小于等于防护包的可防护 IP 数量减去已防护的 IP 数量<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-protection-package/api/describeelasticipresources'>describeElasticIpResources</a> 接口查询防护包可防护的弹性公网 IP<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-protection-package/api/describecpsipresources'>describeCpsIpResources</a> 接口查询防护包可防护的云物理服务器公网 IP<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-protection-package/api/describewafipresources'>describeWafIpResources</a> 接口查询防护包可防护的Web应用防火墙公网 IP<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-protection-package/api/describeccsipresources'>describeCcsIpResources</a> 接口查询防护包可防护的托管区公网 IP

## 请求方式
POST

## 请求地址
https://antipro.jdcloud-api.com/v1/regions/{regionId}/instances/{instanceId}:addProtectedIp

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域 Id, DDoS 防护包目前支持华北-北京, 华东-宿迁, 华东-上海|
|**instanceId**|String|True| |防护包实例 Id|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**protectedIpSpec**|[ProtectedIpSpec](addprotectedip#protectedipspec)|True| |添加防护包防护 IP 请求参数|

### <div id="protectedipspec">ProtectedIpSpec</div>
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**ip**|String[]|True| |被防护 IP 列表|

## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](addprotectedip#result)| |
|**requestId**|String| |
|**error**|[Error](addprotectedip#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](addprotectedip#err)| |
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
|**code**|Integer|添加防护 IP 结果, 0: 添加失败, 1: 添加成功|
|**message**|String|添加失败时给出具体原因|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
