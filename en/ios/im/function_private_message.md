# Private Messaging Integration

To Integrate private messaging feature you need to [initialize the SDK](/?p=/en/ios/im/integration_init.md&k=QoZ4JF0K) first. Private messaging is mainly used to send and receive private messages. The types of private messages supported by the SDK are as follows:

* Text messages
* Image messages
* Audio messages
* Video messages

## <a name='1'></a>1、Build the message object

To speed up the processing of messages, you have to use the correct method to build the objects to send the messages. For example, to send the text messages should be using the buildTextPrivateMessage method to build the message object, using buildImagePrivateMessage for the image messages. the audio messages and video messages are in the same analogy. If the message is built successfully, the result will be 0, if not it is failed.

``` java
LVIMMessage *msg = [[LVIMMessage alloc] init];

//build the text messages
int result = [msg buildTextPrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];

//build the image messages
int result = [msg buildImagePrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];

//build the audio messages
int result = [msg buildAudioPrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];

//buid the video messages
int result = [msg buildVideoPrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];
```

* fid
  * Sender Uid
* tid
  * Receiver UID.
* type
  * Message type, the message extension type fields are provided for you to use, you can use the fields to customize the message type. You can pass any strings, but not an empty string or null.
* content
  * Message content.
* pushTitle
  * Push notification title (if the user is offline, the message will be sent as a push notification).
* pushContent
  * Push notification content.
* extend3
  * Extension, not used yet.
* extend4
  * Voice data, only be used for voice messages, please pass nil for any other media types.
* targetAppID
  * AppId is used when sending messages across the apps. Cross-apps messaging means that two applications with different appIds created by LinkV developers console will be able to send messages to each other. Please pass null for non-cross-application messages.
* targetAppUID
  * User ID for cross-application messaging, please pass nil for non-cross-application messaging.

#### Message types LVIM_MESSAGE_SUBTYPE

| name                       | description               |
| -------------------------- | ------------------ |
| LVIM_MESSAGE_SUBTYPE_MIN   | Minimum invalid content type   |
| LVIM_MESSAGE_SUBTYPE_TEXT  | Custom text content type |
| LVIM_MESSAGE_SUBTYPE_IMAGE | Custom image content type |
| LVIM_MESSAGE_SUBTYPE_AUDIO | Custom audio content type |
| LVIM_MESSAGE_SUBTYPE_VIDEO | Custom video content type |
| LVIM_MESSAGE_SUBTYPE_MAX   | Maximum invalid content type   |

> When the users received the messages, they can obtain the specific type of the message according to the mSubType property in the LVIMMessage object, and use the correct content according to the different message types. For example, when the message is a text message so the content is text content, and when the message is a image message then the content of the message will be the address of the image.

## <a name='2'></a>2、Sending messages

#### Code example 

``` java
[[LVIMSDK sharedInstance] sendMessage:msg context:nil callback:^(int ecode, int rcode, int64_t lvsgid, int64_t 	smsgid, int64_t stime) {
      //the callcack for processing the received messages
}];
```

#### Detailed description

#### SendMessage parameter

* msg
  * The message object built in step 1.
* context
  * The object to send the message, it can be empty.
* callback
  * LVIM_SEND_MESSAGE_CALLBACK type callback block

#### LVIM_SEND_MESSAGE_CALLBACK parameter

``` 
typedef void(^LVIM_SEND_MESSAGE_CALLBACK)(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime);
```

* ecode
  * Error code, if it is 0, it means the message is sent successfully, if not, it means the failure See [error code](/?p=/en/ios/im/ecode.md&k=wOzEX8ba) for details
* rcode
  * Server return code
* lvsgid
  * Client message id
* smsgid
  * Server message id
* estimates
  * Send timestamp (ms)

## <a name='3'></a>3、Messages reception

The reception of private message is in the global message reception monitoring, please see the  [Initialization](/?p=/en/ios/im/integration_init.md&k=QoZ4JF0K) for more details.

