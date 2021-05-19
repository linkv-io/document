# 直播间聊天

## <a name='1'></a>1、场景及功能介绍

> 直播间聊天是在主播观众场景下加入即时通讯消息的功能，即集成LinkV的IM SDK，使得同一直播间的用户可以在直播间内收发IM房间消息。本文档以** [主播观众](/?p=/zh/android/rtc/scene_live.md&k=kvorp7QL) **的直播间场景为例，介绍如何实现直播间聊天功能。

## <a name='2'></a>2、示例 Demo 源码下载

##### [直播聊天Demo下载](/?p=/zh/android/rtc/download_sdk.md&k=LKdNguJq)

## <a name='3'></a>3、集成IM SDK

IM SDK是用以提供全球即时消息服务，集成方式详见[IM快速集成](/?p=/zh/android/im/integration_process.md&k=NtiCQwKr)和[IM初始化](/?p=/zh/android/im/integration_init.md&k=DpgThmSb)

## <a name='4'></a>4、加入直播间

在调用RTC SDK加入直播间的同时用户也必须通过调用IM SDK加入直播间才能收发该直播间的消息。注意：主播请调用createChatRoom方法加入直播间，非主播请调用joinChatRoom加入。这样做方便IM服务器在主播退出直播间后做相应的回收资源工作。

```java
if (mIsHost) {
  LVIMSDK.sharedInstance().createChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);
} else {
  LVIMSDK.sharedInstance().joinChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);
}
IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","加入直播间成功");
            }
        }
    };
```

### 详细说明

#### （1）createChatRoom和joinChatRoom参数详解：

* rid
  * 待加入的直播间ID。

* context
  * 自定义Object对象，此传参会赋值给listener回调方法onIMSendMessageCallback的context参数返回。

* listener
  * 发送消息的回调监听。

#### （2）结果回调

加入直播间和之后的离开直播间以及发直播间消息都是向服务器发消息，得到服务器的响应后SDK会回调IMBridger.IMSendMessageListener类对象的onIMSendMessageCallback方法。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

* ecode
  * 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)

* tid
  * 待加入的直播间ID。
* msg
  * 封装加入直播间消息的对象。
* context 
  * 发消息接口传入的Object类型参数。

## <a name='5'></a>5、发送直播间消息

### 5.1、构建消息

构建一个消息对象，构建失败返回null。

```java
IMMsg msg = IMMsg.buildChatRoomMessage(String targetId,String msgType,String msgContent);
```

* targetId
  * 直播间ID。此处需传成功加入的直播间ID，否则该消息会发送失败。

* msgType
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。由于直播间消息可能数量巨大，此时部分消息可能会被丢弃，若要保证某些类型的消息百分百到达，请联系我们商定该字段的传值以满足该需求。
* msgContent
  * 消息内容。

### 5.2、发送直播间消息

```java
LVIMSDK.sharedInstance().sendMessage(IMMsg msg,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener sendMessageListener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","发送消息成功");
            }
        }
    };
```

#### （1）sendMessage参数详解

* msg
  * 步骤1构建的消息对象。

* context
  * 自定义Object对象，此传参会赋值给listener回调方法onIMSendMessageCallback的context参数返回。

* listener
  * 发送消息的回调监听。

#### （2）onIMSendMessageCallback结果回调

##### 发送消息待服务器响应后IM SDK会回调IMBridger.IMSendMessageListener类对象的onIMSendMessageCallback方法。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

#### 参数详解：

* ecode
  * 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)
* tid
  * 消息接收者ID。
* msg
  * 发送的消息对象。
* context 
  * 发消息接口传入的Object类型参数。

## <a name='6'></a>6、接收直播间消息

加入直播间成功后需设置直播间消息监听才能收到直播间消息。在过滤回调方法中您可以根据各参数对消息进行过滤。以下面代码为例，根据当前待处理消息条数和消息所占字节数过滤掉该消息。

```java
LVIMSDK.sharedInstance().setChatroomReceiveMessageListener(receiveMessageListener);

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

#### （1）onIMReceiveMessageFilter 消息过滤回调

对消息进行过滤。return  true表示丢弃消息。return false 则会继续处理，回调onIMReceiveMessageHandler方法。

```java
boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid,
                                 String toid, String msgType, byte[] msgContent, int waitings, 
                                 int packetSize, int waitLength, int bufferSize)
```

##### 参数解析

* cmdtype 
  * 消息类型：10代表私信类型，11代表群组类型，20代表直播间类型，40代表系统类型。

* subtype 
  * 内容类型，为内容的媒体类型，0代表文本内容，1代表图片内容，2代表音频内容，3代表视频内容。80为直播间消息，即直播间消息不区分媒体类型。

* diytype 
  * SDK处理消息加速策略用，请忽略。

* dataid 
  * SDK处理消息加速策略用，请忽略。

* fromid 
  * 消息发送者用户ID

* toid 

  * 接收者用户ID(如果是直播间消息则是直播间ID)

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

#### （2）onIMReceiveMessageHandler 消息处理回调

如果消息未被丢弃，则调用此方法。

```java
int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize,
                              int waitLength, int bufferSize)
```

##### 参数解析

* owner 
  * 当前登录IM的用户ID。
* msg 
  * IMMsg消息对象，[详见IMMsg API]()
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
LVIMSDK.sharedInstance().leaveChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","离开直播间成功");
            }
        }
    };
```

##### leaveChatRoom参数解析

* rid
  * 待离开的直播间ID。

* context
  * 自定义Object对象，此传参会赋值给listener回调方法onIMSendMessageCallback的context参数返回。

* listener
  * 发送消息的回调监听。

### onIMSendMessageCallback 结果回调

加入直播间和之后的离开直播间以及发直播间消息都是向服务器发消息，得到服务器的响应后SDK会回调IMBridger.IMSendMessageListener类对象的onIMSendMessageCallback方法。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### 参数解析

* ecode
  * 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)

* tid
  * 待离开的直播间ID。
* msg
  * 发送的消息对象。
* context 
  * 发消息接口传入的Object类型参数。

