# 服务端 对接

**更新时间：2020-08-20**

## 1\.准备

在进行下面的步骤之前，需要先获取live_app_key与live_app_secret两个字符串。
- 确保从开发者平台得到的app_id及app_secret(**server版本**)的正确性及完整性
- 使用[动态链接库(0.0.4)](https://dl.linkv.io/static/server/0.0.4/libdecrypt.so)进行解密获得live_app_key及live_app_secret

c 头文件
```sh
#ifndef DECRYPT_LIBRARY_H
#define DECRYPT_LIBRARY_H
#include <stdint.h>
char *decrypt(char *appID, char *cipherText);
void release(char *plainText);
#endif //DECRYPT_LIBRARY_H
```

## 2\.构造auth串

我们希望接入方的技术开发人员按照当前文档约定的规则构造auth串。LinkV会使用同样的方式构造auth串。如果接入方构造auth串的方式错误，将导致验证不通过。下面先说明签名串的具体格式。

auth 为hmac-sha1加密串

expire 为当前秒级时间戳

## 3\.生成auth&expire值
通过准备环节，获取到 rtc_app_id 与 rtc_app_key

假设生成的参数如下：
```sh
expire="1597141347"
rtc_app_id="rtcAppID"
rtc_app_key ="rtcAppKey"
```

将 rtc_app_id 与 expire 链接后作为原串。对原串进行hmac-sha1编码，密钥为rtc_app_key 得到auth
```sh
StringA = "rtcAppID1597141347"

auth = hex(hmac-sha1(StringA,rtc_app_key))
```


## 4\.示例代码

Go
```go
...

func GenRTCAuth() (string, string, string) {
	expireTS := strconv.FormatInt(time.Now().Unix(), 10)
	data := o.GetConfig().AppID + expireTS
	return o.GetConfig().AppID, hex.EncodeToString(hmacSha1([]byte(o.GetConfig().AppKey), []byte(data))), expireTS
}

...
```