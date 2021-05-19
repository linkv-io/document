# SDK 更新日志

## <a name='3'></a> xxxx-xx-xx (v x.x.x.x)

### <a name='3.1'></a> 新增功能
- ##### 转推支持 RTMPS 协议
###### &emsp;&emsp;&emsp;该功能可将直播流转推到 Facebook ，助力客户生态引流。当前仅部署到海外集群。

- ##### 流媒体数据端到端加解密
###### &emsp;&emsp;&emsp;通过推拉流之前设置的对称密钥，进一步强化媒体数据的安全性，密钥设置由外部模块完成，比如客户 App。仅支持 Native SDK 推拉流，不支持转发 CDN、WebRTC、混流客户端和录制客户端。

- ##### MediaRecorder 增加质量回调
###### &emsp;&emsp;&emsp;媒体本地录制代理 ZegoMediaRecordDelegate 新增 -onRecordStatusUpdateFromChannel:storagePath:duration:fileSize:quality: 回调。
###### &emsp;&emsp;&emsp;离线录制时可以通过该回调获取分辨率、帧率等质量信息，及时做容错处理。

> 升级注意:
> 

## <a name='2'></a> xxxx-xx-xx (v x.x.x.x)

### <a name='3.1'></a> 新增功能
- ##### 转推支持 RTMPS 协议
###### &emsp;&emsp;&emsp;该功能可将直播流转推到 Facebook ，助力客户生态引流。当前仅部署到海外集群。

- ##### 流媒体数据端到端加解密
###### &emsp;&emsp;&emsp;通过推拉流之前设置的对称密钥，进一步强化媒体数据的安全性，密钥设置由外部模块完成，比如客户 App。仅支持 Native SDK 推拉流，不支持转发 CDN、WebRTC、混流客户端和录制客户端。

- ##### MediaRecorder 增加质量回调
###### &emsp;&emsp;&emsp;媒体本地录制代理 ZegoMediaRecordDelegate 新增 -onRecordStatusUpdateFromChannel:storagePath:duration:fileSize:quality: 回调。
###### &emsp;&emsp;&emsp;离线录制时可以通过该回调获取分辨率、帧率等质量信息，及时做容错处理。

## <a name='1'></a> xxxx-xx-xx (v x.x.x.x)

### <a name='3.1'></a> 新增功能
- ##### 转推支持 RTMPS 协议
###### &emsp;&emsp;&emsp;该功能可将直播流转推到 Facebook ，助力客户生态引流。当前仅部署到海外集群。

- ##### 流媒体数据端到端加解密
###### &emsp;&emsp;&emsp;通过推拉流之前设置的对称密钥，进一步强化媒体数据的安全性，密钥设置由外部模块完成，比如客户 App。仅支持 Native SDK 推拉流，不支持转发 CDN、WebRTC、混流客户端和录制客户端。

- ##### MediaRecorder 增加质量回调
###### &emsp;&emsp;&emsp;媒体本地录制代理 ZegoMediaRecordDelegate 新增 -onRecordStatusUpdateFromChannel:storagePath:duration:fileSize:quality: 回调。
###### &emsp;&emsp;&emsp;离线录制时可以通过该回调获取分辨率、帧率等质量信息，及时做容错处理。