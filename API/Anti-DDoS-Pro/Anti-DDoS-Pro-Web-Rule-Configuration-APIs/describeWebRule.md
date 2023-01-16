# describeWebRule


## 描述
查询网站类规则

## 请求方式
GET

## 请求地址
https://ipanti.jdcloud-api.com/v1/regions/{regionId}/instances/{instanceId}/webRules/{webRuleId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |区域 ID, 高防不区分区域, 传 cn-north-1 即可|
|**instanceId**|String|True| |高防实例 Id|
|**webRuleId**|String|True| |网站规则 Id|

## 请求参数
无


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](describewebrule#result)| |
|**requestId**|String| |
|**error**|[Error](describewebrule#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](describewebrule#err)| |
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
|**data**|[WebRule](describewebrule#webrule)| |
### <div id="webrule">WebRule</div>
|名称|类型|描述|
|---|---|---|
|**id**|String|规则 Id|
|**instanceId**|String|实例 Id|
|**domain**|String|子域名|
|**cname**|String|规则的 CNAME|
|**cnameStatus**|Integer|CNAME 解析状态, 0: 解析异常, 1: 解析正常|
|**serviceIp**|String|该规则使用中的高防 IP|
|**serviceIpConfig**|[ServiceIpConfig](describewebrule#serviceipconfig)|已配置的高防 IP 列表|
|**protocol**|[WebRuleProtocol](describewebrule#webruleprotocol)| |
|**customPortStatus**|Integer|是否为自定义端口号, 0: 为默认, 1: 为自定义|
|**port**|Integer[]|HTTP 协议的端口号, 如 80,81|
|**httpsPort**|Integer[]|HTTPS 协议的端口号, 如 443,8443|
|**httpOrigin**|Integer|是否开启 HTTP 回源, 0: 为不开启, 1: 为开启, 当勾选 HTTPS 时可以配置该属性|
|**status**|Integer|0: 防御状态, 1: 回源状态|
|**originType**|String|回源类型: A 或者 CNAME|
|**originAddr**|[OriginAddrItem[]](describewebrule#originaddritem)|回源域名, originType 为 A 时返回该字段|
|**originDomain**|String|回源域名, originType 为 CNAME 时返回该字段|
|**onlineAddr**|String[]|备用的回源地址列表, 为一个域名或者多个 IP 地址|
|**httpCertStatus**|Integer|证书状态. <br>- 0: 异常<br>- 1: 正常<br>- 2: 证书未上传|
|**certId**|String|证书 Id, (废弃, 绑定证书信息通过 certs 字段查看)|
|**certName**|String|证书名称, (废弃, 绑定证书信息通过 certs 字段查看)|
|**httpsCertContent**|String|证书内容, (废弃, 绑定证书信息通过 certs 字段查看)|
|**httpsRsaKey**|String|证书私钥, (废弃, 绑定证书信息通过 certs 字段查看)|
|**bindCerts**|[Cert[]](describewebrule#cert)|网站规则绑定证书信息|
|**forceJump**|Integer|是否开启 HTTPS 强制跳转, 当 protocol 为 HTTP_HTTPS 时可以配置该属性<br>- 0: 不强跳<br>- 1: 开启强跳|
|**algorithm**|String|转发规则. <br>- wrr: 带权重的轮询<br>- rr:  不带权重的轮询<br>- sh:  源地址hash|
|**ccStatus**|Integer|CC 状态, 0: CC 关闭, 1: CC 开启|
|**webSocketStatus**|Integer|webSocket 状态, 0: 关闭, 1: 开启|
|**blackListEnable**|Integer|黑名单状态, 0: 关闭, 1: 开启|
|**whiteListEnable**|Integer|白名单状态, 0: 关闭, 1: 开启|
|**geoRsRoute**|[GeoRsRoute[]](describewebrule#georsroute)|按区域分流回源配置|
|**enableKeepalive**|String|是否开启回源长连接, protocol 选项开启 https 时生效, 可取值<br>- on: 开启<br>- off: 关闭|
|**httpVersion**|String|http 版本, protocol 选项开启 https 时生效, 可取值 http1 或 http2|
|**sslProtocols**|String[]|SSL协议类型, protocol 选项开启 https 时生效, 可取值SSLv2,SSLv3,TLSv1.0,TLSv1.1,TLSv1.2|
|**suiteLevel**|String|加密套件等级, protocol 选项开启 https 时生效, 可取值<br>- low: 低级<br>- middle: 中级<br>- high：高级<br>- custom：自定义|
|**userSuiteLevel**|String[]|自定义加密套件等级, suiteLevel 为 custom 是有效|
|**jsFingerprintEnable**|Integer|是否允许在 response 中插入 JS, 0: 关闭, 1: 开启|
|**jsFingerprintScope**|Integer|JS 指纹生效范围, 0: 所有页面, 1: 已配置的自定义页面|
|**ccCustomStatus**|Integer|CC自定义规则总开关, 0: 关闭, 1: 开启|
|**enableHealthCheck**|Integer|健康检查开关, 0: 关闭, 1: 开启|
|**proxyConnectTimeout**|Integer|回源连接超时时长, 单位 秒|
|**enableUnderscores**|Integer|请求头支持下划线, 0: 关闭, 1: 开启|
### <div id="georsroute">GeoRsRoute</div>
|名称|类型|描述|
|---|---|---|
|**geo**|String|要设置的区域编码, 查询 <a href='http://docs.jdcloud.com/anti-ddos-pro/api/describeWebRuleRSGeoAreas'>describeWebRuleRSGeoAreas</a> 接口获取可设置的地域编码|
|**rsAddr**|String[]|对应区域的回源IP的列表|
### <div id="cert">Cert</div>
|名称|类型|描述|
|---|---|---|
|**certId**|String|证书id|
|**certName**|String|证书名称|
### <div id="originaddritem">OriginAddrItem</div>
|名称|类型|描述|
|---|---|---|
|**ip**|String|回源ip|
|**weight**|Integer|权重|
|**inJdCloud**|Boolean|是否为京东云内公网ip|
### <div id="webruleprotocol">WebRuleProtocol</div>
|名称|类型|描述|
|---|---|---|
|**http**|Boolean|http 协议|
|**https**|Boolean|https 协议|
### <div id="serviceipconfig">ServiceIpConfig</div>
|名称|类型|描述|
|---|---|---|
|**serviceIps**|[ServiceIpConfigItem[]](describewebrule#serviceipconfigitem)|已配置的高防IP列表|
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
