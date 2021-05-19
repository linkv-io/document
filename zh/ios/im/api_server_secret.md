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

**cmimtoken**串是一个32位长度的字符串。

**sign**串是一个40位长度的字符串。

## 3.计算签名值

### cmimtoken 签名计算

#### 第一步：拼接字符串（原串）
设所有发送或者接收到的数据为集合M，将集合M内非空参数值的参数的值按照ASCII码从小到大排序（字典序）（即value1value2…），拼接成字符串stringA。

特别注意以下重要规则：
- 参数名ASCII码从小到大排序（字典序）；

假设传送的参数如下：
```sh
appSecret="a8797322c9067852fec8309fa256c339"
timestamp ="1597141347"
nonce ="84469366"
```

按照参数的值按照ASCII字典序排序如下：
```sh
1597141347
84469366
a8797322c9067852fec8309fa256c339

StringA = "159714134784469366a8797322c9067852fec8309fa256c339"
```

#### 第二步：生成签名串
签名校验算法为md5，转为小写，生成cmimtoken签名

假设原串如下：
```sh
StringA = "159714134784469366a8797322c9067852fec8309fa256c339"
```

生成cmimtoken签名
```sh
cmimtoken = Tolower(md5(StringA2)) = "0b45ae8ee88db1cee3f9f4fa1d9d3276"
```

### sign 签名计算

#### 第一步：拼接字符串（原串）
将 appId,appKey,timestamp,nonce 通过 "|" 竖号字符连接，通过SHA-1 散列后的字符串 ，转为大


假设传送的参数如下：
```sh
appId="linkv"
appKey="2q3f9i"
timestamp ="1597141347"
nonce ="84469366"
```

#### 第二步：生成签名串
签名校验算法为sha-1，转为大写，生成sign签名

假设原串如下：
```sh
StringA = "linkv|2q3f9i|1597141347|84469366"
```

生成sign签名
```sh
sign = Toupper(hex(sha1(StringA2))) = "E28F778E4FB130C115EDCBC2E444CA5DB817724D"
```

## 4.示例代码

Go
```go
...

func genRandomString(nLen int) string {
	var container string
	var str = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890"
	b := bytes.NewBufferString(str)
	length := b.Len()
	bigInt := big.NewInt(int64(length))
	for i := 0; i < nLen; i++ {
		randomInt, _ := rand.Int(rand.Reader, bigInt)
		container += string(str[randomInt.Int64()])
	}
	return container
}

func genGUID() string {
	return genRandomString(9) + "-" + genRandomString(4) + "-" + genRandomString(4) + "-" + genRandomString(12)
}

func getTimestampS() string {
	t := time.Now()
	return strconv.FormatInt(t.Unix(), 10)
}

...

func ...(...) {
    ... 
	nonce := genGUID()
	timestamp := getTimestampS()


	arr := []string{nonce, timestamp, o.GetConfig().AppSecret}
	sort.Strings(arr)
	md5Data := md5.Sum([]byte(strings.Join(arr, "")))
	cmimToken := strings.ToLower(hex.EncodeToString(md5Data[:]))

	sha1Data := sha1.Sum([]byte(o.GetConfig().AppID + "|" + o.GetConfig().AppKey + "|" + timestamp + "|" + nonce))
	sign := strings.ToUpper(hex.EncodeToString(sha1Data[:]))
    ...
}
```