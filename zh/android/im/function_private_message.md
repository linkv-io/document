# 私信消息集成

首先集成私信功能需要先 [初始化SDK](/?p=/zh/android/im/integration_init.md&k=DpgThmSb) 。私信消息主要用于收发私信，SDK 支持的私信消息类型有如下：

* 文本类消息
* 图片类消息
* 音频类消息
* 视频类消息

## <a name='1'></a>1、构建消息对象

使用正确的方法构建对象发送消息可加速消息的处理。例如发送文本消息使用buildTextPrivateMessage方法构建消息对象，发送图片则使用buildImagePrivateMessage构建，音频消息和视频消息同理。

### 1.1 文本类消息

如果消息中只包含普通的文本字符串请使用该方法，如果失败返回null。

```java
IMMsg msg = IMMsg.buildTextPrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID);
```

### 1.2 图片类消息

如果消息中包含图片链接地址请使用该方法，构建失败返回null。

```java
IMMsg msg = IMMsg.buildImagePrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID));
```

### 1.3 音频消息

如果消息为音频消息请使用该方法，音频消息的语音数据传给extend4参数。构建失败返回null。

```java
IMMsg msg = IMMsg.buildAudioPrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID));
```

###  1.4 视频消息

如果消息中包含视频链接，需要访问加载视频，请使用该方法构建消息，构建失败返回null。

```java
IMMsg msg = IMMsg.buildVideoPrivateMessage(String targetId, String msgType, String content, String pushTitle, 
                                          String pushContent, String extend3, byte[] extend4,
                                          String targetAppID, String targetAppUID);
```

#### 参数解析

* targetId
  * 消息接收用户ID。
* msgType
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。
* msgContent
  * 消息内容。
* pushTitle
  * 推送通知标题（如果用户离线，消息会以推送通知的形式发送）。
* pushContent
  * 推送通知内容。
* extend3
  * 扩展，暂未使用。
* extend4
  * 语音数据，仅语音类消息有用，其它媒体类型消息请传null。
* targetAppID
  * 跨应用发消息时应用appId，跨应用发消息是指在LinkV开发者后台创建的两个不同appId的应用可以实现互发消息。非跨应用消息请传null。
* targetAppUID
  * 跨应用发消息的用户ID,非跨应用消息请传null。

## <a name='2'></a>2、发送消息

### 代码示例 

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

  

#### （2）onIMSendMessageCallback 结果回调

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

## <a name='3'></a>3、接收消息

私信消息的接收是在全局消息接收监听中，详见[设置接收消息监听](/?p=/zh/android/im/integration_init.md&k=DpgThmSb)

