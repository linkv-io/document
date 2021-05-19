# 私信消息集成

首先集成私信功能需要先 [初始化SDK](/?p=/zh/ios/im/integration_init.md&k=QoZ4JF0K) 。私信消息主要用于收发私信，SDK 支持的私信消息类型有如下：

* 文本类消息
* 图片类消息
* 音频类消息
* 视频类消息

## <a name='1'></a>1、构建消息对象

使用正确的方法构建对象发送消息可加速消息的处理。例如发送文本消息使用buildTextPrivateMessage方法构建消息对象，发送图片则使用buildImagePrivateMessage构建，音频消息和视频消息同理。消息构建成功result为0，非0为构建失败。

```java
LVIMMessage *msg = [[LVIMMessage alloc] init];

//构建文本消息
int result = [msg buildTextPrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];

//构建图片消息
int result = [msg buildImagePrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];

//构建音频消息
int result = [msg buildAudioPrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];

//构建视频消息
int result = [msg buildVideoPrivateRequest:fid tid:tid type:type content:content pushTitle:pushTitle pushContent:pushContent extend3:extend3 extend4:extend4 targetAppID:targetAppID targetAppUID:targetAppUID];
```

* fid
  - 发送消息者用户id
* tid
  * 消息接收用户ID。
* type
  * 消息类型，提供给您使用的消息扩展类型字段，您可以使用这个字段自定义消息类型。可传任意字符串，但不能传空串或null。
* content
  * 消息内容。
* pushTitle
  * 推送通知标题（如果用户离线，消息会以推送通知的形式发送）。
* pushContent
  * 推送通知内容。
* extend3
  * 扩展，暂未使用。
* extend4
  * 语音数据，仅语音类消息有用，其它媒体类型消息请传nil。
* targetAppID
  * 跨应用发消息时应用appId，跨应用发消息是指在LinkV开发者后台创建的两个不同appId的应用可以实现互发消息。非跨应用消息请传null。
* targetAppUID
  * 跨应用发消息的用户ID,非跨应用消息请传nil。

#### 消息类型 LVIM_MESSAGE_SUBTYPE

| 名称                       | 描述               |
| -------------------------- | ------------------ |
| LVIM_MESSAGE_SUBTYPE_MIN   | 最小无效内容类型   |
| LVIM_MESSAGE_SUBTYPE_TEXT  | 自定义文本内容类型 |
| LVIM_MESSAGE_SUBTYPE_IMAGE | 自定义图片内容类型 |
| LVIM_MESSAGE_SUBTYPE_AUDIO | 自定义音频内容类型 |
| LVIM_MESSAGE_SUBTYPE_VIDEO | 自定义视频内容类型 |
| LVIM_MESSAGE_SUBTYPE_MAX   | 最大无效内容类型   |

> 当用户接收到消息时，可以根据LVIMMessage对象中的mSubType属性获取到消息的具体类型，根据不通的消息类型正确的使用content的内容，例如当消息为文本消息时content为文本内容，当消息为图片消息时content为图片地址。

## <a name='2'></a>2、发送消息

#### 代码示例 

```java
[[LVIMSDK sharedInstance] sendMessage:msg context:nil callback:^(int ecode, int rcode, int64_t lvsgid, int64_t 	smsgid, int64_t stime) {
      //处理发送消息回调  
}];
```

#### 详细说明

#### sendMessage参数解析

* msg

  * 步骤1构建的消息对象。
* context
  
  * 发送消息的对象，可传空。
  
* callback

  * LVIM_SEND_MESSAGE_CALLBACK 类型回调block


#### LVIM_SEND_MESSAGE_CALLBACK 参数解析

```
typedef void(^LVIM_SEND_MESSAGE_CALLBACK)(int ecode, int rcode, int64_t lvsgid, int64_t smsgid, int64_t stime);
```

- ecode
  - 错误码，如果为0则代表发送消息成功，非0为失败。详见[错误码](/?p=/zh/ios/im/ecode.md&k=wOzEX8ba)
- rcode
  - 服务端返回码
- lvsgid
  - 客户端消息id
- smsgid
  - 服务端消息id
- stime
  - 发送时间戳(毫秒)

## <a name='3'></a>3、接收消息

私信消息的接收是在全局消息接收监听中，详见[初始化设置消息代理](/?p=/zh/ios/im/integration_init.md&k=QoZ4JF0K)

