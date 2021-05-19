# 服务端 API 汇总

**更新时间：2020-08-19**

## 接口列表
---

### <a name='1'></a>1\.获取直播open_id 及 直播token

获取使用**互动娱乐SDK**需要的live_open_id及live_token

###### URL
> [/open/v0/thGetToken]()

###### 支持格式
> 表单参数

###### HTTP请求方式
> POST （application/x-www-form-urlencoded）

###### 请求参数
> 
| 参数 | 必选 | 类型 | 说明 |
| -----  | -------| -----| -----                    |
|app_id    |true    |string   |LinkV 分配的app_id|
|nonce_str    |true    |string   |随机字符串，前八位和后八位为随机字符串，中间为秒级时间戳|
|sign    |true    |string   |生成的签名串 [签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)|
|userId    |true    |string|用户 Id，支持大小写英文字母、数字、部分特殊符号 + = - _ 的组合方式，最大长度 64 字节。是用户在 App 中的唯一标识，必须保证在同一个 App 内不重复，重复的用户 Id 将被当作是同一用户。                          |
|aid    |true    |string   |用户唯一设备id(非物理设备id)|
|name    | true/false    |string   |用户名称，最大长度 128 字节。用来在 开播时显示用户的名称。（注册必传）|
|portraitUri    |true/false    |string   |用户头像 URI，最大长度 1024 字节。（注册必传）|
|email    |false    |string   |用户邮箱|
|countryCode    |false    |string   |用户国家码 如：US|
|birthday    |false    |string   |用户生日。2010-01-01|
|sex    |false    |string   |性别 -1：未知，1：男，0：女|


###### 返回字段
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|status   |int    |返回结果状态。200：正常。   |
|msg  |string | 返回状态信息                      |
|data |object |                         |
|&nbsp;&nbsp;&nbsp;&nbsp;token |string |    用户 live_token，可以保存应用内，长度在 256 字节以内。                     |
|&nbsp;&nbsp;&nbsp;&nbsp;userId |string |      用户 Id，与参数 userId 相同。                   |
|&nbsp;&nbsp;&nbsp;&nbsp;aid |string |      用户 aid，与参数 aid 相同。                   |
|&nbsp;&nbsp;&nbsp;&nbsp;openId |string |   LinkV互动娱乐生成的唯一live_open_id 。用户开播校验                 |

###### 返回示例
``` json
// success
{
    "data": {
        "token": "asdsaddfa3234234ada2adsf",
        "userId": "534961119",
        "aid": "dsafdsf23wadfaad",
        "openId": "115213496111983232934",
    },
    "msg": "",
    "status": "200"
}
```
```json
// error
{
    "status": "403",
    "msg": "sign err",
    "data": []
}
```

###### 错误码说明
|错误码|描述 | 解决方案|
| --- | --- | --- |
|  400 | 参数错误 | 确认必传参数是否缺少 |
|  400 | 参数长度错误 | 确认userId长度是否超过64位 |
|  403 | 签名错误 | 参照[签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)进行签名生成 |
| 500 | 系统错误 | 联系我们 |

---

### <a name='2'></a>2\.完成订单

充值完成增加金币

###### URL
> [/open/finanv0/orderSuccess]()

###### 支持格式
> 表单参数

###### HTTP请求方式
> POST （application/x-www-form-urlencoded）

###### 请求参数
> 
| 参数 | 必选 | 类型 | 说明 |
| -----  | -------| -----| -----                    |
|app_id|true|string|LinkV 分配的live_app_id|
|nonce_str|true|string|随机字符串，前八位和后八位为随机字符串，中间为秒级时间戳|
|sign|true|string|生成的签名串 [签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)|
|uid|true|string| 通过接口获取到的 live_open_id |
|request_id|true|string|32位长度随机字符串，用来进行幂等。推荐算法(uuid)|
|type|true|string|1.订单增加金币;2.订单删除金币|
|value|true|string|要变化的金币数量|
|order_id|true|string|通过**互动娱乐SDK**获取的**order_id**|
|expriation|true|int|过期时间戳 例: $expiration = (time() / 86400 + 91) * 86400 ;|
|money|true|int|充值美元(单位/分)|
|channel|true|string|LinkV 分配的live_app_alias|
|platform|true|string|支付平台：h5;ios;android|


###### 返回字段
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|status   |int    |返回结果状态。200：正常。   |
|msg  |string | 返回状态信息                      |
|data |object |                         |
|&nbsp;&nbsp;&nbsp;&nbsp;tokens |string |用户剩余金币|

###### 返回示例
``` json
// success
{
    "data": {
        "tokens": "123",
    },
    "msg": "",
    "status": "200"
}
```
```json
// error
{
    "status": "403",
    "msg": "sign err"
}
```

###### 错误码说明
|错误码|描述 | 解决方案|
| --- | --- | --- |
|  400 | 参数错误 | 确认必传参数是否缺少 |
|  400 | 参数长度错误 | 确认userId长度是否超过64位 |
|  403 | 签名错误 | 参照[签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)进行签名生成 |
| 500 | 系统错误 | 联系我们 |

---

### <a name='3'></a>3\.修改金币

充值完成增加金币

###### URL
> [/open/finanv0/changeGold]()

###### 支持格式
> 表单参数

###### HTTP请求方式
> POST （application/x-www-form-urlencoded）

###### 请求参数
> 
| 参数 | 必选 | 类型 | 说明 |
| -----  | -------| -----| -----                    |
|app_id|true|string|LinkV 分配的live_app_id|
|nonce_str|true|string|随机字符串，前八位和后八位为随机字符串，中间为秒级时间戳|
|sign|true|string|生成的签名串 [签名生成](k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)|
|uid|true|string| 通过接口获取到的 live_open_id |
|request_id|true|string|32位长度随机字符串，用来进行幂等。推荐算法(uuid)|
|type|true|string|1.订单增加金币;2.订单删除金币|
|value|true|string|要变化的金币数量|
|expriation|true|int|过期时间戳 例: $expiration = (time() / 86400 + 91) * 86400 ;|
|reason|false|string|本次操作原因|


###### 返回字段
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|status   |int    |返回结果状态。200：正常。   |
|msg  |string | 返回状态信息                      |

###### 返回示例
``` json
// success
{
    "msg": "",
    "status": "200"
}
```
```json
// error
{
    "status": "403",
    "msg": "sign err"
}
```

###### 错误码说明
|错误码|描述 | 解决方案|
| --- | --- | --- |
|  400 | 参数错误 | 确认必传参数是否缺少 |
|  400 | 参数长度错误 | 确认userId长度是否超过64位 |
|  403 | 签名错误 | 参照[签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)进行签名生成 |
| 500 | 系统错误 | 联系我们 |

---

## <a name='4'></a>4\.查询金币

获取用户金币余额

###### URL
> [/open/finanv0/getUserTokens]()

###### 支持格式
> 表单参数

###### HTTP请求方式
> POST （application/x-www-form-urlencoded）

###### 请求参数
> 
| 参数 | 必选 | 类型 | 说明 |
| -----  | -------| -----| -----                    |
|app_id|true|string|LinkV 分配的live_app_id|
|nonce_str|true|string|随机字符串，前八位和后八位为随机字符串，中间为秒级时间戳|
|sign|true|string|生成的签名串 [签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)|
|uid|true|string| 通过接口获取到的 live_open_id |


###### 返回字段
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|status   |int    |返回结果状态。200：正常。   |
|msg  |string | 返回状态信息                      |
|data |object |                         |
|&nbsp;&nbsp;&nbsp;&nbsp;tokens |string |用户剩余金币|

###### 返回示例
``` json
// success
{
    "data": {
        "tokens": "123",
    },
    "msg": "",
    "status": "200"
}
```
```json
// error
{
    "status": "403",
    "msg": "sign err"
}
```

###### 错误码说明
|错误码|描述 | 解决方案|
| --- | --- | --- |
|  400 | 参数错误 | 确认必传参数是否缺少 |
|  400 | 参数长度错误 | 确认userId长度是否超过64位 |
|  403 | 签名错误 | 参照[签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)进行签名生成 |
| 500 | 系统错误 | 联系我们 |

---
