# API summary

###### This summary mainly includes methods for initializing IM SDK and the instant messaging communication, and is suitable for the application scenarios such as peer-to-peer messaging, live broadcast messaging, and group voice/video chat etc.

## Initialization

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ------------------------------------------- |
| [initWithAppId](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#initWithAppId-android.app.Application-java.lang.String-java.lang.String-) | initialization          |
| [sharedInstance](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#sharedInstance--) | Get the singleton object of IMSDK external function            |
| [start](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#start--) | Start the Web worke, run to the update token and dispatching messages ect . |
| [release](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#release--) | Release and destroy                                    |
| [requestDebugToken](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#requestDebugToken-com.im.imlogic.LVIMSDK.RequestDebugTokenListener-) | Request IM token, this method is only valid in debug mode     |
| [stop](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#stop-int-) | stop                                        |

## Login

| method                                                         | Description                                        |
| ------------------------------------------------------------ | -------------- |
| [isAppUserLoginSucceed](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isAppUserLoginSucceed--) | Have you logged into IM |
| [login](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#login-java.lang.String-java.lang.String-) | log in to IM         |
| [logout](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#logout-long-) | log out           |

## Configuration

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ------------------------------ |
| [setAppDeviceID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setAppDeviceID-java.lang.String-) | Set the device ID of the app               |
| [setAppXAID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setAppXAID-java.lang.String-) | Set application AID                    |
| [setChatroomEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setChatroomEnableState-boolean-) | Set whether the room function is available                   |
| [setChatroomReceiveMessageListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setChatroomReceiveMessageListener-com.im.imcore.IMBridger.IMReceiveMessageListener-) | Set the Room Message listener             |
| [setDebugEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setDebugEnableState-boolean-) | Set debug mode                      |
| [setEventListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setEventListener-com.im.imcore.IMBridger.IMModuleEventListener-) | Set the event listener callback             |
| [setGlobalReceiveMessageListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setGlobalReceiveMessageListener-com.im.imcore.IMBridger.IMReceiveMessageListener-) | Set the Global Message listener             |
| [setGroupEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setGroupEnableState-boolean-) | Set whether the group is available               |
| [setHost](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setHost-java.lang.String-) | Set server domain name                 |
| [setIMToken](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setIMToken-java.lang.String-java.lang.String-) | Set the IM Token verification              |
| [setLocalConfig](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setLocalConfig-java.lang.String-java.lang.String-) | Obtain configuration information through encrypted configuration text |
| [setLogVisibleState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setLogVisibleState-boolean-) | Set whether the logs is visible               |
| [setPrivateEnableState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setPrivateEnableState-boolean-) | Set whether private messages are available               |
| [setReportListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setReportListener-com.im.imcore.IMBridger.IMReportListener-) | Set the reporting listener                 |
| [setUnReadMsgNumber](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setUnReadMsgNumber-int-) | Set unread messages number              |
| [setUploadLogFilterListener](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#setUploadLogFilterListener-com.im.imcore.IMBridger.IMUploadLogFilterListener-) | Set the log fillter uploading delegate             |
| [getAppID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getAppID--) | Get app ID                     |
| [getAppKEY](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getAppKEY--) | Get app KEY                    |
| [getApplication](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getApplication--) | Get app examples                   |
| [getCacheDataBasePath](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getCacheDataBasePath--) | obtain the cache database path                 |
| [getCacheMediaFileName](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getCacheMediaFileName-boolean-int-java.lang.String-java.lang.String-java.lang.String-) | random cache media files     |
| [getConfig](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getConfig--) | Get the configuration                     |
| [getCurrentRoomState](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getCurrentRoomState--) | Get the current room status               |
| [getDeviceID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getDeviceID--) | Get device ID                     |
| [getLogPath](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getLogPath--) | Get the log path                   |
| [getUserID](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#getUserID--) | Get device ID                     |
| [isAuthed](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isAuthed--) | Check if the authentication is successful           |
| [isConnected](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isConnected--) | Check if the connection is successful           |
| [isDebugMode](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isDebugMode--) | Check whether it is in debug mode             |
| [isGroupEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isGroupEnabled--) | Check if the group is enabled             |
| [isHttpMessageEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isHttpMessageEnabled--) | Whether http message is enabled             |
| [isPrivateEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isPrivateEnabled--) | Check whether private messaging is enabled             |
| [isChatroomEnabled](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#isChatroomEnabled--) | Check if the chat room is enabled             |

## Prvate messages

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ---------------------------- |
| [sendMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#sendMessage-com.im.imlogic.IMMsg-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | Send the messages                     |
| [deleteLocalPrivateHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#deleteLocalPrivateHistoryMessage-java.lang.String-) | Delete the local private message history     |
| [queryLocalGroupHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryLocalGroupHistoryMessage-java.lang.String-long-int-boolean-java.util.List-) | Query local group message history     |
| [queryLocalPrivateHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryLocalPrivateHistoryMessage-java.lang.String-long-int-boolean-java.util.List-) | Query local private message history     |
| [queryRemoteSessionList](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryRemoteSessionList-int-int-com.im.imcore.IMBridger.IMQueryRemoteSessionListListener-) | get the dialogue history list from remote interface   |
| [queryRemoteSessionMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#queryRemoteSessionMessage-java.lang.String-long-long-int-com.im.imcore.IMBridger.IMQueryRemoteSessionMessageListener-) | get the specific historical messages out of the dialogue from remote. |
| [querySessionMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#querySessionMessage-java.lang.String-long-long-int-com.im.imcore.IMBridger.IMQuerySessionMessageListener-) | Pull historical messages of a certain conversation       |
| [deleteLocalGroupHistoryMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#deleteLocalGroupHistoryMessage-java.lang.String-) | Delete the local group message history     |
| [sendHttpMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#sendHttpMessage-java.lang.String-java.lang.String-java.util.Map-java.util.Map-int-int-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | Send HTTP messages                 |

## Room Message

| method                                                         | Description                                        |
| ------------------------------------------------------------ | -------- |
| [createChatRoom](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#createChatRoom-java.lang.String-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | Create the room |
| [joinChatRoom](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#joinChatRoom-java.lang.String-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | Join the room |
| [leaveChatRoom](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/LVIMSDK.html#leaveChatRoom-java.lang.String-java.lang.Object-com.im.imcore.IMBridger.IMSendMessageListener-) | Leave the room |

## Build the message entities（IMMsg）

| method                                                         | Description                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [buildTextPrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildTextPrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | To build the private text message, and send the text message by using this method to build the message object. Speed up the message process and sendind the message by using the correct method to build the object. |
| [buildAudioPrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildAudioPrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | Build the private audio message                                             |
| [buildImagePrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildImagePrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | Build the private image message                                             |
| [buildVideoPrivateMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildVideoPrivateMessage-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-java.lang.String-java.lang.String-) | Build the private video message                                             |
| [buildChatRoomMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildChatRoomMessage-java.lang.String-java.lang.String-java.lang.String-) | Build the room message                                                 |
| [buildGroupMessage](https://dl.linkv.io/static/Android/IM/api/com/im/imlogic/IMMsg.html#buildGroupMessage-int-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-java.lang.String-byte:A-) | Build the group message                                                 |

