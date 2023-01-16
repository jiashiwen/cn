# describeCpsIpResources


## 描述
查询基础防护已防护的云物理服务器公网 IP 的安全信息. 包括云物理服务器的公网 IP 和弹性公网 IP.


## 请求方式
GET

## 请求地址
https://baseanti.jdcloud-api.com/v1/regions/{regionId}/cpsIpResources

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域编码. 基础防护已支持华北-北京, 华东-宿迁, 华东-上海, 华南-广州|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**pageNumber**|Integer|False|1|页码|
|**pageSize**|Integer|False|10|分页大小|
|**ip**|String|False| |IP 模糊匹配|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](describecpsipresources#result)| |
|**requestId**|String| |
|**error**|[Error](describecpsipresources#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](describecpsipresources#err)| |
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
|**dataList**|[IpResource[]](describecpsipresources#ipresource)| |
|**currentCount**|Integer|当前页数量|
|**totalCount**|Integer|总数|
|**totalPage**|Integer|总页数|
### <div id="ipresource">IpResource</div>
|名称|类型|描述|
|---|---|---|
|**region**|String|公网 IP 所在区域编码|
|**resourceType**|Integer|公网 IP 类型或绑定资源类型. <br><br>- 0: 未知类型<br><br>- 1: 弹性公网 IP(IP 为弹性公网 IP, 绑定资源类型未知)<br><br>- 10: 弹性公网 IP(IP 为弹性公网 IP, 但未绑定资源)<br><br>- 11: 云主机<br><br>- 12: 负载均衡<br><br>- 13: 原生容器实例<br><br>- 14: 原生容器 Pod<br><br>- 2: 云物理服务器公网 IP<br><br>- 3: Web应用防火墙公网 IP<br><br>- 4: 托管区公网 IP"<br>|
|**ip**|String|公网 IP 地址|
|**bandwidth**|Long|带宽上限, 单位 Mbps|
|**cleanThresholdBps**|Long|每秒请求流量|
|**cleanThresholdPps**|Long|每秒报文请求数|
|**blackHoleThreshold**|Long|黑洞阈值|
|**instanceId**|String|绑定防护包 ID, 为空字符串时表示未绑定防护包|
|**instanceName**|String|绑定防护包名称, 为空字符串时表示未绑定防护包|
|**instanceType**|Integer|套餐类型, 为 0 时未绑定防护包. <br>- 1: 独享 IP<br>- 2: 共享 IP|
|**safeStatus**|Integer|安全状态. <br>- 0: 安全<br>- 1: 清洗<br>- 2: 黑洞|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
