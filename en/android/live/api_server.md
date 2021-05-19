# Server API Summary

**Update date：2020-08-19**

## The interface list
---

### <a name='1'></a>1\.Access to live open_id and Live token

Get use**Interactive entertainment SDK**need live_open_id and live_token

###### URL
> [/open/v0/thGetToken]()

###### Supported formats
> The form parameter

###### HTTP Request way
> POST （application/x-www-form-urlencoded）

###### Request parameters
> 
| Parameter | Required | Type | Description |
| -----  | -------| -----| -----                    |
|app_id    |true    |string   |LinkV distributed app_id|
|nonce_str    |true    |string   |Random string，The first eight digits and the last eight digits are random strings，the second time stamp in the middle|
|sign    |true    |string   |Generated signature string [Signature generated](?k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)|
|userId    |true    |string|User Id，supports the combination of upper and lower case Letters, Numbers, and partial special symbols + = - _ ，the maximum length is 64 bytes。It is the unique identifier of the user in the App. It must be guaranteed not to be repeated in the same App. Repeated user IDs will be regarded as the same user。                          |
|aid    |true    |string   |User's unique device id (non-physical device id)|
|name    | true/false    |string   |User name, the maximum length is 128 bytes. Used to display the user's name when the broadcast starts. (Registration must pass)|
|portraitUri    |true/false    |string   |User avatar URI, the maximum length is 1024 bytes. (Registration must pass)|
|email    |false    |string   |User email|
|countryCode    |false    |string   |User country code如：US|
|birthday    |false    |string   |User birthday。2010-01-01|
|sex    |false    |string   |Gender -1：Unknown，1：Male，0：Female|


###### Return Field
> 
|Return Field|Field Type|Description                              |
| -----   | ------| -----------------------------   |
|status   |int    |Return result status。200：Normal。   |
|msg  |string | Return status information                      |
|data |object |                         |
|&nbsp;&nbsp;&nbsp;&nbsp;token |string |    User live_token，can be stored in the application and the length is within 256 bytes.                     |
|&nbsp;&nbsp;&nbsp;&nbsp;userId |string |   User Id, the same as the parameter userId.                   |
|&nbsp;&nbsp;&nbsp;&nbsp;aid |string |      User aid，Same as parameter aid。                   |
|&nbsp;&nbsp;&nbsp;&nbsp;openId |string |   LinkV interactive entertainment generated the only live_open_id 。User broadcast verification                |

###### Return example
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

###### Error code description
|Error code|Description | Solution|
| --- | --- | --- |
|  400 | Parameter error | Confirm whether the required parameter is missing
|  400 |Parameter length error | Confirm whether the userId length exceeds 64 bits |
|  403 | Signature error | Refer[Signature created](?k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)to generate signature |
| 500 | System error | Contact us |

---

### <a name='2'></a>2\.Complete order

Add gold coins after recharge

###### URL
> [/open/finanv0/orderSuccess]()

###### Support format
> Form parameter

###### HTTP request method
> POST （application/x-www-form-urlencoded）

###### Request parameter
> 
| Parameters | Required | Type | Description |
| -----  | -------| -----| -----                    |
|app_id|true|string|LinkV distributed live_app_id|
|nonce_str|true|string|Random string, the first and last eight digits are random strings, and the second-level timestamp is in the middle|
|sign|true|string|Generated signature string [signature generated](?k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)|
|uid|true|string| Obtained live_open_id through the interface |
|request_id|true|string|32 bits length random string, used for idempotence. Recommendation algorithm
(uuid)|
|type|true|string|1.Order add coins;2.Order delete coins|
|value|true|string|The number of coins need to change|
|order_id|true|string|Obtain **order_id** through **Interactive entertainment SDK**|
|expriation|true|int|Expiration timestamp Example: $expiration = (time() / 86400 + 91) * 86400 ;|
|money|true|int|Top up USD (units/min)|
|channel|true|string|LinkV distributed live_app_alias|
|platform|true|string|Payment platform：h5;ios;android|


###### Return field
> 
|Return Field|Field Type|Description                              |
| -----   | ------| -----------------------------   |
|status   |int    |Return result status。200：Normal。   |
|msg  |string | Return status information                     |
|data |object |                         |
|&nbsp;&nbsp;&nbsp;&nbsp;tokens |string |User remaining coins|

###### Return example
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

###### Error code description
|Error code|Description | Solution
| --- | --- | --- |
|  400 | Parameter error | Confirm whether the required parameter is missing
|  400 | Parameter length error | Confirm whether the userId length exceeds 64 bits |
|  403 | Signature error | Refer[signature generated](?k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)to generate signature |
| 500 |  System error | Contact us |

---

### <a name='3'></a>3\.Modify coins


Add coins after recharge

###### URL
> [/open/finanv0/changeGold]()

###### Support format
> Form parameter

###### HTTP request method 
> POST （application/x-www-form-urlencoded）

###### Request parameter
> 
| Parameters | Required | Type | Description
| -----  | -------| -----| -----                    |
|app_id|true|string|LinkV distributed live_app_id|
|nonce_str|true|string|Random string, the first and last eight digits are random strings, and the second-level timestamp is in the middle|
|sign|true|string|Generated signature string [signature generated](k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)|
|uid|true|string| Obtained live_open_id through the interface  |
|request_id|true|string|32 bits length random string, used for idempotence. Recommendation algorithm(uuid)|
|type|true|string|1.Order add coins;2.Order delete coins|
|value|true|string|The number of coins need to change|
|expriation|true|int|Expiration timestamp Example: $expiration = (time() / 86400 + 91) * 86400 ;|
|reason|false|string|Reason for this operation|


###### Return field
> 
|Return Field|Field Type|Description                              |
| -----   | ------| -----------------------------   |
|status   |int    |Return result status。200：Normal。   |
|msg  |string | Return status information                     |

###### Return example
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

###### Error code description
|Error code|Description | Solution
| --- | --- | --- |
|  400 | Parameter error | Confirm whether the required parameter is missing
|  400 | Parameter length error | Confirm whether the userId length exceeds 64 bits |
|  403 | Signature error | Refer[signature generated](?k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)to generate signature |
| 500 |  System error | Contact us |

---

## <a name='4'></a>4\.Query coins

Get user coin balance

###### URL
> [/open/finanv0/getUserTokens]()

###### Support format
> Form parameter

###### HTTP request method 
> POST （application/x-www-form-urlencoded）

###### Request parameter
> 
| Parameters | Required | Type | Description
| -----  | -------| -----| -----                    |
|app_id|true|string|LinkV distributed live_app_id|
|nonce_str|true|string|Random string, the first and last eight digits are random strings, and the second-level timestamp is in the middle|
|sign|true|string|Generated signature string [signature generated](k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)|
|uid|true|string| Obtained live_open_id through the interface  |

###### Return field
> 
|Return Field|Field Type|Description                              |
| -----   | ------| -----------------------------   |
|status   |int    |Return result status。200：Normal。   |
|msg  |string | Return status information                     |
|data |object |                         |
|&nbsp;&nbsp;&nbsp;&nbsp;tokens |string |User remaining coins|

###### Return example
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

###### Error code description
|Error code|Description | Solution
| --- | --- | --- |
|  400 | Parameter error | Confirm whether the required parameter is missing
|  400 | Parameter length error | Confirm whether the userId length exceeds 64 bits |
|  403 | Signature error | Refer[signature generated](?k=kKjoJrYp&m=android&p=%252Fen%252Fios%252Flive%252Fapi_server_secret.md)to generate signature |
| 500 |  System error | Contact us |

---
