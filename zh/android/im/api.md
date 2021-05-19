# API 文档汇总

###### 此分类下主要包括初始化IM SDK和即时通信的方法，适用于点对点发消息，直播间消息，多人聊天等应用场景。

## 初始化

| 方法                                                         | 说明                                        |
| ------------------------------------------------------------ | ------------------------------------------- |
| [initWithAppId](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#initWithAppId-android.app.Application-java.lang.String-java.lang.String-) | 设置应用的appId和appSecret并初始化          |
| [sharedInstance](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#sharedInstance--) | 获取IMSDK 对外功能类的单例对象              |
| [start](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#start--) | 启动工作线程，执行更新token和派发消息等工作 |
| [release](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#release--) | 释放销毁                                    |
| [requestDebugToken](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#requestDebugToken-com.im.imlogic.LVIMSDK.RequestDebugTokenListener-) | 请求IM的token,此方法仅在debug模式下有效     |
| [stop](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#stop-int-) | 停止                                        |

## 登录

| 方法                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [isAppUserLoginSucceed](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isAppUserLoginSucceed--) | 是否已经登录IM |
| [login](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#login-java.lang.String-java.lang.String-) | 登录IM         |
| [logout](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#logout-long-) | 登出           |

## 配置

| 方法                                                         | 说明                           |
| ------------------------------------------------------------ | ------------------------------ |
| [setAppDeviceID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setAppDeviceID-java.lang.String-) | 设置应用的设备ID               |
| [setAppXAID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setAppXAID-java.lang.String-) | 设置应用AID                    |
| [setChatroomEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setChatroomEnableState-boolean-) | 设置房间状态                   |
| [setChatroomReceiveMessageListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setChatroomReceiveMessageListener-com.im.imcore.IMBridger.IMReceiveMessageListener-) | 设置房间消息监听器             |
| [setDebugEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setDebugEnableState-boolean-) | 设置调试状态                   |
| [setEventListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setEventListener-com.im.imcore.IMBridger.IMModuleEventListener-) | 设置事件回调监听器             |
| [setGlobalReceiveMessageListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setGlobalReceiveMessageListener-com.im.imcore.IMBridger.IMReceiveMessageListener-) | 设置全局消息监听器             |
| [setGroupEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setGroupEnableState-boolean-) | 设置群组可用状态               |
| [setHost](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setHost-java.lang.String-) | 设置服务器域名                 |
| [setIMToken](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setIMToken-java.lang.String-java.lang.String-) | 设置IM的验证token              |
| [setLocalConfig](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setLocalConfig-java.lang.String-java.lang.String-) | 通过加密的配置文本得到配置信息 |
| [setLogVisibleState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setLogVisibleState-boolean-) | 设置日志是否可见               |
| [setPrivateEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setPrivateEnableState-boolean-) | 设置私信可用状态               |
| [setReportListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setReportListener-com.im.imcore.IMBridger.IMReportListener-) | 设置回报监听器                 |
| [setUnReadMsgNumber](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setUnReadMsgNumber-int-) | 设置未读消息数量               |
| [setUploadLogFilterListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setUploadLogFilterListener-com.im.imcore.IMBridger.IMUploadLogFilterListener-) | 设置日志上传监听器             |
| [getAppID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getAppID--) | 获取应用ID                     |
| [getAppKEY](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getAppKEY--) | 获取应用KEY                    |
| [getApplication](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getApplication--) | 获取应用实例                   |
| [getCacheDataBasePath](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getCacheDataBasePath--) | 获取数据库路径                 |
| [getCacheMediaFileName](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getCacheMediaFileName-boolean-int-java.lang.String-java.lang.String-java.lang.String-) | 获取本地随机缓存媒体文件名     |
| [getConfig](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getConfig--) | 获取config                     |
| [getCurrentRoomState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getCurrentRoomState--) | 获取当前房间状态               |
| [getDeviceID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getDeviceID--) | 获取设备ID                     |
| [getLogPath](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getLogPath--) | 获取日志路径                   |
| [getUserID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getUserID--) | 获取用户ID                     |
| [isAuthed](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isAuthed--) | 检测是否已经认证成功           |
| [isConnected](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isConnected--) | 检测是否已经连接成功           |
| [isDebugMode](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isDebugMode--) | 检测是否是调试模式             |
| [isGroupEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isGroupEnabled--) | 检测群组是否已启用             |
| [isHttpMessageEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isHttpMessageEnabled--) | 是否启用了http消息             |
| [isPrivateEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isPrivateEnabled--) | 检测私信是否已启用             |
| [isChatroomEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isChatroomEnabled--) | 检测房间是否已启用             |

## 私信消息

| 方法                                                         | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| [sendMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#sendMessage-com.im.imlogic.IMMsg-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | 发送消息                     |
| [deleteLocalPrivateHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#deleteLocalPrivateHistoryMessage-java.lang.String-) | 删除本地私信历史消息记录     |
| [queryLocalGroupHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryLocalGroupHistoryMessage-java.lang.String-long-int-boolean-java.util.List-) | 查询本地群组消息历史记录     |
| [queryLocalPrivateHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryLocalPrivateHistoryMessage-java.lang.String-long-int-boolean-java.util.List-) | 查询本地私信消息历史记录     |
| [queryRemoteSessionList](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryRemoteSessionList-int-int-com.im.imcore.IMBridger.IMQueryRemoteSessionListListener-) | 从远程接口拉取历史会话列表   |
| [queryRemoteSessionMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryRemoteSessionMessage-java.lang.String-long-long-int-com.im.imcore.IMBridger.IMQueryRemoteSessionMessageListener-) | 从远程拉取某个会话的历史消息 |
| [querySessionMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#querySessionMessage-java.lang.String-long-long-int-com.im.imcore.IMBridger.IMQuerySessionMessageListener-) | 拉取某个会话的历史消息       |
| [deleteLocalGroupHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#deleteLocalGroupHistoryMessage-java.lang.String-) | 删除本地群组历史消息记录     |
| [sendHttpMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#sendHttpMessage-java.lang.String-java.lang.String-java.util.Map-java.util.Map-int-int-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | 发送HTTP消息                 |

## 房间消息

| 方法                                                         | 说明     |
| ------------------------------------------------------------ | -------- |
| [createChatRoom](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#createChatRoom-java.lang.String-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | 创建房间 |
| [joinChatRoom](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#joinChatRoom-java.lang.String-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | 加入房间 |
| [leaveChatRoom](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#leaveChatRoom-java.lang.String-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | 离开房间 |

## 构建消息实体类（IMMsg）

| 方法                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [buildTextPrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildTextPrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | 构建文本私信消息,发送文本消息请使用本方法构建消息对象，使用正确的方法构建对象发送消息可加速消息的处理 |
| [buildAudioPrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildAudioPrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | 构建音频私信消息                                             |
| [buildImagePrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildImagePrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | 构建图片私信消息                                             |
| [buildVideoPrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildVideoPrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | 构建视频私信消息                                             |
| [buildChatRoomMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildChatRoomMessage-java.lang.String-java.lang.String-java.lang.String-) | 构建房间消息                                                 |
| [buildGroupMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildGroupMessage-int-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-) | 构建群组消息                                                 |

