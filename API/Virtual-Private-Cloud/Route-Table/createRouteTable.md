# createRouteTable


## 描述
创建路由表

## 请求方式
POST

## 请求地址
https://vpc.jdcloud-api.com/v1/regions/{regionId}/routeTables/

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |Region ID|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**vpcId**|String|True| |路由表所属的私有网络ID|
|**routeTableName**|String|True| |路由表名称，只允许输入中文、数字、大小写字母、英文下划线“_”及中划线“-”，不允许为空且不超过32字符。|
|**description**|String|False| |描述,​ 允许输入UTF-8编码下的全部字符，不超过256字符|


## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](createRouteTable#user-content-result)|返回结果|
|**requestId**|String|请求ID|

### <div id="user-content-result">Result</div>
|名称|类型|描述|
|---|---|---|
|**routeTableId**|String|路由表ID|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|invalid parameter|
|**404**|Resource not found|
|**500**|Internal server error|

## 请求示例
调用方法、签名算法及公共请求参数请参考[京东云OpenAPI公共说明](https://docs.jdcloud.com/common-declaration/api/introduction)。
- 请求示例：在vpc-2wzrfdesf下创建名称为“自建路由表”的路由表

POST
```
/v1/regions/cn-north-1/routeTables/
{
  "vpcId":"vpc-2wzrfdesf",
  "routeTableName":"自建路由表",
  "description":"路由表测试"
}

```

## 返回示例
```
{
    "requestId": "c41qtk73tdsvpwbq8504b906qcnwdcqo", 
    "result": {
        "routeTableId": "rtb-olajkrx4xr"
    }
}
```
