# describeAttackLogs


## 描述
查询攻击记录

## 请求方式
GET

## 请求地址
https://baseanti.jdcloud-api.com/v1/attacklog


## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**pageNumber**|Integer|False|1|页码|
|**pageSize**|Integer|False|10|分页大小|
|**startTime**|String|True| |开始时间, UTC 时间, 格式: yyyy-MM-dd'T'HH:mm:ssZ|
|**endTime**|String|True| |结束时间, UTC 时间, 格式: yyyy-MM-dd'T'HH:mm:ssZ|
|**ip**|String[]|False| |基础防护已防护的公网 IP, ip 不为空时, 查询 ip 对应的攻击记录, ip 为空时, 查询用户所有攻击记录<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describeelasticipresources'>describeElasticIpResources</a> 接口查询基础防护已防护的私有网络弹性公网 IP<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describecpsipresources'>describeCpsIpResources</a> 接口查询基础防护已防护的云物理服务器公网IP 和 弹性公网 IP<br>- 使用 <a href='http://docs.jdcloud.com/anti-ddos-basic/api/describeccsipresources'>describeCcsIpResources</a> 接口查询基础防护已防护的托管区公网 IP|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](describeattacklogs#result)| |
|**requestId**|String| |
|**error**|[Error](describeattacklogs#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](describeattacklogs#err)| |
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
|**dataList**|[AttackLog[]](describeattacklogs#attacklog)| |
|**currentCount**|Integer|当前页数量|
|**totalCount**|Integer|实例总数|
|**totalPage**|Integer|总页数|
### <div id="attacklog">AttackLog</div>
|名称|类型|描述|
|---|---|---|
|**ip**|String|公网 IP 地址|
|**resourceType**|Integer|公网 IP 类型或绑定资源类型.<br><br>- 0: 未知类型<br><br>- 1: 弹性公网 IP(IP 为弹性公网 IP, 绑定资源类型未知)<br><br>- 10: 弹性公网 IP(IP 为弹性公网 IP, 但未绑定资源)<br><br>- 11: 云主机<br><br>- 12: 负载均衡<br><br>- 13: 原生容器实例<br><br>- 14: 原生容器 Pod<br><br>- 2: 云物理服务器<br><br>- 3: Web应用防火墙 IP<br><br>- 4: 托管区公网 IP<br>|
|**attackLogId**|String|攻击记录 ID|
|**startTime**|String|攻击开始时间, UTC 时间, 格式: yyyy-MM-dd'T'HH:mm:ssZ|
|**endTime**|String|攻击结束时间, UTC 时间, 格式: yyyy-MM-dd'T'HH:mm:ssZ|
|**cause**|Integer|触发原因.<br>- 0: 未知,<br>- 1: 四层,<br>- 2: 七层,<br>- 3: 四层和七层|
|**status**|Integer|状态. <br>- 0: 清洗完成<br>- 1: 清洗中<br>- 2: 黑洞中|
|**blackHole**|Boolean|是否黑洞|
|**peak**|Double|攻击流量峰值|
|**unit**|String|攻击流量峰值单位|
|**attackType**|String[]|攻击类型|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
