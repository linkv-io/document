# 初始化

初始化流程主要有设置配置->调用初始化方法->启动服务->登录->token验证授权几个步骤，验证通过即代表成功集成SDK，可以使用SDK了。

## <a name='1'></a>1、申请 AppID 与 AppSecret

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV)。

## <a name='2'></a>2、初始化SDK

### 2.1 初始化

* 打开日志，true为打印日志，false为不打印。如不设置，默认为不打印。

```java
LVIMSDK.sharedInstance().setLogVisibleState(true);
```

* 请在初始化之前调用打开日志、设置主机域名（setHost）、打开调试模式等配置方法。更多配置方法详见 [配置API文档](/?p=/zh/android/im/api.md&k=esSPZloQ) 

```java
LVIMSDK.sharedInstance().initWithAppId(Application app, String appId, String appSecret);
```

#### 参数解析

* app
  * 应用的实例对象Application，不能传null
* appId
  * 后台申请的appId
* appSecret
  * 后台申请的appSecret

### 2.2 启动IM服务

```java
LVIMSDK.sharedInstance().start();
```

## <a name='3'></a>3、设置监听器

### 3.1 设置接收消息监听

建议在初始化sdk时设置全局消息监听，如不设置，私信消息和房间消息都将无法收到。在过滤回调方法中您可以根据各参数对消息进行过滤。以下面代码为例，根据当前待处理消息条数和消息所占字节数过滤消息。

```java
LVIMSDK.sharedInstance().setGlobalReceiveMessageListener(receiveMessageListener);

IMBridger.IMReceiveMessageListener receiveMessageListener = new IMBridger.IMReceiveMessageListener() {
        @Override
        public boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid, String toid, String msgType, byte[] msgContent, int waitings, int packetSize, int waitLength, int bufferSize) {
            // 比如当前有超过1000条消息待处理并且消息所占字节数大于10K，则丢弃该消息。
          	if(waitings > 1000 && packetSize > 10000){
              return true;
            }
            return false;
        }

        @Override
        public int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize, int waitLength, int bufferSize) {
            // ...
          
            return 0;
        }
    };
```

### 详细说明

#### （1）onIMReceiveMessageFilter，消息过滤回调

对消息进行过滤。return  true表示丢弃消息。return false 则会继续处理，回调onIMReceiveMessageHandler方法。

```java
boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid,
                                 String toid, String msgType, byte[] msgContent, int waitings, 
                                 int packetSize, int waitLength, int bufferSize)
```

#### 参数解析

* cmdtype 
  * 消息类型：10代表私信类型，11代表群组类型，20代表房间类型，40代表系统类型。

* subtype 
  * 内容类型，为内容的媒体类型，0代表文本内容，1代表图片内容，2代表音频内容，3代表视频内容。80为房间消息，即房间消息不区分媒体类型。

* diytype 
  * SDK处理消息加速策略用，请忽略。

* dataid 
  * SDK处理消息加速策略用，请忽略。

* fromid 
  * 消息发送者用户ID

* toid 

  * 接收者用户ID(如果是房间消息则是房间ID)

* msgType 
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。

* msgContent 
  * 消息内容，是消息内容字符串对应的字节数组。

* waitings 
  * 当前收到的消息队列中等待处理的消息数量。如果待处理的消息量特别大，建议适当丢弃部分消息。

* packetSize 

  * 此条消息数据包所占字节数。在内存紧张的情况下，建议丢弃占字节数特别大的消息。

* waitLength 
  * 当前读取消息的缓冲区中等待处理的字节数大小。

* bufferSize 
  *  当前读取消息的缓冲区的大小。

> fromid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>
> toid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

#### （2）onIMReceiveMessageHandler，消息处理回调

如果消息未被丢弃，则调用此方法。

```java
int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize,
                              int waitLength, int bufferSize)
```

#### 参数解析

* owner 
  * 当前登录IM的用户ID。
* msg 
  * IMMsg消息对象，[详见IMMsg API](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html)
* waitings 

  * 当前收到的消息队列中等待处理的消息数量。
* packetSize 
  * 此条消息数据包所占字节数大小。
* waitLength 
  * 当前读取消息的缓冲区中等待处理的字节数大小。
* bufferSize 
  * 当前读取消息的缓冲区的大小。

> owner 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

### 3.2 设置token验证监听

token的用途和获取详见 [SDK架构设计](/?p=/zh/android/im/integration_intro.md&k=sCd25bBW)

```java
LVIMSDK.sharedInstance().setEventListener(moduleEventListener);
/** token验证事件监听 **/
IMBridger.IMModuleEventListener moduleEventListener = new IMBridger.IMModuleEventListener() {
    @Override
    public void onQueryIMToken() {
   				//....
		}

    @Override
    public void onIMAuthFailed(int ecode, int rcode, String uid, boolean isTokenExpired) {
        // IM token校验失败会回调此方法。同时也回调onQueryIMToken().
            LogUtils.d(TAG, "IM token校验失败 错误码 = " + ecode);
        }

    @Override
    public void onIMAuthSucceed(String uid, String token, long unReadMsgSize) {
        // IM校验token通过
        
        //...     
    }

    @Override
    public void onIMTokenExpired(String uid, String token, String emsg) {
        // IM token过期会回调此方法。同时也回调onQueryIMToken().
        
        //...
    }
};
```

### 详细说明

####  （1）onQueryIMToken，查询token回调

请在此回调中请求并设置IM token。需要特别注意的是token错误，过期，或者未设置时，此回调会频繁调用，请注意加逻辑控制避免频繁请求。具体实现可参考[IM demo](/?p=/zh/android/im/download_demo.md&k=n2yBGW3V)

```java
void onQueryIMToken()
```

#### （2）onIMAuthFailed，校验token失败回调

设置token后，SDK会将token和用户ID传给IM Server进行验证，如果验证失败会调用此方法，同时也会调用onQueryIMToken方法。所以失败后不需要在验证失败的回调中写请求和设置IM token的逻辑。

```java
void onIMAuthFailed(int ecode, int rcode, String uid, boolean isTokenExpired)
```

##### 参数解析

* ecode
  * 错误码，详见[错误码表](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)

* rcode
  * 值恒为0 ，忽略。

* uid
  * 登录IM用户ID
* isTokenExpired
  * true为token过期错误，false为非过期错误。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

#### （3）onIMAuthSucceed，校验token成功回调

token验证成功后就可以使用IM的进行发消息等功能了，可在此提示用户连接IM成功。

```java
void onIMAuthSucceed(String uid, String token, long unReadMsgSize)
```

#### 参数解析

* uid
  * 验证成功的IM用户ID。
* token
  * 验证成功的IM token。
* unReadMsgSize
  * 未读消息数。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

#### （4）onIMTokenExpired，token过期回调

IM SDK向IM Server拉取未读消息时如果返回结果为token过期会调用此方法，同时也会调用onQueryIMToken方法。所以不需要在token过期的回调中写请求和设置IM token的逻辑。

```java
void onIMTokenExpired(String uid, String token, String emsg)
```

##### 参数解析

* uid
  * 验证成功的IM用户ID。
* token
  * 验证成功的IM token。
* emsg
  * 值为"QUERY_IM_CONFIG"代表请求IM配置时token过期，"QUERY_UNREAD_MSG"代表拉取未读消息时检测到token过期。您可忽略。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

## <a name='4'></a>4、登录

用户登录时应触发，成功返回0, 否则返回非0。

```java
LVIMSDK.sharedInstance().login(String uid, String country);
```

##### 参数解析

* uid 
  * 用户ID。

* country
  * 用户所属国家码，可传空串或null，传空会默认取设备的国家码。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

## <a name='5'></a>5、登出

用户登出时应触发 登出，停止 IM 服务，释放 IMSDK 。

#### 登出

```java
LVIMSDK.sharedInstance().logout();
```

#### 停止IM服务

```java
LVIMSDK.sharedInstance().stop();
```

#### 释放销毁IMSDK

无特殊情况尽量不要使用

```java
LVIMSDK.sharedInstance().release();
```



**更多API的使用详见 [API文档汇总](/?p=/zh/android/im/api.md&k=esSPZloQ)**

