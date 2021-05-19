# Signature generation

**Update Date：2020-08-20**

## 1.Prepare

Before proceeding to the following steps，Need to get the two strings live_app_key and live_app_secret first。
- Ensure the correctness and integrity of the app_id and app_secret (**server version**) obtained from the developer platform
- Use[Dynamic link library(0.0.4)](https://dl.linkv.io/static/server/0.0.4/libdecrypt.so)to decrypt and get live_app_key and live_app_secret

c Head File
```sh
#ifndef DECRYPT_LIBRARY_H
#define DECRYPT_LIBRARY_H
#include <stdint.h>
char *decrypt(char *appID, char *cipherText);
void release(char *plainText);
#endif //DECRYPT_LIBRARY_H
```


## 2.Construct signature string

We hope that the technical developers of the accessing party will construct the signature string according to the rules agreed in the current document.LinkV will use the same method to construct the signature string.
If the access party constructs the signature string in a wrong way, the signature verification will fail.The following describes the specific format of the signature string.


The signature string is a 32-bit string.

## 3.Calculate signature value

### The first step: splicing strings (original string)
Set all sent or received data as set M, add the nonce_str parameter random string, and sort the non-empty parameter values ​​in set M from small to large according to the ASCII code of the parameter name (dictionary order), using URL key-value pairs Format (ie key1=value1&key2=value2...), spliced ​​into a string stringA。


Pay special attention to the following important rules：
- Parameter name ASCII code sorted from small to large (dictionary order)；
- If the parameter value is empty, it will not participate in the signature；
- Parameter names are case sensitive；
- nonce_str is a random string, the first and last eight digits are random strings, and the second-level timestamp is in the middle
  - Example： 661a3893156378771361c1a022    The first and last eight digits are random strings, and in the middle is a second-level stamp：1563787713
  - **The interface will verify the timestamp, the valid verification time is within 5 minutes, if it exceeds 5 minutes, the verification will fail**


Assume that the transmitted parameters are as follows：
```sh
"app_id": "LM6000101140927991745433"

"params1": "t1"

"a123": ""
```

The parameters are in the format of key=value and sorted in ASCII dictionary order as follows：
```sh
StringA = "app_id=LM6000101140927991745433&nonce_str=24dcadd615637909402f4877b0&param1=t1"
```

### Step Two: Generate signature string
The signature verification algorithm is md5. At the end of stringA, splicing key=live_app_secret to get stringSignTemp string, and perform MD5 operation on stringSignTemp, convert it to lowercase, and generate sign signature

Suppose the original string is as follows：
```sh
StringA = “app_id=LM6000101140927991745433&nonce_str=24dcadd615637909402f4877b0&param1=t1”
```

Splicing API key(live_app_secret)
```sh
StringA2 = "app_id=LM6000101140927991745433&nonce_str=24dcadd615637909402f4877b0&param1=t1&key=live_app_secret"

sign = Tolower(md5(StringA2)) = "864070ea8d99310992fbbb1d8579f674"
```

## 4.Sample code

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