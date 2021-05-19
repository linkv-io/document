# Initialization

The initialization process  includes the steps of setting the configuration->starting the service->login->verifying the token authorization. When the authorization is verified, which means the SDK is integrated successfully and ready to use.

## <a name='1'></a>1、Apply for the AppID and AppSign

Please apply for the appid and signature required for SDK authentication from the [LinkV developer console](http://dev.linkv.io/) . Here is the [guide for obtaining the AppID and AppSercret](/?p=%252Fen%252Fopen%252Fquick_start.md&k=R5tULcvV) .

## <a name='2'></a>2、Initialize the SDK

### 2.1 Set up the IM configuration

* Open the log, true to print the log, false to not print. If not set, the default is not to print.
```java
LVIMSDK.sharedInstance().setLogVisibleState(true);
```

* Please call open log before initialization、Set the host domain name（setHost）、Open debugging mode and other configuration methods。For more configuration methods, see [Configure API documentation](/?p=/en/android/im/api.md&k=esSPZloQ) 

```java
LVIMSDK.sharedInstance().initWithAppId(Application app, String appId, String appSecret);
```

#### Parameter analysis

* app
  * The instance object Application，Cannot pass null
* appId
  * AppId applied in the background
* appSecret
  * AppSecret applied in the background

### 2.2 Start IM service

```java
LVIMSDK.sharedInstance().start();
```

## <a name='3'></a>3、Set the listener

### 3.1 Setting up the receiving message listener
Recommend to set up global message monitoring when initializing the SDK，If not，Private messages and room messages will not be received。In the filter callback method, you can filter messages according to various parameters。Take the following code as an example，Filters messages based on the number of messages currently being processed and the number of bytes of messages。

```java
LVIMSDK.sharedInstance().setGlobalReceiveMessageListener(receiveMessageListener);

IMBridger.IMReceiveMessageListener receiveMessageListener = new IMBridger.IMReceiveMessageListener() {
        @Override
        public boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid, String toid, String msgType, byte[] msgContent, int waitings, int packetSize, int waitLength, int bufferSize) {
            // For example, there are currently more than 1000 messages to be processed and the number of bytes occupied by the messages is greater than 10K，then discard the message。
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

#### （1）onIMReceiveMessageFilter, message filtering callback

Filtering the messages. return YES means to discard the messages. return NO will continue the processing.

```java
boolean onIMReceiveMessageFilter(int cmdtype, int subtype, int diytype, int dataid, String fromid,
                                 String toid, String msgType, byte[] msgContent, int waitings, 
                                 int packetSize, int waitLength, int bufferSize)
```

#### Parameters

* cmdtype 
* Message type: 10 represents the private message type, 11 represents the group type, 20 represents the room type, and 40 represents the system type.
* subtype 
* Content type is the media type of the content. 0 represents text content, 1 represents image content, 2 represents audio content, and 3 represents video content. 80 is the room message, that is, the room message does not distinguish media types.
* diytype
  * The SDK uses the message acceleration strategy, please ignore it.
* dataid 
* SDK processing message acceleration strategy, please ignore.
* fromid
  * Message sender's UID
* toid
  * Receiver's ID (or room ID if it is a room message)
* msgType
  * Message type, the message extension field is provided for you to use, you can use this field to customize the message type. And you can throw any of the strings, but cannot throw the blank strings or null.
* msgContent 
  * The message content is the byte array corresponding to the message content string.
* waitings
  * The current number of pending messages in the queue. It is recommended to discard some messages appropriately when there is a huge amount of messages need to be processed
* packetSize
  * The size in bytes of the message packet. In the case of tight memory, it is recommended to discard some messages that are particularly large in bytes.
* waitLength
  * The number of bytes are pending to be processed in the read-message buffer currently
* bufferSize
  * The size of the read-message buffer currently

> fromid format requirement：String type，Length does not exceed 32，Only allow underline _ 
>
> toid format requirement：String type，Length does not exceed 32，Only allow underline _ 
>

#### （2）onIMReceiveMessageHandler, message receiving callback

This method will be called if the message has not been discarded.

```java
int onIMReceiveMessageHandler(String owner, IMMsg msg, int waitings, int packetSize,
                              int waitLength, int bufferSize)
```

#### Parametes

* owner 
  * ID of the current logged-in IM user.
* msg 
  * IMMsgMessage type，[Please see IMMsg API](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html)
* waitings 
  * The number of messages received and waiting to be processed
* packetSize 
  * The size in bytes of the current message packet.
* waitLength 
  * The number of bytes are pending to be processed in the read-message buffer currently
* bufferSize 
  * The size of the read-message buffer currently。

> owner format requirement：String type，Length does not exceed 32，Only allow underline _ 
>

### 3.2 Set up token verification listener

For the details about obtaining and using the Token, please refer to [SDK Architecture Design](/?p=/en/android/im/integration_intro.md&k=sCd25bBW)

```java
LVIMSDK.sharedInstance().setEventListener(moduleEventListener);
/** Token verification event monitoring **/
IMBridger.IMModuleEventListener moduleEventListener = new IMBridger.IMModuleEventListener() {
    @Override
    public void onQueryIMToken() {
   				//....
		}

    @Override
    public void onIMAuthFailed(int ecode, int rcode, String uid, boolean isTokenExpired) {
        // If IM token verification fails, this method will be called back. At the same time also call back onQueryIMToken().
            LogUtils.d(TAG, "IM token verification failed error code = " + ecode);
        }

    @Override
    public void onIMAuthSucceed(String uid, String token, long unReadMsgSize) {
        // IM verification token passed
        
        //...     
    }

    @Override
    public void onIMTokenExpired(String uid, String token, String emsg) {
        // If IM token verification fails, this method will be called back. At the same time also call back onQueryIMToken().
        
        //...
    }
};
```

### Detailed description

####  （1）onQueryIMToken, callback for query the token

Please request and set IM token in this callback. Special attention is needed when the token is wrong, expired, or not set, this callback will be called frequently, please pay attention to add logic control to avoid frequent requests。Specific implementation can refer to[IM demo](/?p=/en/android/im/download_demo.md&k=n2yBGW3V)

```java
void onQueryIMToken()
```

#### （2）onIMAuthFailed, callback for failed token verification

After setting the token, the SDK will pass the token and the user ID to the IM Server for the verification. If the verification failed, this method and the onQueryIMToken method will be called. Therefore, after the failure, there is no need to write the request and set the logic of the IM token in the callback of the verification failure.

```java
void onIMAuthFailed(int ecode, int rcode, String uid, boolean isTokenExpired)
```

##### Parameters

* ecode
  * Error code, please click [error codes](/?p=/en/android/im/ecode.md&k=dNfqIW6P) for more details

* rcode
  * The value is always 0, please ignore it.

* uid
  * Login IM user ID
* isTokenExpired
  * true is the token expired error，false is a non-expired error。

> uid Format requirements: string type, length does not exceed 32, only allowed to contain underscores _ 
>

#### （3）onIMAuthSucceed, callback for successful token verification

After the Token has been verified, you will be able to send messages and some other functions by using IM, and you can be prompted here for connecting to IM successfully.

```java
void onIMAuthSucceed(String uid, String token, long unReadMsgSize)
```

#### Parameters

* uid
  * The IM user ID that has been successfully verified.
* token
  * The verified IM token.
* unReadMsgSize
  * The number of unread messages.

> uid Format requirements: string type, length does not exceed 32, only allowed to contain underscores _ 
>

#### （4）onIMTokenExpired, callback for token expired

When the IM SDK requests the unread messages from the IM Server with the expired token, this callback function will be triggered. And the onQueryIMToken callback function will also be called. So there is no need to request token again in this callback function when the token expired.

```java
void onIMTokenExpired(String uid, String token, String emsg)
```

##### Parameters

* uid
  * IM user ID that has been successfully verified.
* token
  * The verified IM token.
* emsg
  * The value "QUERY_IM_CONFIG" means the token expired when requesting IM configuration, and "QUERY_UNREAD_MSG" means the token expired when pulling unread messages. You can ignore。

> uid Format requirements: string type, length does not exceed 32, only allowed to contain underscores _ 
>

## <a name='4'></a>4、Login

It should be triggered when the user is logging in and returns to 0 if it is successful, otherwise it returns to non-zero.

```java
LVIMSDK.sharedInstance().login(String uid, String country);
```

##### Parameters

* uid 
  * User ID.

* country
  * The country code of the user, and can be thrown as an empty string.

> uid Format requirements: string type, length does not exceed 32, only allowed to contain underscores _ 
>

## <a name='5'></a>5、Logout

Stop the IM service when the user trigger the logged-out.

#### logout

```java
LVIMSDK.sharedInstance().logout();
```

#### Stop IM service

```java
LVIMSDK.sharedInstance().stop();
```

#### Release and destroy IMSDK

Try not to use it without special circumstances

```java
LVIMSDK.sharedInstance().release();
```



**For more information about API, please see the [API summary](/?p=/en/android/im/api.md&k=esSPZloQ)**

