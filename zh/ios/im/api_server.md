# 服务端 API 汇总

**更新时间：2020-10-22**

## 接口列表
---

### <a name='1'></a>1\.获取IM token

获取使用**IM SDK**需要的im_token

###### URL
> [/api/rest/getToken]()

###### 支持格式
> 表单参数

###### HTTP请求方式
> POST （application/x-www-form-urlencoded）

###### 请求header
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|appId |string |   LinkV 分配的 im_app_id                 |
|appkey |string |    LinkV 分配的 im_app_key                     |
|nonce   |string    |随机字符串   |
|cmimToken  |string | 参照[签名生成cmimToken]()进行签名生成                      |
|sign |string |       参照[签名生成sign]()进行签名生成              |
|timestamp |string |      秒级时间戳                   |
|appUid |string |      用户 Id，支持大小写英文字母、数字、部分特殊符号 + = - _ 的组合方式，最大长度 64 字节。是用户在 App 中的唯一标识，必须保证在同一个 App 内不重复，重复的用户 Id 将被当作是同一用户。                    |
|signature |string |   与 sign 一致                 |

###### 请求参数
> 
| 参数 | 必选 | 类型 | 说明 |
| -----  | -------| -----| -----                    |
|userId    |true    |string|用户 Id，支持大小写英文字母、数字、部分特殊符号 + = - _ 的组合方式，最大长度 64 字节。是用户在 App 中的唯一标识，必须保证在同一个 App 内不重复，重复的用户 Id 将被当作是同一用户。                          |


###### 返回字段
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|code   |string    |标识是否成功，200表示成功，其余失败   |
|userId   |string    |请求时传递的用户Id   |
|token  |string | token                      |

###### 返回示例
``` json
// success
{
  "code": "200", // 标识是否成功，200表示成功，其余失败
  "userId": "738131192624578560",
  "token": "hamif02795fce736993c96be32c31daa"
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

> 该接口与其他接口请求头不同

###### 错误码说明
|错误码|描述 | 解决方案|
| --- | --- | --- |
|  400 | 参数错误 | 确认必传参数是否缺少 |
|  401 | 签名错误 | 参照[签名生成]()进行签名生成 |
| 500 | 系统错误 | 联系我们 |
|  602 | appkey无效 | 联系我们 |

---

### <a name='2'></a>2\.单聊消息发送

发送1 v 1聊天消息

###### URL
> [/api/rest/message/converse/pushConverseData]()

###### 支持格式
> 表单参数

###### HTTP请求方式
> POST （application/x-www-form-urlencoded）

###### 请求header
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|appId   |string    |LinkV 分配的 im_app_id   |
|appKey  |string | LinkV 分配的 im_app_key                      |
|cmimToken |string |       通过[获取IM token]() 得到的im_token             |
|timestamp |string |    秒级时间戳                     |
|nonce |string |      随机数                   |
|sign |string |      参照[签名生成](?k=kKjoJrYp&m=android&p=%252Fzh%252Fios%252Flive%252Fapi_server_secret.md)进行签名生成                    |

###### 请求参数
> 
| 参数 | 必选 | 类型 | 说明 |
| -----  | -------| -----| -----                    |
|appId|true|string|LinkV 分配的im_app_id|
|fromUserId|true|string| 发送用户标识 |
|toUserId|true|string| 发送用户标识 |
|content|true|string|消息内容|
|toUserAppid|false|string|LinkV 分配的im_app_id|
|toUserExtSysUserId|false|string|接收方外部系统用户id|
|isCheckSensitiveWords|false|string|是否敏感词过滤 1：过滤，0:不过滤。默认：1|

###### 返回字段
> 
|返回字段|字段类型|说明                              |
| -----   | ------| -----------------------------   |
|code   |int    |返回结果状态。200：正常。   |
|msg  |string | 返回状态信息                      |
|&nbsp;&nbsp;&nbsp;&nbsp;tokens |string |用户剩余金币|

###### 返回示例
``` json
// success
{
    "msg": "成功",
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

### <a name='3'></a>3\.事件消息发送

充值完成增加金币

###### URL
> [/api/rest/sendEventMsg]()

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
