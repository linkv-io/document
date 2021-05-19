# Live room chat


## <a name='1'></a>1、Scene and function introduction


> Live room chat is the function of adding instant messaging messages in the host audience scenario, that is, integrating LinkV's IM SDK, so that users in the same live room can send and receive IM room messages in the live room. This document starts with ** [Anchor Audience](/?p=/en/ios/rtc/scene_live.md&k=kvorp7QL) **as an example to introduce how to realize the chat function in the live room。

## <a name='2'></a>2、Demo Demo Source download

##### [Live chat Demo download](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq)

## <a name='3'></a>3、Integrated IM SDK

IM The SDK is used to provide global instant messaging services, the integration method is detailed in[IM quick integration](/?p=/en/ios/im/integration_process.md&k=NtiCQwKr)and [IM initialization](/?p=/en/ios/im/integration_init.md&k=DpgThmSb)

## <a name='4'></a>4、Join the live room


When calling the RTC SDK to join the live room, users must also call the IM SDK to join the live room in order to send and receive messages from the live room. Note: The host, please call the createChatRoom method to join the live room, and the non-host please call joinChatRoom to join. This is convenient for the IM server to do the corresponding resource recovery work after the anchor exits the live broadcast room.

```java
if (mIsHost) {
  [[LVIMSDK sharedInstance] createChatRoom:rid context:nil callback:^(int ecode, int rcode, int64_t cmsgid, 		int64_t smsgid, int64_t stime) {
		//Message Callback 
	}];
} else {
  [[LVIMSDK sharedInstance] joinChatroom:rid context:nil callback:^(int ecode, int rcode, int64_t cmsgid, 		   	 int64_t smsgid, int64_t stime) {
		//Message Callback 
	}];
}
```

### Detailed description

#### LVIM_SEND_MESSAGE_CALLBACK Parameter analysis

```
typedef void(^LVIM_SEND_MESSAGE_CALLBACK)(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime);
```

- ecode
  - Error code，If it is 0, the message is sent successfully，Non-zero means failure。Please see [Error code](/?p=/en/ios/im/ecode.md&k=wOzEX8ba)
- rcode
  - The return code of the server
- lvsgid
  - Client message id
- smsgid
  - Server message id
- stime
  - Send timestamp (ms)

#### createChatRoom and joinChatRoom parameter analysis：

* rid
  * ID of broadcast room to be added。

* context
  * Custom Object object, this parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return.
* callback
  * Callback monitoring for sending messages。

## <a name='5'></a>5、Send live room message

### 5.1、Build message

Build a message object，Return 0 if the build fails

```java
LVIMMessage *msg = [[LVIMMessage alloc] init];
int result = [msg buildChatroomRequest:uid tid:tid type:type content:content];
```

#### buildChatroomRequest Parameter analysis

* uid
  - User's id。
* tid
  * Broadcast room‘s ID i。Upload the room ID that was successfully added, otherwise the message will fail to be sent.
* type
  * Message type, the message extension type field provided for you to use, you can use this field to customize the message type. This field can pass any string, but cannot pass an empty string or null. As the number of messages in the room may be huge, some messages may be discarded at this time. To ensure that certain types of messages can reach 100%, please contact us to discuss the value of this field to meet this demand.
* content
  * Message content 。

### 5.2、Send live room message

```java
[[LVIMSDK sharedInstance] sendMessage:msg context:self callback:^(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime) {
     //Message Callback
}];
```

> The structure of the callback data is the same as the data of joining Chatroom, which is of type LVIM_SEND_MESSAGE_CALLBACK.

#### sendMessage Parameter analysis

* msg
  * The message object constructed in step 1。

* context
  * Custom Object object, this parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return.

* callback
  * Callback monitoring for sending messages。

## <a name='6'></a>6、 receiving the live room messages

- After successfully joining the room, you need to set up a message agent to receive room messages.


```java
[[LVIMSDK sharedInstance] setChatroomReceiveMessageDelegate:delegateObject];

-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)cmimmsg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
		//Process the received message
    return 0;
}
```

- In the filter callback method, you can filter messages based on various parameters.

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
    //Please filter messages according to the parameters of this callback method
    // For example, if there are currently more than 1000 messages to be processed and the number of bytes occupied by the message is greater than 10K, the message should be discarded.
    if(waitings > 1000 && packetSize > 10000){
       return YES;
    }
    return NO;
}
```

> Note: It is recommended to set the global message agent when initializing the SDK, otherwise, the private message and room message will not be received. If the room message agent is set, only the room message agent method will be called back.In the filter callback method, you can filter messages based on various parameters.

### Detailed description

#### （1）onIMReceiveMessageFilter Message filtering callback
Filter the messages. return  YES means that the message will be discarded。return NO means that the message will continue to be processed.

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

#### Parameter analysis

* diytype 
  * SDK handles message acceleration policy, please ignore.

* fromid 
  * The user ID of the message sender

* toid 

  * Receiver user ID(live broadcast ID if it is a live broadcast message)

* msgtype 
  * Message type, which provides you with a message extension type field that you can use to customize the message type. Can pass any string, but cannot pass null or null.

* content 
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
-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)msg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
    return 0;
}
```

#### Parameter analysis

* owner 
  * The user ID that is currently logged into IM。
* msg 
  * LVIMMessage Object，[see LVIMMessage API](/?p=/en/ios/im/api.md&k=UO6NoMsq)
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
[[LVIMSDK sharedInstance] leaveChatroom:rid context:nil callback:^(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime) {
   //Message Callback 
}];
```

> The structure of the callback data is the same as the data of joining Chatroom, which is of type LVIM_SEND_MESSAGE_CALLBACK.

##### leaveChatRoomThe structure of the callback data is the same as the data of joining Chatroom, which is of type LVIM_SEND_MESSAGE_CALLBACK.

* rid Parameter analysis
  * ID of the live room to be left
* context
  * Custom Object object, this parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return.

* callback
  * Callback monitoring for sending messages。
