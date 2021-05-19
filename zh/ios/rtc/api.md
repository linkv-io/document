# 文档使用 API 汇总

###### 此分类下主要包括初始化 SDK 和基本音视频通信的方法，适用于语音通话、视频通话、语音/视频直播等应用场景。

## <a name='1'></a> 基础功能
###### 此分类下主要包括初始化 SDK 和基本音视频通信的方法，适用于语音通话、视频通话、语音/视频直播等应用场景

### <a name='1.1'></a> 初始化

| 方法名 | 说明 |
| --- | --- |
|[sharedInstance](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sharedInstance)|获取 LVRTCEngine 单例|
|[initSdk](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/initSdk)|使用 SDK 前请先出时候 SDK|
|[unInitSDK](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/unInitSDK)|卸载SDK，资源释放|
|[setISOCountryCode](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setISOCountryCode:)|设置国家码，SDK 辅助信息，可以不传|
|[setLogLevel:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setLogLevel:)|设置日志级别|
|[setUseTestEnv:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setUseTestEnv:)|设置是否使用测试环境|
|[setUseInternationalEnv:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setUseInternationalEnv:)|是否使用国际版本（SDK 默认使用中国版本，国内用户请不要调用）|
|[setDebugServerIp:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setDebugServerIp:)|设置调试服务 IP，可以不传|
|[setDecoderPixelType:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setDecoderPixelType:)|设置解码像素格式|

### <a name='1.2'></a> 鉴权、登录和登出

| 方法名 | 说明 |
| --- | --- |
| [auth:skStr:userId:completion](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/auth:skStr:userId:completion:) | SDK 鉴权接口，使用 SDK 时必须确保鉴权成功才能使用 |
|[loginRoom:roomId:isHost:isOnlyAudio:delegate](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/loginRoom:roomId:isHost:isOnlyAudio:delegate:)| 登陆房间接口，发布资源、连麦、开始播放视频流之前需要先登陆房间，同时为 RTC 引擎设置代理回调 |
|[logoutRoom:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/logoutRoom:)|登出房间、清理资源|

### <a name='1.3'></a> 推流和推流参数设置

| 方法名 | 说明 |
| --- | --- |
|[startPublishing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startPublishing)|开始发布直播接口，观众也可以调用该接口和主编进行连麦，注意该接口需要配和 startCapture 来使用 |
|[stopPublishing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopPublishing)|停止推流接口|
|[startCapture](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startCapture)|开始视频采集接口|
|[stopCapture](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopCapture)|停止视频采集|
|[addDisplayView:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/addDisplayView:)|为特定用户设置预览视图|
|[enableMic:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableMic:)|打开和关闭麦克风|
|[switchCamera:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/switchCamera:)|切换摄像头|
|[enableVideoAutoRotation:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableVideoAutoResolution:)|是否打开视频方向随设备方向自动变化，默认打|
|[setOutputVideoRotation:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setOutputVideoRotation:)|设置视频输出方向，需要将自动旋转方向关闭才能生效|
|[setAVConfig](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setAVConfig:)|设置视频编码、码率、分辨率等采集参数|
|[getAVConfig](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAVConfig)|获取Video采集、编码、推流等参数配置|
|[setDegradationPreference:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setDegradationPreference:)|设置视频网络自适应模式|
|[setPublishQualityMonitorCycle](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setPublishQualityMonitorCycle:)|设置推流质量信息统计回掉频率|

### <a name='1.4'></a> 拉流和播放、停止拉流

| 方法名 | 说明 |
| --- | --- |
|[startPlayingStream:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startPlayingStream:)|开始拉流|
|[stopPlayingStream:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopPlayingStream:)|停止拉流|
|[enableSpeakerphone:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableSpeakerphone:)|打开和关闭扬声器|
|[setAudioRecordFlag:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setAudioRecordFlag:)|设置音频数据回掉方式|
|[startSoundLevelMonitor:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startSoundLevelMonitor:)|开启音量变化通知|
|[stopSoundLevelMonitor](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopSoundLevelMonitor)|停止音量变化的监听|
|[getSoundLevelByUserId:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getSoundLevelByUserId:)|获取用户音量数据|
|[setPlayQualityMonitorCycle:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setPlayQualityMonitorCycle:)|设置拉流质量信息统计回掉频率|

### <a name='1.5'></a> 版本

| 方法名 | 说明 |
| --- | --- |
|[versionNumber](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/versionName)|获取 SDK 版本号|
|[versionName](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/versionName)|获取 SDK build 版本号|
|[buildVersion](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/buildVersion)|获取 SDK 编译版本号|

## <a name='2'></a> 进阶功能

### <a name='2.1'></a> 混音功能

| 方法名 | 说明 |
| --- | --- |
|[startAudioMixing:replace:loop](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startAudioMixing:replace:loop:)|开启混音功能、并设置混音和循环播放模式|
|[stopAudioMixing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopAudioMixing)|停止混音|
|[pauseAudioMixing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/pauseAudioMixing)|暂停混音|
|[resumeAudioMixing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/resumeAudioMixing)|恢复混音|
|[getAudioMixingVolume](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAudioMixingVolume)|获取混音音量|
|[adjustAudioMixingVolume](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/adjustAudioMixingVolume:)|调整混音音量|
|[getAudioMixingTotalLength](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAudioMixingTotalLength)|获取当前伴奏文件总时长，单位毫秒。请在房间内调用该方法|
|[getAudioMixingCurrentPosition](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAudioMixingCurrentPosition)|获取音乐文件的播放进度。单位为毫秒。请在房间内调用该方法。|
|[setAudioMixingPosition](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setAudioMixingPosition:)|设置音乐文件的播放位置。请在房间内调用该方法。|

### <a name='2.2'></a> 外置音视频采集
###### 本组方法为开发者提供自定义视频采集源的功能，适用于直播场景。

| 方法名 | 说明 |
| --- | --- |
|[enableExternalAudioInput](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableExternalAudioInput:)|打开和关闭外置音频采集功能呢|
|[setExternalAudioConfig:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setExternalAudioConfig:)|设置外置音频采集参数|
|[getExternalAudioConfig](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getExternalAudioConfig)|获取外部音频采集参数配置|
|[sendAudioFrame:length](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sendAudioFrame:length:)|发送外置音频数据|
|[sendVideoFrame:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sendVideoFrame:)|发送外置视频数据|
|[sendVideoFrame:sei:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sendVideoFrame:sei:)|发送外置视频数据并携带附加信息|

### <a name='2.3'></a> 音视频混流

| 方法名 | 说明 |
| --- | --- |
|[mixStream:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/mixStream:)|开始混流并设置混流参数|
|[stopMixStream](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopMixStream)|停止混流|

## <a name='3'></a> 场景功能

### <a name='3.1'></a> 房间 PK，跨房间连麦

| 方法名 | 说明 |
| --- | --- |
|[linkRoom:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/linkRoom:)|开始房间 PK|
|[unlinkRoom:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/unlinkRoom:)|取消房间 PK|

### <a name='3.2'></a> 预览视图设置(本地预览视图和远端视频预览视图)

| 方法名 | 说明 |
| --- | --- |
|[addDisplayView:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/addDisplayView:)|为某个用户添加预览视图|
|[removeDisplayView:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/removeDisplayView:)|移除预览视图|

### <a name='3.3'></a> 房间内事件

| 方法名 | 说明 |
| --- | --- |
|[OnRoomReconnected](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnRoomReconnected)|房间重连成功|
|[OnEnterRoomComplete:users](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnEnterRoomComplete:users:)|房间重连成功|
|[OnExitRoomComplete](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnExitRoomComplete)|退出房间成功|
|[OnRoomDisconnected:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnRoomDisconnected:)|房间断开的通知，网络异常时 SDK 会自动进行重连|
|[OnAddRemoter:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAddRemoter:)|有成员加入的通知|
|[OnDeleteRemoter:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnDeleteRemoter:)|有成员离开的通知|
|[OnMixComplete:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnMixComplete:)|远端混流完成的回掉，用户可以通过调用混乱方法在远端进行音视频混流，参考 mixStream|
|[OnAudioData:audio_data:bits_per_sample:sample_rate:number_of_channels:number_of_frames](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAudioData:audio_data:bits_per_sample:sample_rate:number_of_channels:number_of_frames:)|单路音频流回掉|
|[OnAudioMixStream:samples:nchannel:flag](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAudioMixStream:samples:nchannel:flag:)|混音录音数据回掉，该方法需要打开录音功能才会触发回掉 setAudioRecordFlag:|
|[OnPublishQualityUpdate:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPublishQualityUpdate:)|发布资源质量状态变化的通知|
|[OnPlayQualityUpate:userId:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPlayQualityUpate:userId:)|播放质量变化的通知|
|[OnPublishStateUpdate:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPublishStateUpdate:)|发布资源状态变更的通知|
|[OnPlayStateUpdate:userId:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPlayStateUpdate:userId:)|播放状态变化的通知|
|[OnAudioVolumeUpdate:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAudioVolumeUpdate:)|远端用户音量变化的通知|
|[OnMediaSideInfoInPublishVideoFrame:]()|是否需要在视频帧上附加其他媒体信息|
|[OnDrawFrame:uid:sei](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnDrawFrame:uid:sei:)|收到远端视频数据回掉，如果为 SDK 设置了渲染视图，SDK 内部会自动将该视频帧渲染出来|
|[OnKickOff](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnKickOff:roomId:)|用户被踢出房间|

