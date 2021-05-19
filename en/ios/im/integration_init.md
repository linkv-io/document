# Initialization

The initialization process  includes the steps of setting the configuration->starting the service->login->verifying the token authorization. When the authorization is verified, which means the SDK is integrated successfully and ready to use.

## <a name='1'></a>1、Apply for the AppID and AppSign

Please apply for the appid and signature required for SDK authentication from the [LinkV developer console](http://dev.linkv.io/) . Here is the [guide for obtaining the AppID and AppSercret](/?p=%252Fen%252Fopen%252Fquick_start.md&k=R5tULcvV) .

## <a name='2'></a>2、Initialize the SDK

### 2.1 Set up the IM configuration

* Configure the appId and secret.

``` java
[[LVIMSDK sharedInstance] initWithAppId:appid secret:secret];
```

* Set to enter the debug mode to use the testing environment. YES is the debug mode, NO is the production environment. Default is production environment.

``` java
[[LVIMSDK sharedInstance] setDebugMode:YES];
```

* Open the logs, YES is to print the log, NO is not to print. Default is NO.

``` java
[[LVIMSDK sharedInstance] setLogVisible:YES];
```

> For more configuration methods, please see in the [API Summary](/?p=/en/ios/im/api.md&k=UO6NoMsq) . 

### 2.2 Start IM service

``` java
[[LVIMSDK sharedInstance] start];
```

## <a name='3'></a>3、Set the delegation

### 3.1 Setting up the receiving message delegate

* It is recommended to set the global message delegate when initializing the SDK. If not, the private messages and room messages can not be received.

``` java
LVIMSDK *sdk = [[LVIMSDK sharedInstance] setAppId:appid secret:secret];

[[LVIMSDK sharedInstance] setGlobalReceiveMessageDelegate:delegateObject];

[[LVIMSDK sharedInstance] start];
```

``` 
//callback for golbal messages
-(int)onIMReceiveMessageHandler:(NSString*)owner
                          immsg:(LVIMMessage*)immsg
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
    //process the messages
    return 0;
}
```

* In the filtering callback, you will be able to filter the messages according to the parameters. Take the following codes as an example for filtering the messages based on the current number of pending messages and the size(bytes) of the messages.

``` 
//callback for filtering messages
-(BOOL)onIMReceiveMessageFilter:(int32_t)diytype
                         fromid:(const char*)fromid
                           toid:(const char*)toid
                        msgtype:(const char*)msgtype
                        content:(const char*)content
                       waitings:(int)waitings
                     packetSize:(int)packetSize
                     waitLength:(int)waitLength
                     bufferSize:(int)bufferSize {
		// For example, if there are currently more than 1000 pending messages to be processed and the size(bytes) of the messages is greater than 10K bytes, then the messages will be discarded
		if(waitings > 1000 && packetSize > 10000){
			return YES;
		}
    return NO;
}
```

#### Detailed description

#### （1）onIMReceiveMessageFilter, message filtering callback

Filtering the messages. return YES means to discard the messages. return NO will continue the processing.

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
  * Message sender's UID
* toid
  * Receiver's ID (or room ID if it is a room message)
* msgtype
  * Message type, the message extension field is provided for you to use, you can use this field to customize the message type. And you can throw any of the strings, but cannot throw the blank strings or null.
* content
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

#### Parametes

* owner 
  * ID of the current logged-in IM user.
* msg 
  * LVIMMessage message object, please [see more details in LVIMMessage API](/?p=/en/ios/im/api.md&k=UO6NoMsq)
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

For the details about obtaining and using the Token, please refer to [SDK Architecture Design](/?p=/en/ios/im/integration_intro.md&k=QeIBd8jF)

``` java
[[LVIMSDK sharedInstance] setModuleEventDelegate:delegateObject];

-(void)onQueryIMToken {
  
	//....
  //pseudocode NSString *token = getToken();
  [[LVIMSDK sharedInstance] setIMToken:uid token:token];
}

-(void)onIMAuthSuccessed:(NSString*)uid token:(NSString*)token unReadMsgSize:(int)unReadMsgSize {
	// Token verified by IM  
}

-(void)onIMAuthFailed:(NSString*)uid token:(NSString*)token ecode:(int)ecode rcode:(int)rcode expired:(BOOL)expired {
	// Fail to verify the Token will trigger this callback and the callback of onQueryIMToken.
}

-(void)onIMTokenExpired:(NSString*)uid token:(NSString*)token owner:(NSString*)owner {
	// Expired Token will trigger this callback and the call back of onQueryIMToken
}
```

### Detailed description

####  （1）onQueryIMToken, callback for query the token

Please request and set IM token in this callback. Especially when the token is invalid, expired, or not been set, this callback will be called constantly, please pay attention to set the logical control to avoid the constant requests.

``` java
-(void)onQueryIMToken;
```

#### （2）onIMAuthFailed, callback for failed token verification

After setting the token, the SDK will pass the token and the user ID to the IM Server for the verification. If the verification failed, this method and the onQueryIMToken method will be called. Therefore, after the failure, there is no need to write the request and set the logic of the IM token in the callback of the verification failure.

``` java
-(void)onIMAuthFailed:(NSString*)uid token:(NSString*)token ecode:(int)ecode rcode:(int)rcode expired:(BOOL)expired;
```

#### Parameters

* uid
  * The Logged-in IM user ID
* token
  * Token that failed the verification
* ecode
  * Error code, please click [error codes](/?p=/en/ios/im/ecode.md&k=wOzEX8ba) for more details
* rcode
  * The value is always 0, please ignore it.
* expired
  * YES is the error caused by the expired token, NO is the error caused by the non-expired token.

> uid 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

#### （3）onIMAuthSucceed, callback for successful token verification

After the Token has been verified, you will be able to send messages and some other functions by using IM, and you can be prompted here for connecting to IM successfully.

``` java
-(void)onIMAuthSuccessed:(NSString*)uid token:(NSString*)token unReadMsgSize:(int)unReadMsgSize;
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

``` java
-(void)onIMTokenExpired:(NSString*)uid token:(NSString*)token owner:(NSString*)owner;
```

#### Parameters

* uid
  * IM user ID that has been successfully verified.
* token
  * The verified IM token.
* owner
  * A value of "queryLVIMConfig" means that the token is expired when requesting IM configuration, and the value of "getUnReadMsg" means that the expired token was detected when pulling unread messages.

> uid Format requirements: string type, length does not exceed 32, only allowed to contain underscores _ 
>

## <a name='4'></a>4、Login

It should be triggered when the user is logging in and returns to 0 if it is successful, otherwise it returns to non-zero.

``` java
[[LVIMSDK sharedInstance] login:uid country:@""];
```

#### Parameters

* uid
  * User ID.
* country
  * The country code of the user, and can be thrown as an empty string.

> uid Format requirements: string type, length does not exceed 32, only allowed to contain underscores _ 
>

## <a name='5'></a>5、Logout

Stop the IM service when the user trigger the logged-out.

#### logout

``` java
 [[LVIMSDK sharedInstance] logout:waitFlushTimeout waitFinishTimeout:waitFinishTimeout];
```

#### Parameters

* waitFlushTimeout
  + The waiting-timeout in Ms for the data synchronization(will not be waiting when less than or equal to 0, the default is 1000).
* waitFinishTimeout
  + The waiting-timeout in Ms for the completion (will not be waiting when less than or equal to 0, default 1000)

#### Stop the IM service

``` java
[[LVIMSDK sharedInstance] stop:timeout];
```

#### Parameter

* timeout
  * The maximum waiting-timeout in for stopping the running service.

  

**For more information about API, please see the [API summary](/?p=/en/ios/im/api.md&k=UO6NoMsq) .**

