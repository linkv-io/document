# API summary

###### This summary mainly includes methods for initializing IM SDK and the instant messaging communication, and is suitable for the application scenarios such as peer-to-peer messaging, live broadcast messaging, and group voice/video chat etc.

## Initialization

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ------------------------------------------- |
| [initWithAppId](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/initWithAppId:secret:) | initialization                                      |
| [sharedInstance](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/sharedInstance) | Get the singleton object of IMSDK external function        |
| [start](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/start) | Start the Web worke, run to the update token and dispatching messages ect, . |
| [stop](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/stop:) | stop                                        |

## Login

| method                                                         | Description                                        |
| ------------------------------------------------------------ | -------------- |
| [login](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/login:token:guest:country:) | log in to IM         |
| [logout](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/logout:waitFinishTimeout:) | log out           |

## Configuration

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ------------------------------ |
| [setChatroomEnable](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setChatroomEnable:) | Set whether the room function is available                   |
| [setChatroomReceiveMessageDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setChatroomReceiveMessageDelegate:) | Set the Room Message delegate             |
| [setDebugMode](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setDebugMode:) | Set debug mode                   |
| [setModuleEventDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setModuleEventDelegate:) | Set the event delegation callback             |
| [setGlobalReceiveMessageDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setGlobalReceiveMessageDelegate:) | Set the Global Message delegate             |
| [setGroupEnable](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setGroupEnable:) | Set whether the group is available               |
| [setIMToken](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setIMToken:token:) | Set the IM Token verification              |
| [setLogVisible](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setLogVisible:) | Set whether the logs is visible               |
| [setPrivateEnable](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setPrivateEnable:) | Set whether private messages are available               |
| [setReportDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setReportDelegate:) | Set the reporting delegate                 |
| [setUploadLogFilterDelegate](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/setUploadLogFilterDelegate:) | Set the log fillter uploading delegate             |
| [getCacheDatabasePath](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCacheDatabasePath) | obtain the cache database path                 |
| [getCacheMediaFileName](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCacheMediaFileName:mftype:fid:tid:fsuffix:) | get the names of local random cache media files      |
| [getConfig](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getConfig) | Get the configuration                     |
| [getCurrentRoomState](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCurrentRoomState) | Get the current room status               |
| [getCacheLogPath](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/getCacheLogPath) | Get the log path                   |
| [isAuthed](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/isAuthed) | Check if the authentication is successful           |
| [isConnected](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/isConnected) | Check if the connection is successful           |
| [isHttpMessageEnabled](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/isHttpMessageEnabled) | Whether http message is enabled             |

## Prvate messages

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ---------------------------- |
| [sendMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/sendMessage:context:callback:) | Send the messages                     |
| [deleteLocalPrivateHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/deleteLocalPrivateHistoryMessage:) | Delete the local private message history     |
| [queryLocalGroupHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryLocalGroupHistoryMessage:dbid:limit:desc:rmsgs:) | Query local group message history     |
| [queryLocalPrivateHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryLocalPrivateHistoryMessage:dbid:limit:desc:rmsgs:) | Query local private message history     |
| [queryRemoteSessionList](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryRemoteSessionList:pageSize:callback:) | get the dialogue history list from remote interface   |
| [queryRemoteSessionMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/queryRemoteSessionMessage:smsgid:sequence:size:callback:) | get the specific historical messages out of the dialogue from remote. |
| [deleteLocalGroupHistoryMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/deleteLocalGroupHistoryMessage:) | Delete the local group message history     |
| [sendHttpMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/sendHttpMessage:method:content:headers:sendtmo:recvtmo:context:callback:) | Send HTTP messages                 |

## Room messages

| method                                                         | Description                                        |
| ------------------------------------------------------------ | -------- |
| [createChatroom](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/createChatroom:context:callback:) | Create the room |
| [joinChatroom](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/joinChatroom:context:callback:) | Join the room |
| [leaveChatroom](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMSDK.html#//api/name/leaveChatroom:context:callback:) | Leave the room |

## Build the message entities（IMMsg）

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [buildTextPrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildTextPrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | To build the private text message, and send the text message by using this method to build the message object. Speed up the message process and sendind the message by using the correct method to build the object.|
| [buildAudioPrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildAudioPrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | Build the private audio message                                             |
| [buildImagePrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildImagePrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | Build the private image message                                             |
| [buildVideoPrivateRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildVideoPrivateRequest:tid:type:content:pushTitle:pushContent:extend3:extend4:targetAppID:targetAppUID:) | Build the private video message                                             |
| [buildChatRoomTextMessage](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildChatRoomTextMessage:toid:uname:content:) | Build the room message                                                 |
| [buildGroupRequest](https://dl.linkv.io/static/iOS/IM/api/Classes/LVIMMessage.html#//api/name/buildGroupRequest:fid:tid:type:content:pushTitle:pushContent:extend3:extend4:) | Build the group message                                                 |

