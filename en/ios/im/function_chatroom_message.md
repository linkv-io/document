# Room Messaging Integration

The integration of room messaging need to [initialize the SDK](/?p=/en/ios/im/integration_init.md&k=QoZ4JF0K) first. The main functions are to join the room, send and receive the room messages, and leave the room. The detailed process is as follows:

## <a name='1'></a>1、Join the room

The users have to join the room to send and receive messages from the room, and identify the room by the unique room ID. Returning 0 on success, Non-zero on failure.

###  Code example 

``` java
[[LVIMSDK sharedInstance] joinChatroom:roomId context:nil callback:^(int ecode, int rcode, int64_t cmsgid, int64_t smsgid, int64_t stime) {
		//message callback
}];
```

#### LVIM_SEND_MESSAGE_CALLBACK parameters

``` 
typedef void(^LVIM_SEND_MESSAGE_CALLBACK)(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime);
```

* ecode
  * Error code, if it is 0, it means the message is sent successfully, if it is not 0, it means failure. Please see the [error code](/?p=/en/ios/im/ecode.md&k=wOzEX8ba) for details
* rcode
  * Server return code
* lvsgid
  * Client message id
* smsgid
  * Server message id
* estimates
  * Send timestamp (ms)

#### joinChatRoom parameters

* rid
  * ID of the room to be waiting to join.
* context
  * The object to send the message.
* callback
  * Message callback.

## <a name='2'></a>2、Send the room messages

### 2.1 Build the messsages

The result is 0 for the successful build and non-zero for failure.

``` java
LVIMMessage *msg = [[LVIMMessage alloc] init];
int result = [msg buildChatroomRequest:uid tid:tid type:type content:content];
```

#### BuildChatroomRequest parameters

* uid
  * User id.
* time
  * Room ID. You need to pass the joined room ID successfully, otherwise the message will fail to be sent.
* type
  * Message type, the message extension type fields are provided for you to use, you can use the fields to customize the message type. You can pass any strings, but not an empty string or null. Due to the huge number of room messages, some of the messages may be discarded at this time. To ensure that certain types of messages to be arrived 100%, please contact us to negotiate the value of this field to meet this demand.
* content
  * Message content.

### 2.2 Code example 

``` java
[[LVIMSDK sharedInstance] sendMessage:msg context:self callback:^(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime) {
     //message callback      
}];

```

> This data callback structure is the same as the joinChatroom callback, and is of the same type as LVIM_SEND_MESSAGE_CALLBACK.

#### sendMessage parameters

* msg
  * The built message object in step 1.
* context
  * The object to send the message.
* callback
  * Message callback.

## <a name='3'></a>3、Receive the room messages

* After successfully joining the room, you need to configure the room message delegate to receive room messages.


``` java
[[LVIMSDK sharedInstance] setChatroomReceiveMessageDelegate:delegateObject];

-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)cmimmsg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
		//process the received messages
    return 0;
}
```

* In the filtering callback method, you can filter the messages according to the various parameters.

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
    // filter the messages according to this callback parameter.
    // for example if there are more than 1000 pending messages to be processed and the total size in bytes is greater than 10k, then  the messages are discarded.
    if(waitings > 1000 && packetSize > 10000){
       return YES;
    }
    return NO;
}
```

> Note: It is recommended to set up the global message delegate when initializing the SDK. If not , the private messages and room messages can not be received. If the room message delegate is set, only the callback of room message delegate will be triggered. In the filtering callback method, you can filter messages according to various parameters.

####  Detailed description

#### （1）onIMReceiveMessageFilter, messages filtering callback

To filter the messages. return YES means to discard the message. return NO will continue processing.

``` java
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

#### Parameters

* diytype
  * The SDK uses the message acceleration strategy, please ignore it.
* fromid
  * Message sender UID
* toid
  * Receiver UID (or room ID if it is a room message)
* msgtype
  * Message type, the message extension type field are provided for you to use, you can use the fields to customize the message type. You can pass any strings, but not an empty string or null.
* content
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

``` java
-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)msg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
    return 0;
}
```

#### Parameters

* owner
  * ID of the user currently logged in to IM.
* msg 
  * LVIMMessage message object, please [see LVIMMessage API for details](/?p=/en/ios/im/api.md&k=UO6NoMsq)
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

``` java
[[LVIMSDK sharedInstance] leaveChatroom:rid context:nil callback:^(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime) {
   //message callback 
}];
```

> The callback data structure is the same as the joinChatroom callback, and is of the same type as LVIM_SEND_MESSAGE_CALLBACK.

#### Detailed description

#### （1）Detailed parameters of leaveChatRoom:

* rid
  * The ID of the room to leave.
* context
  * The object to send the message.
* callback
  * Message callback.
