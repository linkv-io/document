# ErrCode

###### This article lists common error codes for SDK initialization, room login, push-pull streaming, and mixed streaming.
|Error code|enumeration value|description|
| --- | --- | --- |
| success | 0 | SDK Successful business operation|
| paramError| 1000| Parameter error|
| notInitError| 1001| No initialization error|
| notAuthError| 1002| SDK No authorization，Please authorize before use|
| initError| 1003| Room instance initialization error|
| unsupportFormat| 1004| Unsupported audio and video format|
| authError|2000 | SDK Authorization error|
| disconnectSignaling|3000 | Audio and video signaling service disconnection error|
| disconnectMedia| 3001| Media service disconnect error|
| noEdgeError | 4000| Cannot obtain valid audio and video signaling services|
| networkReqError| 4001| Network request error（Including network unreachable, network request timeout, 40x series error）|
| networkRspError| 4002| Network response error（Illegal return data, 50x series error）|
| unknownError| 10000| unknown mistake|
