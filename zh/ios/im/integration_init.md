# 初始化

初始化流程主要有设置配置->启动服务->登录->token验证授权几个步骤，验证通过即代表成功集成SDK，可以使用SDK了。

## <a name='1'></a>1、申请 AppID 与 AppSign

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV)。

## <a name='2'></a>2、初始化SDK

### 2.1 设置IM配置

* 配置appId和secret。

```java
[[LVIMSDK sharedInstance] initWithAppId:appid secret:secret];
```


* 设置进入调试状态，使用测试环境。YES为调试状态，NO为正式环境。默认为正式环境。

```java
[[LVIMSDK sharedInstance] setDebugMode:YES];
```

* 打开日志，YES为打印日志，NO为不打印。如不设置，默认为不打印。

```java
[[LVIMSDK sharedInstance] setLogVisible:YES];
```

> 更多配置方法详见 [配置API文档](/?p=/zh/ios/im/api.md&k=UO6NoMsq) 

### 2.2 启动IM服务

```java
[[LVIMSDK sharedInstance] start];
```

## <a name='3'></a>3、设置代理

### 3.1 设置接收消息代理
- 建议在初始化sdk时设置全局消息代理，如不设置，私信消息和房间消息都将无法收到。


```java
LVIMSDK *sdk = [[LVIMSDK sharedInstance] setAppId:appid secret:secret];

[[LVIMSDK sharedInstance] setGlobalReceiveMessageDelegate:delegateObject];

[[LVIMSDK sharedInstance] start];
```

```
//全局消息回调方法
-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)immsg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
    //处理消息
    return 0;
}
```

- 在过滤回调方法中您可以根据各参数对消息进行过滤。以下面代码为例，根据当前待处理消息条数和消息所占字节数过滤消息。

```
//消息过滤回调方法
-(BOOL)onIMReceiveMessageFilter:(int32_t)diytype
                         fromid:(const char*)fromid
                           toid:(const char*)toid
                        msgtype:(const char*)msgtype
                        content:(const char*)content
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
		// 比如当前有超过1000条消息待处理并且消息所占字节数大于10K，则丢弃该消息。
		if(waitings > 1000 && packetSize > 10000){
			return YES;
		}
    return NO;
}
```

#### 详细说明

#### （1）onIMReceiveMessageFilter，消息过滤回调

对消息进行过滤。return  YES表示丢弃消息。return NO 则会继续处理。

```java
-(BOOL)onIMReceiveMessageFilter:(int32_t)diytype
                         fromid:(const char*)fromid
                           toid:(const char*)toid
                        msgtype:(const char*)msgtype
                        content:(const char*)content
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize
  return NO;
}
```

#### 参数解析

* diytype 
  * SDK处理消息加速策略用，请忽略。
* fromid 
  * 消息发送者用户ID
* toid 
  * 接收者用户ID(如果是房间消息则是房间ID)
* msgtype 
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。
* content 
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
-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)msg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
    return 0;
}
```

#### 参数解析

* owner 
  * 当前登录IM的用户ID。
* msg 
  * LVIMMessage消息对象，[详见LVIMMessage API](/?p=/zh/ios/im/api.md&k=UO6NoMsq)
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

token的用途和获取详见 [SDK架构设计](/?p=/zh/ios/im/integration_intro.md&k=QeIBd8jF)

```java
[[LVIMSDK sharedInstance] setModuleEventDelegate:delegateObject];

-(void)onQueryIMToken {
  
	//....
  //伪代码 NSString *token = getToken();
  [[LVIMSDK sharedInstance] setIMToken:uid token:token];
}

-(void)onIMAuthSuccessed:(NSString*)uid token:(NSString*)token unReadMsgSize:(int)unReadMsgSize {
	// IM校验token通过	
}

-(void)onIMAuthFailed:(NSString*)uid token:(NSString*)token ecode:(int)ecode rcode:(int)rcode expired:(BOOL)expired {
	// IM token校验失败会回调此方法。同时也回调onQueryIMToken.
}

-(void)onIMTokenExpired:(NSString*)uid token:(NSString*)token owner:(NSString*)owner {
	// IM token过期会回调此方法。同时也回调onQueryIMToken
}
```

### 详细说明

####  （1）onQueryIMToken，查询token回调

请在此回调中请求并设置IM token。需要特别注意的是token错误，过期，或者未设置时，此回调会频繁调用，请注意加逻辑控制避免频繁请求。

```java
-(void)onQueryIMToken;
```

#### （2）onIMAuthFailed，校验token失败回调

设置token后，SDK会将token和用户ID传给IM Server进行验证，如果验证失败会调用此方法，同时也会调用onQueryIMToken方法。所以失败后不需要在验证失败的回调中写请求和设置IM token的逻辑。

```java
-(void)onIMAuthFailed:(NSString*)uid token:(NSString*)token ecode:(int)ecode rcode:(int)rcode expired:(BOOL)expired;
```

#### 参数解析

* uid
  * 登录IM用户ID
* token
  * 校验失败的token
* ecode
  * 错误码，详见[错误码表](/?p=/zh/ios/im/ecode.md&k=wOzEX8ba)
* rcode
  * 值恒为0 ，忽略。
* expired
  * YES为token过期错误，NO为非过期错误。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

#### （3）onIMAuthSucceed，校验token成功回调

token验证成功后就可以使用IM的进行发消息等功能了，可在此提示用户连接IM成功。

```java
-(void)onIMAuthSuccessed:(NSString*)uid token:(NSString*)token unReadMsgSize:(int)unReadMsgSize;
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
-(void)onIMTokenExpired:(NSString*)uid token:(NSString*)token owner:(NSString*)owner;
```

#### 参数解析

* uid
  * 验证成功的IM用户ID。
* token
  * 验证成功的IM token。
* owner
  * 值为"queryLVIMConfig"代表请求IM配置时token过期，"getUnReadMsg"代表拉取未读消息时检测到token过期。您可忽略。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

## <a name='4'></a>4、登录

用户登录时应触发，成功返回0, 否则返回非0。

```java
[[LVIMSDK sharedInstance] login:uid country:@""];
```

#### 参数解析

* uid 
  * 用户ID。
* country
  * 用户所属国家码，可传空串。

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

## <a name='5'></a>5、登出

用户登出时应触发 登出，停止 IM 服务。

#### 登出

```java
 [[LVIMSDK sharedInstance] logout:waitFlushTimeout waitFinishTimeout:waitFinishTimeout];
```

#### 参数解析

* waitFlushTimeout 
  * 等待数据同步超时毫秒数(小于等于0时不等待,默认1000)。
* waitFinishTimeout
  -  等待完成超时毫秒数(小于等于0时不等待,默认1000)

#### 停止IM服务

```java
[[LVIMSDK sharedInstance] stop:timeout];
```

#### 参数解析

* timeout 
  * 等待停止运行的最大超时毫秒数。

  

**更多API的使用详见 [API文档汇总](/?p=/zh/ios/im/api.md&k=UO6NoMsq)**

