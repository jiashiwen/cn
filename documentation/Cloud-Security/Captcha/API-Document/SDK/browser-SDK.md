# 验证码SDK PC/M端接入

# 1、验证码接入步骤

## 1.1 加载sdk js文件

```
<script type="text/javascript" src="https://captcha-api-global.jdcloud.com/home/requireCaptcha.js"></script>
```

## 1.2 初始化验证码

```
let Jcap = {}
let option = {
    sessionId: '', 会话Id
    appId: '', // 应用Id
    language: '1', // 语言 1-中文简体 
    onSuccess: function(ret) {
        //验证成功后回调（ret.vt为后台需要再次验证的verifytoken）
    },
    onLoad: function(ret) {
        // 验证码初始化完毕时会被调用
    },
    onFailure: function(ret) {
        // sid失效，vt过期需重新申请sid，调用reset方法
        //验证失败后回调（接口异常）
    },
}
```


```
// 初始化验证码，此函数只需初始化一次，之后去重新创建请调用Jcap.create()
captchaLoadJS(option, (obj) => {
    Jcap = obj
})
```

**option参数说明：**

| 参数      | 说明                                                         | 类型        | 默认值 | 必填  |
| :-------- | :----------------------------------------------------------- | :---------- | :----- | :---- |
| sessionId | 服务端返回的sid                                              | String      | ''     | true  |
| appId     | 接入的应用Id                                                 | Number      | 无     | true  |
| onSuccess | 验证通过回调，验证成功时将后台校验token发回服务端验证，否则获取错误信息 | Function(e) | ()=>{} | true  |
| onLoad    | 验证码初始化完成回调                                         | Function(e) | ()=>{} | false |
| onFailure | 验证失败回调，例如sessionid过期，需要从服务端申请新的sessionid创建验证码 | Function(e) | ()=>{} | true  |

**回调返回参数ret说明：**

| 参数   | 说明                                                         | 类型   |
| :----- | :----------------------------------------------------------- | :----- |
| code   | 验证码返回的错误码，0为成功，其他均为失败，各错误码需要进行的处理参见下表 | Number |
| msg    | 错误信息                                                     | String |
| s_code | 后台详细错误代号(code非0时存在)                              | Number |
| vt     | code为0时存在，后台再次校验的verify_token值                  | String |

**错误代码、错误代码解释及建议处理逻辑：**

| 错误代码(code) | 错误代码解释(msg)    | 建议处理逻辑                             |
| :------------- | :------------------- | :--------------------------------------- |
| 错误代码(code) | 错误代码解释(msg)    | 建议处理逻辑                             |
| 0              | 成功                 | 不用处理                                 |
| 16801          | 参数无效             | 不用处理                                 |
| 16802          | 服务异常             | 不用处理                                 |
| 16803          | 请求太频繁           | 不用处理                                 |
| 16807          | 验证码未通过         | 不用处理                                 |
| 16808          | sessionid过期失效    | 申请新的sessionid，根据各端api重置验证码 |
| 16809          | verify_token过期失效 | 申请新的sessionid，根据各端api重置验证码 |

## 1.3 创建验证码

需要创建验证码时调用，显示验证码:

```
Jcap.create() // captchaLoadJS执行后，可通过create创建验证码；也可传入参数用于创建新验证码，如 create({}) 或 create({sessionId: sessionid})
```

**Jcap对象方法说明：**

| 方法名           | 解释                                                         |
| :--------------- | :----------------------------------------------------------- |
| create()         | `captchaLoadJS执行后，可通过create创建验证码；也可传入参数用于创建新验证码` |
| getSessionId()   | 当前使用的sessionid                                          |
| reset(sessionid) | 使用新的sessionid重置验证码，用于sessionid过期时             |

# 接入示例代码 test.html

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
</head>
<body>
<h1>京东云验证码PC端SDKDemo</h1>
<br>
<button onclick="initJcap()">测试一下</button>
<script src="http://apps.bdimg.com/libs/jquery/1.9.1/jquery.js"></script> 
<script type="text/javascript" src="https://captcha-api-global.jdcloud.com/home/requireCaptcha.js"></script>
<script>
    function initJcap() {
        var appid = 12345678 //应用id，请勿直接使用，从界面获取
        var sceneid = 12345678 //场景id，请勿直接使用，从界面获取
        var sid = 'xxxxx' //会话id，调用getsessionid接口获取
        let option = {
            sessionId: '', //会话Id，从服务端获取
            appId: '',     //应用Id
            onSuccess: function(ret) {
                //验证成功后回调（ret.vt为后台需要再次验证的vt）
                console.log("onSuccess callback", ret)
            },
            onLoad: function(ret) {
                // 验证码初始化完毕时会被调用
                console.log("onLoad callback", ret)
            },
            onFailure: function(ret) {
                // sid失效，vt过期需重新申请sid，调用reset方法
                // 验证失败后回调（接口异常）
                console.log("onFailure callback", ret)
            },
        }
        option.appId = appid
        option.sessionId = sid

        // 创建验证码
        let Jcap = {}
        captchaLoadJS(option, (obj) => {
            Jcap = obj
        })
        console.log(Jcap, typeof Jcap.create);
        if (Jcap && typeof Jcap.create === 'function') {
            Jcap.create()
        }
    } 
    
</script>
</body>
</html>
```

