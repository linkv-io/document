# Server integration

**Update date：2020-08-19**

LiveMe The social entertainment server SDK generally supports Go, PHP, Python, Node, and mainstream server languages etc.。

## <a name='1'></a>1、 Go SDK integration

##### Please make sure to meet the following development environment：

- Go 1.8 or above version

##### Obtain
Login https://github.com/linkv-io/go-sdk Check the latest version number and replace the version number in the following command

```sh
go get github.com/linkv-io/go-sdk@v0.0.0
```

> Please do not use the master to divide, this version has not been rigorously tested, and the stability is not guaranteed
>

##### Use
```go
// Developer platform obtained app_id
appID := ""
// Developer platform obtained app_secret
appSecret := ""
// http request waiting time unit(s)
httpTimeout := 30
// http number in the request pool
httpPoolSize := 10
if err := linkv.Init(appID, appSecret, httpTimeout, httpPoolSize); err != nil {
    fmt.Println(err)
    return
}
```
> Please do not use the master to divide, this version has not been rigorously tested, and the stability is not guaranteed
>
> Please set **Timeout time**reasonably
> 
> Please set **request pool**quantity reasonably，abnormal frequency may trigger attack detection
>

## <a name='2'></a>2、 Python3 SDK integration

##### Please make sure to meet the following development environment：

- Python 3.5
- Python 3.6
- Python 3.7
- Python 3.8

##### Obtain
Login https://github.com/linkv-io/python-sdk Download the latest version

##### Install

```sh
cd python-sdk

python setup.py build

python setup.py install --record log # Keep installation records Required for uninstall
```

> Please do not use the master to divide, this version has not been rigorously tested, and the stability is not guaranteed
>

##### Uninstall
```sh
cd python-sdk
cat log |xargs rm -rf 
rm -rf build dist linkv_sdk.egg-info log
```

##### Use
```python
// Developer platform obtained app_id
app_id = ''
// Developer platform obtained app_secret
app_secret = ''
// http number in the request pool
pool_size = 10
if not linkv_sdk.init(app_id, app_secret, pool_size=pool_size):
    return
```
> Please set **request pool**quantity reasonably，abnormal frequency may trigger attack detection
>

## <a name='3'></a>3、 PHP SDK Integration

##### Please make sure to meet the following development environment：

- PHP 5.*
- PHP-CPP [1.7.1](https://github.com/CopernicaMarketingSoftware/PHP-CPP-LEGACY)

or

- PHP 7.0 ~ 7.3
- PHP-CPP [2.1.4](https://github.com/CopernicaMarketingSoftware/PHP-CPP)

or

- PHP 7.4 +
- PHP-CPP [2.2.0](https://github.com/CopernicaMarketingSoftware/PHP-CPP)

##### Obtain
Login https://github.com/linkv-io/php-sdk Download the latest corresponding version so file


##### Use
Enable LinkV extension
```sh
[linkv]
extension=/path/linkv.so
```
Use
```php
// Developer platform obtained app_id
$appID = "";
// Developer platform obtained app_secret
$appSecret = "";
if (!LvInit($appID,$appSecret)) {
    return;
}
```

## <a name='4'></a>4、 Node SDK Integration

##### Please make sure to meet the following development environment：

- Node 10.15.3 + 

##### Obtain
Login https://github.com/linkv-io/node-sdk View the latest version number，write in package.json

```sh
"dependencies": {
    "linkv": "git://github.com/linkv-io/node-sdk.git#0.0.0"
}
```
> Please do not use the master to divide, this version has not been rigorously tested, and the stability is not guaranteed
>

Install
```sh
npm install
```


##### Use
```js
const Linkv = require('linkv');
// Developer platform obtained app_id
const appID = '';
// Developer platform obtained app_secret
const appSecret = '';

const res = new Linkv(appID, appSecret);
```

## <a name='5'></a>5、 Python2 SDK Integration

##### Please make sure to meet the following development environment：

- Python 2.7.9 +

> Depend on SetupTools need to be installed separately
>
> wget https://bootstrap.pypa.io/ez_setup.py -O - | python
> 

##### Obtain
Login https://github.com/linkv-io/python2-sdk Download the latest corresponding version so file

##### Install

```sh
cd python-sdk

python setup.py build

python setup.py install --record log # Keep installation records Required for uninstall
```

> Please do not use the master to divide, this version has not been rigorously tested, and the stability is not guaranteed
>

##### Uninstall
```sh
cd python-sdk
cat log |xargs rm -rf 
rm -rf build dist linkv_sdk.egg-info log
```

##### Use 
```python
// Developer platform obtained app_id
app_id = ''
// Developer platform obtained app_secret
app_secret = ''
if not linkv_sdk.init(app_id, app_secret):
    return
```

## <a name='6'></a>6、 Dart SDK Integration

##### Please make sure to meet the following development environment：

- Dart >= 2.5.0
- Dart < 3.0.0 

##### Obtain
Login https://github.com/linkv-io/dart-sdk View the latest version number，write in pubspec.yaml

```yaml
dependencies:
    linkv_sdk:
        git:
          url: git@github.com:linkv-io/dart-sdk.git
          ref: 0.0.0
```
> Please do not use the master to divide, this version has not been rigorously tested, and the stability is not guaranteed
>

##### Install
```sh
pub get
```


##### Use
```dart
import 'package:linkv_sdk/linkv_sdk.dart' as linkv;

// Developer platform obtained app_id
var appID = '';
// Developer platform obtained app_secret
var appSecret = '';

if (!await linkv.init(appID, appSecret)) {
    print('await linkv.init');
    return;
}
```