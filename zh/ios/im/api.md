# API 文档汇总

###### 此分类下主要包括初始化IM SDK和即时通信的方法，适用于点对点发消息，直播间消息，多人聊天等应用场景。

## 初始化
| 方法                                                         | 说明                                        |
| ------------------------------------------------------------ | ------------------------------------------- |
| [initWithAppId](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/initWithAppId:secret:) | 初始化                                      |
| [sharedInstance](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/sharedInstance) | 获取IMSDK 对外功能类的单例对象。            |
| [start](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/start) | 启动工作线程，执行更新token和派发消息等工作 |
| [stop](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/stop:) | 停止                                        |

## 登录
| 方法                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [login](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/login:token:guest:country:) | 登录IM         |
| [logout](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/logout:waitFinishTimeout:) | 登出           |

## 配置
| 方法                                                         | 说明                           |
| ------------------------------------------------------------ | ------------------------------ |
| [setChatroomEnable](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setChatroomEnable:) | 设置房间功能是否可用                   |
| [setChatroomReceiveMessageDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setChatroomReceiveMessageDelegate:) | 设置房间消息代理对象             |
| [setDebugMode](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setDebugMode:) | 设置调试模式                   |
| [setModuleEventDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setModuleEventDelegate:) | 设置事件回调代理对象             |
| [setGlobalReceiveMessageDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setGlobalReceiveMessageDelegate:) | 设置全局消息代理对象             |
| [setGroupEnable](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setGroupEnable:) | 设置群组是否可用               |
| [setIMToken](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setIMToken:token:) | 设置IM的验证token              |
| [setLogVisible](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setLogVisible:) | 设置日志是否可见               |
| [setPrivateEnable](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setPrivateEnable:) | 设置私信是否可用               |
| [setReportDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setReportDelegate:) | 设置回报代理对象                 |
| [setUploadLogFilterDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setUploadLogFilterDelegate:) | 设置日志上传代理对象             |
| [getCacheDatabasePath](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCacheDatabasePath) | 获取数据库路径                 |
| [getCacheMediaFileName](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCacheMediaFileName:mftype:fid:tid:fsuffix:) | 获取本地随机缓存媒体文件名     |
| [getConfig](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getConfig) | 获取config                     |
| [getCurrentRoomState](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCurrentRoomState) | 获取当前房间状态               |
| [getCacheLogPath](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCacheLogPath) | 获取日志路径                   |
| [isAuthed](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/isAuthed) | 检测是否已经认证成功           |
| [isConnected](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/isConnected) | 检测是否已经连接成功           |
| [isHttpMessageEnabled](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/isHttpMessageEnabled) | 是否启用了http消息             |

## 私信消息
| 方法                                                         | 说明                         |
| ------------------------------------------------------------ | ---------------------------- |
| [sendMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/sendMessage:context:callback:) | 发送消息                     |
| [deleteLocalPrivateHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/deleteLocalPrivateHistoryMessage:) | 删除本地私信历史消息记录     |
| [queryLocalGroupHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryLocalGroupHistoryMessage:dbid:limit:desc:rmsgs:) | 查询本地群组消息历史记录     |
| [queryLocalPrivateHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryLocalPrivateHistoryMessage:dbid:limit:desc:rmsgs:) | 查询本地私信消息历史记录     |
| [queryRemoteSessionList](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryRemoteSessionList:pageSize:callback:) | 从远程接口拉取历史会话列表   |
| [queryRemoteSessionMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryRemoteSessionMessage:smsgid:sequence:size:callback:) | 从远程拉取某个会话的历史消息 |
| [deleteLocalGroupHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/deleteLocalGroupHistoryMessage:) | 删除本地群组历史消息记录     |
| [sendHttpMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/sendHttpMessage:method:content:headers:sendtmo:recvtmo:context:callback:) | 发送HTTP消息                 |

## 房间消息
| 方法                                                         | 说明     |
| ------------------------------------------------------------ | -------- |
| [createChatroom](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/createChatroom:context:callback:) | 创建房间 |
| [joinChatroom](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/joinChatroom:context:callback:) | 加入房间 |
| [leaveChatroom](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/leaveChatroom:context:callback:) | 离开房间 |

## 构建消息实体类（IMMsg）

| 方法                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [buildTextPrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildTextPrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | 构建文本私信消息,发送文本消息请使用本方法构建消息对象，使用正确的方法构建对象发送消息可加速消息的处理。 |
| [buildAudioPrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildAudioPrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | 构建音频私信消息                                             |
| [buildImagePrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildImagePrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | 构建图片私信消息                                             |
| [buildVideoPrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildVideoPrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | 构建视频私信消息                                             |
| [buildChatRoomTextMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildChatRoomTextMessage:toid:uname:content:) | 构建房间消息                                                 |
| [buildGroupRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildGroupRequest:fid:tid:type:content:pushTitle:pushContent:extend3:extend4:) | 构建群组消息                                                 |
