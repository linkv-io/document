# 常见错误码

###### 本文针对初始化 SDK、登录房间、推拉流、混流部分列出常见错误码。
|错误码|枚举值|描述|
| --- | --- | --- |
| success | 0 | SDK 业务操作成功|
| paramError| 1000| 参数错误|
| notInitError| 1001| 没有初始化错误|
| notAuthError| 1002| SDK 没有授权，请先授权再使用|
| initError| 1003| 房间实例初始化错误|
| unsupportFormat| 1004| 不支持的音视频格式|
| authError|2000 | SDK 授权错误|
| disconnectSignaling|3000 | 音视频信令服务断开连接错误|
| disconnectMedia| 3001| 媒体服务断开连接错误|
| noEdgeError | 4000| 获取不到有效的音视频信令服务|
| networkReqError| 4001| 网络请求错误（含网络不可达，网络请求超时、40x 系列错误）|
| networkRspError| 4002| 网络响应错误（返回数据非法、50x 系列错误）|
| unknownError| 10000| 未知错误|
