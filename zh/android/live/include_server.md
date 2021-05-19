# 服务端集成

**更新时间：2020-08-19**

LiveMe 社交娱乐服务端SDK目前支持Go、PHP、Python、Node等主流服务端语言。

## <a name='1'></a>1、 Go SDK 集成

##### 请确保满足以下开发环境：

- Go 1.8 或以上版本

##### 获取
登陆 https://github.com/linkv-io/go-sdk 查看最新版本号，替换如下指令中的版本号

```sh
go get github.com/linkv-io/go-sdk@v0.0.0
```

> 请不要使用master分之，该版本还未进过严格测试，稳定性未得到保障
>

##### 使用
```go
// 开发者平台 获取的app_id
appID := ""
// 开发者平台 获取的app_secret
appSecret := ""
// http请求等待时间 单位(s)
httpTimeout := 30
// http请求池内数量
httpPoolSize := 10
if err := linkv.Init(appID, appSecret, httpTimeout, httpPoolSize); err != nil {
    fmt.Println(err)
    return
}

```
> 请合理设置**超时时间**
> 
> 请合理设置**请求池**数量，频率异常可能会触发攻击检测
>

## <a name='2'></a>2、 Python3 SDK 集成

##### 请确保满足以下开发环境：

- Python 3.5
- Python 3.6
- Python 3.7
- Python 3.8

##### 获取
登陆 https://github.com/linkv-io/python-sdk 下载最新版本

##### 安装

```sh
cd python-sdk

python setup.py build

python setup.py install --record log # 保留安装记录 卸载时需要
```

> 请不要使用master分之，该版本还未进过严格测试，稳定性未得到保障
>

##### 卸载
```sh
cd python-sdk
cat log |xargs rm -rf 
rm -rf build dist linkv_sdk.egg-info log
```

##### 使用
```python
// 开发者平台 获取的app_id
app_id = ''
// 开发者平台 获取的app_secret
app_secret = ''
// http请求池内数量
pool_size = 10
if not linkv_sdk.init(app_id, app_secret, pool_size=pool_size):
    return
```
> 请合理设置**请求池**数量，频率异常可能会触发攻击检测
>

## <a name='3'></a>3、 PHP SDK 集成

##### 请确保满足以下开发环境：

- PHP 5.*
- PHP-CPP [1.7.1](https://github.com/CopernicaMarketingSoftware/PHP-CPP-LEGACY)

or

- PHP 7.0 ~ 7.3
- PHP-CPP [2.1.4](https://github.com/CopernicaMarketingSoftware/PHP-CPP)

or

- PHP 7.4 +
- PHP-CPP [2.2.0](https://github.com/CopernicaMarketingSoftware/PHP-CPP)

##### 获取
登陆 https://github.com/linkv-io/php-sdk 下载对应版本的最新so文件


##### 使用
启用LinkV扩展
```sh
[linkv]
extension=/path/linkv.so
```
使用
```php
// 开发者平台 获取的app_id
$appID = "";
// 开发者平台 获取的app_secret
$appSecret = "";
if (!LvInit($appID,$appSecret)) {
    return;
}
```

## <a name='4'></a>4、 Node SDK 集成

##### 请确保满足以下开发环境：

- Node 10.15.3 + 

##### 获取
登陆 https://github.com/linkv-io/node-sdk 查看最新版本号，写入package.json

```sh
"dependencies": {
    "linkv": "git://github.com/linkv-io/node-sdk.git#0.0.0"
}
```
> 请不要使用master分之，该版本还未进过严格测试，稳定性未得到保障
>

安装
```sh
npm install
```


##### 使用
```js
const Linkv = require('linkv');
// 开发者平台 获取的app_id
const appID = '';
// 开发者平台 获取的app_secret
const appSecret = '';

const res = new Linkv(appID, appSecret);
```

## <a name='5'></a>5、 Python2 SDK 集成

##### 请确保满足以下开发环境：

- Python 2.7.9 +

> 依赖 SetupTools 需要单独安装
>
> wget https://bootstrap.pypa.io/ez_setup.py -O - | python
> 

##### 获取
登陆 https://github.com/linkv-io/python2-sdk 下载最新版本

##### 安装

```sh
cd python-sdk

python setup.py build

python setup.py install --record log # 保留安装记录 卸载时需要
```

> 请不要使用master分之，该版本还未进过严格测试，稳定性未得到保障
>

##### 卸载
```sh
cd python-sdk
cat log |xargs rm -rf 
rm -rf build dist linkv_sdk.egg-info log
```

##### 使用
```python
// 开发者平台 获取的app_id
app_id = ''
// 开发者平台 获取的app_secret
app_secret = ''
if not linkv_sdk.init(app_id, app_secret):
    return
```

## <a name='6'></a>6、 Dart SDK 集成

##### 请确保满足以下开发环境：

- Dart >= 2.5.0
- Dart < 3.0.0 

##### 获取
登陆 https://github.com/linkv-io/dart-sdk 查看最新版本号，写入pubspec.yaml

```yaml
dependencies:
    linkv_sdk:
        git:
          url: git@github.com:linkv-io/dart-sdk.git
          ref: 0.0.0
```
> 请不要使用master分之，该版本还未进过严格测试，稳定性未得到保障
>

##### 安装
```sh
pub get
```


##### 使用
```dart
import 'package:linkv_sdk/linkv_sdk.dart' as linkv;

// 开发者平台 获取的app_id
var appID = '';
// 开发者平台 获取的app_secret
var appSecret = '';

if (!await linkv.init(appID, appSecret)) {
    print('await linkv.init');
    return;
}
```