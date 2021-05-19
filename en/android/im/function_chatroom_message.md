# Room Messaging Integration

The integration of room messaging need to [initialize the SDK](/?p=/en/android/im/integration_init.md&k=DpgThmSb) 。first. The main functions are to join the room, send and receive the room messages, and leave the room. The detailed process is as follows:

## <a name='1'></a>1、Join the room

The users have to join the room to send and receive messages from the room, and identify the room by the unique room ID. Returning 0 on success, Non-zero on failure.

### 1.1 Code example 

```java
LVIMSDK.sharedInstance().joinChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","Join the room successfully");
            }
        }
    };
```

##### joinChatRoom parameters

* rid
  * ID of the room to be waiting to join.

* context
  * The object to send the message.

* listener
  * Callback listening for sending messages.

### 1.2 Result callback

Adding rooms, leaving rooms and sending room messages are all sending messages to the server，The SDK calls back IMBridger when it gets a response from the server.The onIMSendMessageCallback method of the IMSendMessageListener class object。

```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### Argument parsing

* ecode
  * Error codes，A value of 0 means the message was sent successfully，Non-zero means failure。See [Error code](/?p=/en/android/im/ecode.md&k=dNfqIW6P)

* tid
  * Room ID to be added.
* msg
  * Encapsulates the object that joins the room message.
* context 
  * Object type parameters passed in the message interface.

## <a name='2'></a>2、Send the room messages

### 2.1 Build the messsages

Return null if the build fails.

```java
IMMsg msg = IMMsg.buildChatRoomMessage(String targetId,String msgType,String msgContent);
```

##### BuildChatroomRequest parameters

* targetId
  * Room ID. You need to pass the joined room ID successfully, otherwise the message will fail to be sent.

* msgType
  * Message type, the message extension type fields are provided for you to use, you can use the fields to customize the message type. You can pass any strings, but not an empty string or null. Due to the huge number of room messages, some of the messages may be discarded at this time. To ensure that certain types of messages to be arrived 100%, please contact us to negotiate the value of this field to meet this demand.
* msgContent
  * Message content.

### 2.2 Code example 

```java
LVIMSDK.sharedInstance().sendMessage(IMMsg msg,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener sendMessageListener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","Message sent successfully");
            }
        }
    };
```

#### Detailed description

#### （1）sendMessage parameters

* msg
  * The built message object in step 1.

* context
  * The object to send the message.

* listener
  * Callback monitoring for sending messages.

#### （2）onIMSendMessageCallback，Result callback

After sending the private message and the server responds, the SDK will call back the onIMSendMessageCallback method of the IMBridger.IMSendMessageListener class object.
```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### Parameter analysis

* ecode
  * Error code, if it is 0, it means the message is sent successfully, if it is not 0, it means failure. Please see the [error code](/?p=/en/android/im/ecode.md&k=dNfqIW6P) for details

* tid
  * Message recipient ID。
* msg
  * Message object sent。
* context 
  * Object type parameters passed in the message interface。

## <a name='3'></a>3、Receive the room messages

After successfully joining the room, you need to configure the room message delegate to receive room messages.

```java
LVIMSDK.sharedInstance().setChatroomReceiveMessageListener(receiveMessageListener);

IMBridger.IMReceiveMessageListener receiveMessageListener = new IMBridger.IMReceiveMessageListener() {
        @Override
        public boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid, String toid, String msgType, byte[] msgContent, int waitings, int packetSize, int waitLength, int bufferSize) {
           // For example, there are currently more than 1000 messages to be processed and the number of bytes occupied by the message is greater than 10K, then the message is discarded
。
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

> Note: It is recommended to set up the global message delegate when initializing the SDK. If not , the private messages and room messages can not be received. If the room message delegate is set, only the callback of room message delegate will be triggered. In the filtering callback method, you can filter messages according to various parameters.

####  Detailed description

#### （1）onIMReceiveMessageFilter, messages filtering callback

Filter message。return true means discard the message。return false will continue processing，Callback onIMReceiveMessageHandler method。

```java
boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid,
                                 String toid, String msgType, byte[] msgContent, int waitings, 
                                 int packetSize, int waitLength, int bufferSize)
```

Parameters：

* cmdtype 
  * Message type: 10 represents message type, 11 represents group type, 20 represents room type, and 40 represents system type.

* subtype 
  * Content type，Media type for content，0 represents text content，1 represents picture contents，2 represents audio contents，3 represents video content. 80 is for the room message，That is, room messages do not differentiate between media types.

* diytype 
  * The SDK uses the message acceleration strategy, please ignore it.

* dataid 
  * SDK processes message acceleration policy used, please ignore.

* fromid 
  * Message sender UID

* toid 
  * Receiver UID (or room ID if it is a room message)
* msgType 
  * Message type, the message extension type field are provided for you to use, you can use the fields to customize the message type. You can pass any strings, but not an empty string or null.
* msgContent 
  * The message content, it is the byte array corresponding to the message content string.
* waitings 
  * The current number of pending messages to be processed in the queue. If the amount of messages to be processed is particularly large, it is recommended to discard some of the messages appropriately.
* packetSize 
  * The size in bytes of the message packet. In the case of the tight memory, it is recommended to discard the messages that occupied a particular large number of bytes.
* waitLength 
  * The number of bytes waiting to be processed in the buffer currently reading the message.
* bufferSize 
  * The size of the buffer currently reading messages.

#### （2）onIMReceiveMessageHandler, message receiving callback

If the message has not been discarded, this method is called.

```java
int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize,
                              int waitLength, int bufferSize)
```

* owner 
  * ID of the user currently logged in to IM.
* msg 
  * IMMsg message object，[Please see IMMsg API](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html)
* waitings 
  * The number of messages waiting to be processed in the currently received message queue.
* packetSize 
  * The size of the bytes of this message packet.
* waitLength 
  * The current number of bytes waiting to be processed in the message reading buffer.
* bufferSize 
  * The current size of the message reading buffer.

## <a name='4'></a>4、Leave the room

There is a correspondence between leaving and joining the room. This method is called when the user exits the room. They will not be able to send or receive messages from that room after the room exit.

```java
LVIMSDK.sharedInstance().leaveChatRoom(String rid,Object context, IMBridger.IMSendMessageListener listener);

IMBridger.IMSendMessageListener listener = new IMBridger.IMSendMessageListener() {
        @Override
        public void onIMSendMessageCallback(int ecode, String tid, final IMMsg msg, Object context) {
            if (ecode == 0) {
               Log.d("TAG","Leave room successfully");
            }
        }
    };
```

#### Detailed description

#### （1）Detailed parameters of leaveChatRoom:

* rid
  * The ID of the room to leave.

* context
  * Custom object，This parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return。

* listener
  * Callback monitoring for sending messages。

#### （2）onIMSendMessageCallback，Result callback

Adding rooms, leaving rooms and sending room messages are all sending messages to the server, The SDK calls back IMBridger when it gets a response from the server. The onIMSendMessageCallback method of the IMSendMessageListener class object.
```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

* ecode
  * Error code，If it is 0, the message is sent successfully，Non-zero means failure。Please see[Error Code](/?p=/en/android/im/ecode.md&k=dNfqIW6P)

* tid
  * Room ID to be left。
* msg
  * Message object sent。
* context 
  * Object type parameters passed in the message interface。

