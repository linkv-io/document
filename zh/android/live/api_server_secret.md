# 签名生成

**更新时间：2020-08-20**

## 1.准备

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


## 2.构造签名串

我们希望接入方的技术开发人员按照当前文档约定的规则构造签名串。LinkV会使用同样的方式构造签名串。如果接入方构造签名串的方式错误，将导致签名验证不通过。下面先说明签名串的具体格式。

签名串是一个32位长度的字符串。

## 3.计算签名值

### 第一步：拼接字符串（原串）
设所有发送或者接收到的数据为集合M，将nonce_str参数随机字符串加入，将集合M内非空参数值的参数按照参数名ASCII码从小到大排序（字典序），使用URL键值对的格式（即key1=value1&key2=value2…），拼接成字符串stringA。

特别注意以下重要规则：
- 参数名ASCII码从小到大排序（字典序）；
- 如果参数的值为空不参与签名；
- 参数名区分大小写；
- nonce_str为随机字符串，前八位和后八位为随机字符串，中间为秒级时间戳
  - 例子： 661a3893156378771361c1a022    其中前后八位为随机字符串，中间为秒级时间戳：1563787713
  - **接口会校验时间戳，5分钟内位有效校验时间，如果超过5分钟则校验失败**

假设传送的参数如下：
```sh
"app_id": "LM6000101140927991745433"

"params1": "t1"

"a123": ""
```

对参数按照key=value的格式，并按照参数名ASCII字典序排序如下：
```sh
StringA = "app_id=LM6000101140927991745433&nonce_str=24dcadd615637909402f4877b0&param1=t1"
```

### 第二步：生成签名串
签名校验算法为md5，在stringA最后拼接上key=live_app_secret得到stringSignTemp字符串，并对stringSignTemp进行MD5运算，转为小写，生成sign签名

假设原串如下：
```sh
StringA = “app_id=LM6000101140927991745433&nonce_str=24dcadd615637909402f4877b0&param1=t1”
```

拼接API密钥(live_app_secret)
```sh
StringA2 = "app_id=LM6000101140927991745433&nonce_str=24dcadd615637909402f4877b0&param1=t1&key=live_app_secret"

sign = Tolower(md5(StringA2)) = "864070ea8d99310992fbbb1d8579f674"
```

## 4.示例代码

Go
```go
...

func genRandomString() string {
	nLen := 16
	var container string
	var str = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890"
	b := bytes.NewBufferString(str)
	length := b.Len()
	bigInt := big.NewInt(int64(length))
	for i := 0; i < nLen; i++ {
		randomInt, _ := rand.Int(rand.Reader, bigInt)
		container += string(str[randomInt.Int64()])
		if i == 7 {
			container += strconv.FormatInt(time.Now().Unix(), 10)
		}
	}
	return container
}

func genSign(params url.Values, md5Secret string) string {
	data := encode(params) + "&key=" + md5Secret
	md5Data := md5.Sum([]byte(data))
	return strings.ToLower(hex.EncodeToString(md5Data[:]))
}

func encode(v url.Values) string {
	if v == nil {
		return ""
	}
	var buf strings.Builder
	keys := make([]string, 0, len(v))
	for k := range v {
		keys = append(keys, k)
	}
	sort.Strings(keys)
	for _, k := range keys {
		vs := v[k]
		if buf.Len() > 0 {
			buf.WriteByte('&')
		}
		buf.WriteString(k)
		buf.WriteByte('=')
		buf.WriteString(vs[0])
	}
	return buf.String()
}

...

func ...(...) {
    ... 
	nonce := genRandomString()
	params.Add("nonce_str", nonce)
	params.Add("app_id", LiveAppKey)

	params.Add("userId", thirdUID)
	params.Add("aid", aID)

	if len(userName) > 0 {
		params.Add("name", userName)
	}

    params.Add("sign", genSign(params, LiveAppSecret))
    ...
}
```