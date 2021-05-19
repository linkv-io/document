<!--
 * @Date: 2020-06-17 11:21:08
 * @LastEditors: GWK
 * @LastEditTime: 2020-07-02 19:16:29
 * @FilePath: /linkv_doc/doc_new/zh/web/livemesdk/api.md
-->

# Web JS SDK API 文档

## <a name='1'></a> 1 请求接口

### <a name='1.1'></a> 1.1 初始化配置

> let octopusRTC = new OctopusRTC(option) option 对象参数如下:

| 参数     | 含义                 | 类型   | 必填                |
| -------- | -------------------- | ------ | ------------------- |
| appId    | appId                | String | 是                  |
| userId   | 用户 id              | String | 是                  |
| userName | 用户名               | String | 否                  |
| env      | 环境 test production | String | 否(默认 production) |

### <a name='1.1'></a> 1.2 初始化

> octopusRTC.init() 无参数

### <a name='1.2'></a> 1.3 登录房间

> octopusRTC.login(roomId,role,token).then(success).catch(error) 参数如下:

| 参数    | 含义                   | 类型                            | 必填 |
| ------- | ---------------------- | ------------------------------- | ---- |
| roomId  | 房间 id                | String                          | 是   |
| role    | 角色类型 1:主播 2:观众 | Number                          | 是   |
| token   | 登录验证               | String                          | 是   |
| success | 加入成功               | function(streamList)            | 否   |
| error   | 加入失败               | function(error)) 详见错误码列表 | 否   |

> streamList 数组中 stream 对象结构

| 参数     | 含义            | 类型   |
| -------- | --------------- | ------ |
| streamId | 流 id           | String |
| userId   | 流对应的用户 id | String |
| roomId   | 房间号          | String |

### <a name='1.4'></a> 1.4 登出房间

> octopusRTC.logout() 无参数
> 调用之后会向 OctopusRTC 服务器发送登出信令

### <a name='1.5'></a> 1.5 启动预览

> octopusRTC.startPreview(localVideo, mediaStreamConstraints).then(success).catch(error). 参数如下：

| 参数                   | 含义                  | 类型            | 必填                |
| ---------------------- | --------------------- | --------------- | ------------------- |
| localVideo             | 本地预览的 video 对象 | 文档对象        | 是                  |
| mediaStreamConstraints | 音视频配置项          | Object          | 否 (默认音视频加入) |
| success                | 预览成功              | function()      | 否                  |
| error                  | 预览失败              | function(error) | 否                  |

> mediaStreamConstraints 的对象结构

| 参数         | 含义                        | 类型    |
| ------------ | --------------------------- | ------- |
| audio        | 是否需要音频                | Boolean |
| audioInput   | 麦克风设备 Id               | String  |
| video        | 是否需要视频                | Boolean |
| videoInput   | 摄像头设备 Id               | String  |
| videoQuality | 视频质量等级 1:低 2:中 3:高 | Number  |

- audioInput 和 videoInput 可以不用指定，即不传或填 undefined。不指定时使用默认设备

> videoQuality 参数取值

| 取值 | 分辨率     |
| ---- | ---------- |
| 1    | 240\*320   |
| 2    | 480\*640   |
| 3    | 720\* 1280 |

> error 的解释如下,详情[点击此处](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)

| name                 | 含义             |
| -------------------- | ---------------- |
| AbortError           | 中止错误         |
| NotAllowedError      | 拒绝错误         |
| NotFoundError        | 找不到错误       |
| NotReadableError     | 无法读取错误     |
| OverConstrainedError | 无法满足要求错误 |
| SecurityError        | 安全错误         |
| TypeError            | 类型错误         |

### <a name='1.6'></a> 1.6 停止预览

> octopusRTC.stopPreview(localVideo)，参数如下：

| 参数       | 含义                  | 类型     | 必填 |
| ---------- | --------------------- | -------- | ---- |
| localVideo | 本地预览的 video 对象 | 文档对象 | 是   |

- 推流过程中，停止预览会导致推流中断

### <a name='1.7'></a> 1.7 开始推流

> octopusRTC.startPublishingStream(streamId,localVideo) 参数如下：

| 参数       | 含义                  | 类型     | 必填 |
| ---------- | --------------------- | -------- | ---- |
| streamId   | 推流 id               | Sting    | 是   |
| localVideo | 本地预览的 video 对象 | 文档对象 | 是   |

### <a name='1.8'></a> 1.8 结束推流

> octopusRTC.stopPublishingStream(streamId) 参数如下：

| 参数     | 含义  | 类型   | 必填 |
| -------- | ----- | ------ | ---- |
| streamId | 流 id | String | 是   |

### <a name='1.6'></a> 1.9 开始播放流

> octopusRTC.startPlayingStream(streamId,remoteVideo) 参数如下:

| 参数        | 含义                  | 类型     | 必填 |
| ----------- | --------------------- | -------- | ---- |
| streamId    | 拉流 id               | String   | 是   |
| remoteVideo | 拉流界面的 video 对象 | 文档对象 | 是   |

### <a name='1.10'></a> 1.10 停止播放流

> octopusRTC.stopPlayingStream(streamId) 参数如下:

| 参数     | 含义  | 类型   | 必填 |
| -------- | ----- | ------ | ---- |
| streamId | 流 id | String | 是   |

### <a name='1.11'></a> 1.11 暂停音效

> octopusRTC.mute(userId) 参数如下:

| 参数   | 含义    | 类型   | 必填 |
| ------ | ------- | ------ | ---- |
| userId | 用户 id | String | 是   |

### <a name='1.12'></a> 1.12 恢复音效

> octopusRTC.unmute(userId) 参数如下:

| 参数   | 含义    | 类型   | 必填 |
| ------ | ------- | ------ | ---- |
| userId | 用户 id | String | 是   |

### <a name='1.13'></a> 1.13 打开摄像头

> octopusRTC.openCamera() 无参数

### <a name='1.14'></a> 1.14 关闭摄像头

> octopusRTC.closeCamera() 无参数

## <a name='2'></a> 2 回调接口

### <a name='2.1'></a> 2.1 房间连接断开通知

> octopusRTC.onDisconnect(err) 参数如下

| 参数     | 含义     | 类型   |
| -------- | -------- | ------ |
| err.code | 错误码   | Number |
| err.msg  | 错误信息 | String |

### <a name='2.2'></a> 2.2 被踢下线通知

> octopusRTC.onKickOut(err) 参数如下:

| 参数     | 含义     | 类型   |
| -------- | -------- | ------ |
| err.code | 错误码   | Number |
| err.msg  | 错误信息 | String |

### <a name='2.3'></a> 2.3 流更新通知

> octopusRTC.onStreamUpdated(type, streamList,error) 参数如下:

| 参数       | 含义                    | 类型   |
| ---------- | ----------------------- | ------ |
| type       | 变更类型 0:添加，1:删除 | Number |
| streamList | 变更流列表              | Array  |

> 流信息对象结构:

| 参数     | 含义            | 类型   |
| -------- | --------------- | ------ |
| streamId | 流 id           | String |
| userId   | 流对应的用户 id | String |
| roomId   | 房间号          | String |

### <a name='2.4'></a> 2.4 拉流状态变更通知

> octopusRTC.onPlayStateUpdate(type, streamId)

| 参数     | 含义                                           | 类型   |
| -------- | ---------------------------------------------- | ------ |
| type     | 流状态类型 0: 拉流成功 1 : 拉流失败 2:重新拉流 | Number | Number |
| streamId | 流 id                                          | String |

### <a name='2.5'></a> 2.5 推流状态变更通知

> octopusRTC.onPublishStateUpdate(type, streamId);

| 参数     | 含义                                          | 类型   |
| -------- | --------------------------------------------- | ------ |
| type     | 流状态类型 0 :推流成功 1:推流失败 2: 重新推流 | Number |
| streamId | 流 id                                         | String |

## <a name='3'></a> 3 工具方法

### <a name='3.1'></a> 3.1 获取 roomId

> octopusRTC.roomId()

### <a name='3.2'></a> 3.2 获取 userId

> octopusRTC.userId()

### <a name='3.3'></a> 3.3 获取 userName

> octopusRTC.userName()

### <a name='3.4'></a> 3.4 获取本地摄像头信息

> octopusRTC.getCamerasList().then(success).catch(errr)

| 参数    | 含义                   | 类型                      | 必填 |
| ------- | ---------------------- | ------------------------- | ---- |
| success | 获取本地摄像头信息成功 | function(inputVideoArray) | 是   |
| error   | 获取本地摄像头信息失败 | function(error)           | 是   |

> inputVideoArray 中每个 InputVideoInfo 的参数含义如下

| 参数     | 含义          | 类型   |
| -------- | ------------- | ------ |
| deviceId | 设备 id       | String |
| groupId  | 设备所在组 id | String |
| kind     | videoinput    | String |
| label    | 设备名称      | Stirng |

### <a name='3.5'></a> 3.5 获取本地音频输入设备信息

> octopusRTC.getMicrophonesList().then(success).catch(errr)

| 参数    | 含义                         | 类型                      | 必填 |
| ------- | ---------------------------- | ------------------------- | ---- |
| success | 获取本地音频输入设备信息成功 | function(inputAudioArray) | 是   |
| error   | 获取本地音视输入设备信息失败 | function(error)           | 是   |

> inputAudioArray 中每个 InputDeviceInfo 的参数含义如下

| 参数     | 含义          | 类型   |
| -------- | ------------- | ------ |
| deviceId | 设备 id       | String |
| groupId  | 设备所在组 id | String |
| kind     | audioinput    | String |
| label    | 设备名称      | Stirng |

### <a name='3.6'></a> 3.6 获取本地音频输出设备信息

> octopusRTC.getSpeakersList().then(success).catch(errr)

| 参数    | 含义                         | 类型                    | 必填 |
| ------- | ---------------------------- | ----------------------- | ---- |
| success | 获取本地音频输出设备信息成功 | function(outAudioArray) | 是   |
| error   | 获取本地音频输出设备信息失败 | function(error)         | 是   |

> outAudioArray 中每个 outAudioInfo 的参数含义如下

| 参数     | 含义          | 类型   |
| -------- | ------------- | ------ |
| deviceId | 设备 id       | String |
| groupId  | 设备所在组 id | String |
| kind     | audiooutput   | String |
| label    | 设备名称      | Stirng |

### <a name='3.7'></a> 3.7 获取本地设备信息

> octopusRTC.devicesList().then(success).catch(errr)

| 参数    | 含义     | 类型                 | 必填 |
| ------- | -------- | -------------------- | ---- |
| success | 获取     | function(deviceList) | 是   |
| error   | 预览失败 | function(error)      | 是   |

## <a name='4'></a> 4 错误码列表

| 错误码            | 描述                    |
| ----------------- | ----------------------- |
| 400000            | edge is null            |
| 60002001          | kRoomInvalidSocketError |
| WS_JOINROOM_ERROR | 加入失败                |
