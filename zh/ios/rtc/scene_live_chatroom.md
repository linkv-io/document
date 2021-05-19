# 直播间聊天

## <a name='1'></a>1、场景及功能介绍

> 直播间聊天是在主播观众场景下加入即时通讯消息的功能，即集成LinkV的IM SDK，使得同一直播间的用户可以在直播间内收发IM房间消息。本文档以** [主播观众](/?p=/zh/ios/rtc/scene_live.md&k=kvorp7QL) **的直播间场景为例，介绍如何实现直播间聊天功能。

## <a name='2'></a>2、示例 Demo 源码下载

##### [Github 下载]()

## <a name='3'></a>3、集成IM SDK

IM SDK是用以提供全球即时消息服务，集成方式详见 [IM快速集成](/?p=/zh/ios/im/integration_process.md&k=NtiCQwKr)和 [IM初始化](/?p=/zh/ios/im/integration_init.md&k=DpgThmSb)

## <a name='4'></a>4、加入直播间

在调用RTC SDK加入直播间的同时用户也必须通过调用IM SDK加入直播间才能收发该直播间的消息。注意：主播请调用createChatRoom方法加入直播间，非主播请调用joinChatRoom加入。这样做方便IM服务器在主播退出直播间后做相应的回收资源工作。

```java
if (mIsHost) {
  [[LVIMSDK sharedInstance] createChatRoom:rid context:nil callback:^(int ecode, int rcode, int64_t cmsgid, 		int64_t smsgid, int64_t stime) {
		//消息回调
	}];
} else {
  [[LVIMSDK sharedInstance] joinChatroom:rid context:nil callback:^(int ecode, int rcode, int64_t cmsgid, 		   	 int64_t smsgid, int64_t stime) {
		//消息回调
	}];
}
```

### 详细说明

#### LVIM_SEND_MESSAGE_CALLBACK 参数解析

```
typedef void(^LVIM_SEND_MESSAGE_CALLBACK)(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime);
```

- ecode
  - 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/ios/im/ecode.md&k=wOzEX8ba)
- rcode
  - 服务端返回码
- lvsgid
  - 客户端消息id
- smsgid
  - 服务端消息id
- stime
  - 发送时间戳(毫秒)

#### createChatRoom和joinChatRoom参数详解：

* rid
  * 待加入的房间ID。

* context
  * 发送消息的对象。

* callback
  * 消息回调。

## <a name='5'></a>5、发送直播间消息

### 5.1、构建消息

构建成功result为0，失败为非0。

```java
LVIMMessage *msg = [[LVIMMessage alloc] init];
int result = [msg buildChatroomRequest:uid tid:tid type:type content:content];
```

#### buildChatroomRequest参数解析

* uid
  - 用户id。
* tid
  * 房间ID。此处需传成功加入的房间ID，否则该消息会发送失败。
* type
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。由于房间消息可能数量巨大，此时部分消息可能会被丢弃，若要保证某些类型的消息百分百到达，请联系我们商定该字段的传值以满足该需求。
* content
  * 消息内容。

### 5.2、发送直播间消息

```java
[[LVIMSDK sharedInstance] sendMessage:msg context:self callback:^(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime) {
     //消息回调   
}];
```

> callback数据结构与进入直播间joinChatroom callback相同，同为LVIM_SEND_MESSAGE_CALLBACK类型。

#### sendMessage参数解析

* msg
  * 步骤1构建的消息对象。

* context
  * 发送消息的对象。

* callback
  * 消息回调。

## <a name='6'></a>6、接收直播间消息

- 加入房间成功后需设置房间消息代理才能收到房间消息。


```java
[[LVIMSDK sharedInstance] setChatroomReceiveMessageDelegate:delegateObject];

-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)cmimmsg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
		//处理收到的消息
    return 0;
}
```

- 在过滤回调方法中您可以根据各参数对消息进行过滤。

```
-(BOOL)onIMReceiveMessageFilter:(int32_t)diytype
                         fromid:(const char*)fromid
                           toid:(const char*)toid
                        msgtype:(const char*)msgtype
                        content:(const char*)content
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
    //根据此回调方法的参数进行消息过滤
    // 比如当前有超过1000条消息待处理并且消息所占字节数大于10K，则丢弃该消息。
    if(waitings > 1000 && packetSize > 10000){
       return YES;
    }
    return NO;
}
```

> 注意：建议在初始化sdk时设置全局消息代理，如不设置，私信消息和房间消息都将无法收到。若设置了房间消息代理，则房间消息只会回调房间消息代理方法。在过滤回调方法中您可以根据各参数对消息进行过滤。

### 详细说明

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

## <a name='7'></a>7、离开直播间

离开直播间和加入直播间对应，当用户退出直播间时调用此方法。离开直播间后将无法收发该直播间的消息。

```java
[[LVIMSDK sharedInstance] leaveChatroom:rid context:nil callback:^(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime) {
   //消息回调  
}];
```

> callback数据结构与进入直播间joinChatroom callback相同，同为LVIM_SEND_MESSAGE_CALLBACK类型。

##### leaveChatRoom参数解析

* rid
  * 待离开的房间ID。
* context
  * 发送消息的对象。

* callback
  * 消息回调。
