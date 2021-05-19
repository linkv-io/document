# Live room chat


## <a name='1'></a>1、Scene and function introduction


> Live room chat is the function of adding instant messaging messages in the host audience scenario, that is, integrating LinkV's IM SDK, so that users in the same live room can send and receive IM room messages in the live room. This document starts with ** [Anchor Audience](/?p=/en/android/rtc/scene_live.md&k=kvorp7QL) **as an example to introduce how to realize the chat function in the live room。

## <a name='2'></a>2、Demo Demo Source download


##### [Live chat Demo download](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq)

## <a name='3'></a>3、Integrated IM SDK

IM The SDK is used to provide global instant messaging services, the integration method is detailed in[IM quick integration](/?p=/en/android/im/integration_process.md&k=NtiCQwKr)和[IM初始化](/?p=/en/android/im/integration_init.md&k=DpgThmSb)

## <a name='4'></a>4、Join the live room


When calling the RTC SDK to join the live room, users must also call the IM SDK to join the live room in order to send and receive messages from the live room. Note: The host, please call the createChatRoom method to join the live room, and the non-host please call joinChatRoom to join. This is convenient for the IM server to do the corresponding resource recovery work after the anchor exits the live broadcast room.

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
               Log.d("TAG","Successfully joined the live room");
            }
        }
    };
```

### Detailed description


#### （1）createChatRoom and joinChatRoom parameter analysis：

* rid
  * ID of broadcast room to be added。

* context
  * Custom Object object, this parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return.

* listener
  * Callback monitoring for sending messages。

#### （2）Result callback


Joining the live room, leaving the live room afterwards, and sending the live room messages are all sending messages to the server，after getting the response from the server, the SDK will call back the onIMSendMessageCallback method of the IMBridger.IMSendMessageListener class object
。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

* ecode
  * Error code，If it is 0, the message is sent successfully，Non-zero means failure。Please see [Error code](/?p=/en/android/im/ecode.md&k=dNfqIW6P)

* tid
  * ID of the live room to be added
。
* msg
  * Encapsulate the object added to the live room message
。
* context 
  * Object type parameters passed in the message interface
。

## <a name='5'></a>5、Send live room message


### 5.1、Build message


Build a message object，Return null if the build fails
。

```java
IMMsg msg = IMMsg.buildChatRoomMessage(String targetId,String msgType,String msgContent);
```

* targetId
  *Live room ID. Here you need to pass the ID of the live broadcast room successfully joined, otherwise the message will fail to be sent
。

* msgType
* Message type, the message extension type field provided for you to use, you can use this field to customize the message type. Any string can be passed, but an empty string or null cannot be passed. Due to the large number of messages in the live broadcast room, some messages may be discarded at this time. To ensure that certain types of messages arrive 100%, please contact us to agree on the value of this field to meet this demand.
* msgContent
  * Message content
。

### 5.2、Send live room message


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

#### （1）Detailed explanation of sendMessage parameters

* msg
  * The message object constructed in step 1。

* context
  * Custom Object object, this parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return.

* listener
  * Callback monitoring for sending messages。

#### （2）onIMSendMessageCallback result callback


##### After the message is sent and the server responds, the IM SDK will call back the onIMSendMessageCallback method of the IMBridger.IMSendMessageListener class object。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

#### Detailed parameter：

* ecode
  * Error code. If it is 0, it means that the message is sent successfully. If it is not 0, it means that it failed. See [error code](/?p=/en/android/im/ecode.md&k=dNfqIW6P) for details
* tid
  * Message recipient ID
。
* msg
  * Message object sent。
* context 
  * Object type parameters passed in the message interface。

## <a name='6'></a>6、Receive live room news

After successfully joining the live room, you need to set up the live room message monitoring to receive the live room message. In the filter callback method, you can filter messages based on various parameters. Take the following code as an example, filter out the message according to the current number of messages to be processed and the number of bytes occupied by the message.

```java
LVIMSDK.sharedInstance().setChatroomReceiveMessageListener(receiveMessageListener);

IMBridger.IMReceiveMessageListener receiveMessageListener = new IMBridger.IMReceiveMessageListener() {
        @Override
        public boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid, String toid, String msgType, byte[] msgContent, int waitings, int packetSize, int waitLength, int bufferSize) {
            // For example, there are currently more than 1000 messages to be processed and the number of bytes occupied by the message is greater than 10K, then the message is discarded。
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

### Detailed description

#### （1）onIMReceiveMessageFilter Message filtering callback

Filter the messages. Return true means discarding the message. Return false will continue processing and call back onIMReceiveMessageHandler method.

```java
boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid,
                                 String toid, String msgType, byte[] msgContent, int waitings, 
                                 int packetSize, int waitLength, int bufferSize)
```

##### Parameter analysis

* cmdtype 
  * Message type: 10 for message type, 11 for group type, 20 for studio type, 40 for system type.
* subtype 
  * Content type, is the media type of content, 0 represents text content, 1 represents picture content, 2 represents audio content, 3 represents video content. 80 is broadcast room news, that is, broadcast room news does not distinguish between media types.
* diytype 
  * SDK handles message acceleration policy, please ignore.
* dataid 
  * SDK handles message acceleration policy, please ignore.
* fromid 
  * The user ID of the message sender

* toid 

  * Receiver user ID(live broadcast ID if it is a live broadcast message)

* msgType 
  * Message type, which provides you with a message extension type field that you can use to customize the message type. Can pass any string, but cannot pass null or null.
* msgContent 
  * Message content, which is the byte array corresponding to the message content string.
* waitings 
  * Number of messages currently received in the message queue waiting to be processed. If the number of messages to be processed is particularly large, it is recommended that some of the messages be discarded as appropriate.
* packetSize 

  * Number of bytes of this message packet. In memory tight situations, it is recommended to discard messages that take up an unusually large number of bytes.
* waitLength 
  * The number of bytes in the buffer that is currently reading a message waiting to be processed。

* bufferSize 
  *  The size of the buffer that is currently reading the message。

#### （2）onIMReceiveMessageHandler Message processing callback

This method is called if the message is not discarded.

```java
int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize,
                              int waitLength, int bufferSize)
```

##### Parameter analysis

* owner 
  * The user ID that is currently logged into IM。
* msg 
  * IMMsg Message Object, [see IMMsg API for details]()
* waitings 

  * The number of messages waiting to be processed in the currently received message queue。
* packetSize 
  * The number of bytes occupied by this message packet。
* waitLength 
  * The number of bytes waiting to be processed in the buffer of the current read message。
* bufferSize 
  * The size of the buffer currently reading messages。

## <a name='7'></a>7、Leaving the live room


Leaving the live room corresponds to joining the live room. This method is called when the user exits the live room. After you leave the live broadcast room, you will not be able to send and receive messages from the live broadcast room.

```java
LVIMSDK.sharedInstance().leaveChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","Successfully left the live room");
            }
        }
    };
```

##### leaveChatRoom parameter analysis


* rid
  * ID of the live room to be left
。

* context
* Custom Object object, this parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return.

* listener
  * Callback monitoring for sending messages。

### onIMSendMessageCallback Result callback


Joining the live room, leaving the live room and sending messages from the live room are all sending messages to the server, and the SDK will call back the onIMSendMessageCallback method of the IMBridger.IMSendMessageListener class object after receiving the response from the server.

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### Parameter analysis

* ecode
  * Error code. If 0, the message was sent successfully; non-0, the message failed. See [Error code](/? p=/en/android/im/ecode.md&k=dNfqIW6P)

* tid
  * ID of the live room to be left
。
* msg
  * Message object sent
。
* context 
  * Object type parameters passed in the message interface。

