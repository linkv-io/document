# 房间消息集成

集成房间消息功能需要先 [初始化SDK](/?p=/zh/android/im/integration_init.md&k=DpgThmSb) 。主要功能为加入房间，收发房间消息，离开房间，具体流程如下：

## <a name='1'></a>1、加入房间

用户必须加入房间才能收发该房间的消息，通过房间ID唯一标识某个房间。成功返回0，失败则返回非0。

### 1.1 代码示例 

```java
LVIMSDK.sharedInstance().joinChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","加入房间成功");
            }
        }
    };
```

##### joinChatRoom参数解析

* rid
  * 待加入的房间ID。

* context
  * 自定义Object对象，此传参会赋值给listener回调方法onIMSendMessageCallback的context参数返回。

* listener
  * 发送消息的回调监听。

### 1.2 结果回调

加入房间和之后的离开房间以及发房间消息都是向服务器发消息，得到服务器的响应后SDK会回调IMBridger.IMSendMessageListener类对象的onIMSendMessageCallback方法。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### 参数解析

* ecode
  * 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)

* tid
  * 待加入的房间ID。
* msg
  * 封装加入房间消息的对象。
* context 
  * 发消息接口传入的Object类型参数。

## <a name='2'></a>2、发送房间消息

### 2.1 构建消息

构建失败返回null。

```java
IMMsg msg = IMMsg.buildChatRoomMessage(String targetId,String msgType,String msgContent);
```

##### 参数解析

* targetId
  * 房间ID。此处需传成功加入的房间ID，否则该消息会发送失败。

* msgType
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。由于房间消息可能数量巨大，此时部分消息可能会被丢弃，若要保证某些类型的消息百分百到达，请联系我们商定该字段的传值以满足该需求。
* msgContent
  * 消息内容。

### 2.2 代码示例 

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

#### 详细说明

#### （1）sendMessage参数解析

* msg
  * 步骤1构建的消息对象。

* context
  * 自定义Object对象，此传参会赋值给listener回调方法onIMSendMessageCallback的context参数返回。

* listener
  * 发送消息的回调监听。

#### （2）onIMSendMessageCallback，结果回调

发送私信消息待服务器响应后SDK会回调IMBridger.IMSendMessageListener类对象的onIMSendMessageCallback方法。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### 参数解析

* ecode
  * 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)

* tid
  * 消息接收者ID。
* msg
  * 发送的消息对象。
* context 
  * 发消息接口传入的Object类型参数。

## <a name='3'></a>3、接收房间消息

加入房间成功后需设置房间消息监听才能收到房间消息。

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

注意：建议在初始化sdk时设置全局消息监听，如不设置，私信消息和房间消息都将无法收到。若设置了房间消息监听，则房间消息只会回调房间消息监听器的方法。在过滤回调方法中您可以根据各参数对消息进行过滤。以上面代码为例，根据当前待处理消息条数和消息所占字节数过滤掉该消息。

####  详细说明

#### （1）onIMReceiveMessageFilter，消息过滤回调

对消息进行过滤。return  true表示丢弃消息。return false 则会继续处理，回调onIMReceiveMessageHandler方法。

```java
boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid,
                                 String toid, String msgType, byte[] msgContent, int waitings, 
                                 int packetSize, int waitLength, int bufferSize)
```

参数说明：

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

#### （2）onIMReceiveMessageHandler，消息处理回调

如果消息未被丢弃，则调用此方法。

```java
int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize,
                              int waitLength, int bufferSize)
```

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

## <a name='4'></a>4、离开房间

离开房间和加入房间对应，当用户退出房间时调用此方法。离开房间后将无法收发该房间的消息。

```java
LVIMSDK.sharedInstance().leaveChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","离开房间成功");
            }
        }
    };
```

#### 详细说明

#### （1）leaveChatRoom参数详解：

* rid
  * 待离开的房间ID。

* context
  * 自定义Object对象，此传参会赋值给listener回调方法onIMSendMessageCallback的context参数返回。

* listener
  * 发送消息的回调监听。

#### （2）onIMSendMessageCallback，结果回调

加入房间和之后的离开房间以及发房间消息都是向服务器发消息，得到服务器的响应后SDK会回调IMBridger.IMSendMessageListener类对象的onIMSendMessageCallback方法。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

* ecode
  * 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/android/im/ecode.md&k=dNfqIW6P)

* tid
  * 待离开的房间ID。
* msg
  * 发送的消息对象。
* context 
  * 发消息接口传入的Object类型参数。

