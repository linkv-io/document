# Private Messaging Integration

To Integrate private messaging feature you need to [initialize the SDK](/?p=/en/android/im/integration_init.md&k=DpgThmSb) first. Private messaging is mainly used to send and receive private messages. The types of private messages supported by the SDK are as follows:

* Text messages
* Image messages
* Audio messages
* Video messages

## <a name='1'></a>1、Build the message object

To speed up the processing of messages, you have to use the correct method to build the objects to send the messages. For example, to send the text messages should be using the buildTextPrivateMessage method to build the message object, using buildImagePrivateMessage for the image messages. the audio messages and video messages are in the same analogy. If the message is built successfully, the result will be 0, if not it is failed.

### 1.1 Text class message

Use this method if the message contains only ordinary text strings，If it fails, return null。

```java
IMMsg msg = IMMsg.buildTextPrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID);
```

### 1.2 Picture type message

Please use this method if the message contains the link address of the picture，Return null if the build fails。

```java
IMMsg msg = IMMsg.buildImagePrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID));
```

### 1.3 Audio message

Use this method if the message is an audio message，the voice data of the audio message is passed to the extend4 parameter。Return null if the build fails。

```java
IMMsg msg = IMMsg.buildAudioPrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID));
```

###  1.4 Video Message

If the message contains a video link，Need access to load video，Please use this method to build the message，Return null if the build fails。

```java
IMMsg msg = IMMsg.buildVideoPrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID);
```

#### Parameter analysis

* targetId
  * Message receiving user ID。
* msgType
  * Message type, the message extension type fields are provided for you to use, you can use the fields to customize the message type. You can pass any strings, but not an empty string or null.
* msgContent
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

## <a name='2'></a>2、Sending messages

### Code example

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

#### （1）sendMessage parameter

* msg
  * The message object built in step 1.
* context
  
  * Custom Object，This parameter will be assigned to the context parameter of the listener callback method onIMSendMessageCallback to return。
  
* listener

  * Callback monitoring for sending messages。

  

#### （2）onIMSendMessageCallback Result callback

After sending the private message and the server responds, the SDK will call back the onIMSendMessageCallback method of the IMBridger.IMSendMessageListener class object.
```java
void onIMSendMessageCallback(int ecode,String tid,IMMsg msg,Object context);
```

##### Parameter analysis

* ecode
  * Error code, if it is 0, it means the message is sent successfully, if not, it means the failure See [error code](/?p=/en/android/im/ecode.md&k=dNfqIW6P) for details
* tid
  * Message recipient ID。
* msg
  * Message object sent。
* context 
  * Object type parameters passed in the message interface。

## <a name='3'></a>3、Messages reception

The reception of private messages is in the global message reception monitoring，Please see[Set up receiving message monitoring](/?p=/en/android/im/integration_init.md&k=DpgThmSb)

