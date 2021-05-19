# 文档使用 API 汇总

###### 此分类下主要包括初始化 SDK 和基本音视频通信的方法，适用于语音通话、视频通话、语音/视频直播等应用场景。

## <a name='1'></a> 基础功能
###### 此分类下主要包括初始化 SDK 和基本音视频通信的方法，适用于语音通话、视频通话、语音/视频直播等应用场景

### <a name='1.1'></a> 初始化

| 方法名 | 说明 |
| --- | --- |
|[getInstance](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getInstance-Context-)|获取 LVRTCEngine 单例|
|[initSDK](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#initSDK--)|初始化SDK，使用 SDK 前请先初始化 SDK|
|[unInitSDK](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#unInitSDK--)|卸载SDK，资源释放|
|[setISOCountryCode](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setISOCountryCode-java.lang.String-)|设置国家码，SDK 辅助信息，可以不传|
|[setLogLevel](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setLogLevel-int-)|设置日志级别|
|[setUseTestEnv](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setUseTestEnv-boolean-)|设置是否使用测试环境|
|[setUseInternationalEnv](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setUseInternationalEnv-boolean-)|是否使用国际服务器环境（默认使用中国环境）|
|[setDebugServerIp](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setDebugServerIp-java.lang.String-)|设置调试服务 url，可以不传|
|[setLiveRoomCallback](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setLiveRoomCallback-com.linkv.rtc.callback.LVRTCCallback-)|设置引擎回调|

### <a name='1.2'></a> 鉴权、登录和登出

| 方法名 | 说明 |
| --- | --- |
| [auth](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#auth-java.lang.String-java.lang.String-java.lang.String-com.linkv.rtc.callback.LVResultCallback1-) | SDK 鉴权，使用 SDK 时必须确保鉴权成功才能使用 |
|[loginRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#loginRoom-java.lang.String-java.lang.String-boolean-boolean-com.linkv.rtc.callback.LVResultCallback2-)| 登陆房间接口，发布资源、连麦、开始播放视频流之前需要先登陆房间，同时为 RTC 引擎设置监听回调 |
|[logoutRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#logoutRoom-com.linkv.rtc.callback.LVResultCallback1-)|登出房间、清理资源|

### <a name='1.3'></a> 推流和推流参数设置

| 方法名 | 说明 |
| --- | --- |
|[startPublishing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startPublishing--)|开始推流 |
|[stopPublishing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopPublishing--)|停止推流|
|[startCapture](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startCapture--)|开始视频采集|
|[stopCapture](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopCapture--)|停止视频采集|
|[addDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#addDisplayView-Context-com.linkv.rtc.render.LVDisplayView-)|为特定用户设置预览视图|
|[enableMic](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableMic-boolean-)|设置推流是否静音|
|[switchCamera](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#switchCamera-com.linkv.rtc.LVConstants.CMRTCCameraPosition-)|切换摄像头|
|[enableVideoAutoRotation](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableVideoAutoRotation-boolean-)|设置是否允许 SDK 自动根据设备的方向调整视频的输出方向，默认是true|
|[setOutputVideoRotation](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setOutputVideoRotation-com.linkv.rtc.LVConstants.CMVideoRotation-)|设置视频输出方向，需要将自动旋转方向关闭才能生效|
|[setAVConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setAVConfig-com.linkv.rtc.entity.LVAVConfig-)|设置Video采集、编码推流等参数|
|[getAVConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAVConfig--)|获取Video采集、编码、推流等参数配置|
|[setVideoEncoderMode](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setVideoEncoderMode-int-)|设置视频编码器模式|
|[setLVRenderCallback](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setLVRenderCallback-com.linkv.rtc.callback.LVRenderCallback-)|设置视频渲染回调|
|[setPublishQualityMonitorCycle](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPublishQualityMonitorCycle-int-)|设置推流质量信息统计回掉频率|

### <a name='1.4'></a> 拉流和播放、停止拉流

| 方法名 | 说明 |
| --- | --- |
|[startPlayingStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startPlayingStream-java.lang.String-)|开始拉流|
|[stopPlayingStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopPlayingStream-java.lang.String-)|停止拉流|
|[enableSpeakerphone](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableSpeakerphone-boolean-)|打开和关闭扬声器|
|[isSpeakerphoneOn](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#isSpeakerphoneOn--)|扬声器是否开启|
|[setAudioRecordFlag](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setAudioRecordFlag-com.linkv.rtc.LVConstants.AudioRecordType...-)|设置音频录制模式，可同时设置多种录制模式|
|[startSoundLevelMonitor](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startSoundLevelMonitor-int-)|开启音量变化通知|
|[stopSoundLevelMonitor](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopSoundLevelMonitor--)|停止音量变化的监听|
|[getSoundLevelByUserId](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getSoundLevelByUserId-java.lang.String-)|获取用户音量大小|
|[setVideoDecoderMode](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setVideoDecoderMode-int-)|设置视频解码器模式|
|[setPlayQualityMonitorCycle](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPlayQualityMonitorCycle-int-)|设置拉流质量信息统计回掉频率|
|[setPlayVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPlayVolume-int-)|控制远端音频流音量, 加入房间成功后调用|
|[setPlayVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPlayVolume-java.lang.String-int-)|控制所有远端音频流音量, 加入房间成功后调用|

### <a name='1.5'></a> 版本

| 方法名 | 说明 |
| --- | --- |
|[versionNumber](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#versionNumber--)|获取 SDK 主版本号|
|[versionName](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#versionName--)|获取 SDK 主版本名称|
|[buildVersion](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#buildVersion--)|获取 SDK 编译版本号|

## <a name='2'></a> 进阶功能

### <a name='2.1'></a> 混音功能

| 方法名 | 说明 |
| --- | --- |
|[startAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startAudioMixing-java.lang.String-boolean-int-)|开始播放音乐文件及混音|
|[stopAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopAudioMixing--)|停止播放音乐文件及混音|
|[pauseAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#pauseAudioMixing--)|暂停播放音乐文件及混音|
|[resumeAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#resumeAudioMixing--)|恢复播放音乐文件及混音|
|[getAudioMixingVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAudioMixingVolume--)|获取当前伴奏音量|
|[adjustAudioMixingVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#adjustAudioMixingVolume-int-)|调节音乐文件的播放音量|
|[getAudioMixingTotalLength](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAudioMixingTotalLength--)|获取当前伴奏文件总时长，单位毫秒。请在房间内调用该方法|
|[getAudioMixingCurrentPosition](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAudioMixingCurrentPosition--)|获取音乐文件的播放进度。单位为毫秒。请在房间内调用该方法。|
|[setAudioMixingPosition](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setAudioMixingPosition-int-)|设置音乐文件的播放位置。请在房间内调用该方法。|

### <a name='2.2'></a> 外置音视频采集
###### 本组方法为开发者提供自定义视频采集源的功能，适用于直播场景。

| 方法名 | 说明 |
| --- | --- |
|[enableExternalAudioInput](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableExternalAudioInput-boolean-)|打开或关闭外置音频采集|
|[setExternalAudioConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setExternalAudioConfig-com.linkv.rtc.entity.LVExternalAudioConfig-)|设置外置音频采集参数|
|[getExternalAudioConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getExternalAudioConfig--)|获取外部音频采集参数配置|
|[sendAudioFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#sendAudioFrame-byte:A-)|发送外置音频数据|
|[sendVideoFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#sendVideoFrame-java.nio.ByteBuffer-int-int-int-int-long-java.lang.String-)|发送外置视频数据，外部输入byte格式视频数据，目前只支持I420格式|
|[sendVideoFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#sendVideoFrame-int-int-int-float:A-long-java.lang.String-)|发送外置视频数据，外部输入texture格式视频数据|

### <a name='2.3'></a> 音视频混流

| 方法名 | 说明 |
| --- | --- |
|[mixStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#mixStream-com.linkv.rtc.entity.LVMixStreamConfig-)|开始服务端混流|
|[stopMixStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopMixStream--)|停止服务端混流|

## <a name='3'></a> 场景功能

### <a name='3.1'></a> 房间 PK，跨房间连麦

| 方法名 | 说明 |
| --- | --- |
|[linkRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#linkRoom-java.lang.String-)|跨房间连麦|
|[unlinkRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#unlinkRoom-java.lang.String-)|取消跨房间连麦|

### <a name='3.2'></a> 视频显示视图设置(本地视频视图和远端视频视图)

| 方法名 | 说明 |
| --- | --- |
|[addDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#addDisplayView-Context-com.linkv.rtc.render.LVDisplayView-)|设置视频显示视图|
|[removeDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#removeDisplayView-com.linkv.rtc.render.LVDisplayView-)|移除显示视图|
|[removeDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#removeDisplayView-java.lang.String-)|根据uid移除显示视图|

### <a name='3.3'></a> 房间内事件

| 方法名 | 说明 |
| --- | --- |
|[onRoomReconnected](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onRoomReconnected--)|房间重连成功|
|[onRoomDisconnected](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onRoomDisconnected-int-)|房间断开的通知，网络异常时 SDK 会自动进行重连|
|[onAddRemoter](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onAddRemoter-com.linkv.rtc.entity.LVUser-)|有成员加入的通知|
|[onDeleteRemoter](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onDeleteRemoter-java.lang.String-)|有成员离开的通知|
|[onMixComplete](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onMixComplete-boolean-)|远端混流完成的回掉，用户可以通过调用混乱方法在远端进行音视频混流，参考 mixStream|
|[onAudioMixStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onAudioMixStream-byte:A-int-int-int-int-com.linkv.rtc.LVConstants.AudioRecordType-)|混音录音数据回掉，该方法需要打开录音功能才会触发回掉 setAudioRecordFlag:|
|[onPublishQualityUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPublishQualityUpdate-com.linkv.rtc.entity.LVVideoStatistic-)|发布资源质量状态变化的通知|
|[onPlayQualityUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPlayQualityUpdate-com.linkv.rtc.entity.LVVideoStatistic-java.lang.String-)|播放质量变化的通知|
|[onPublishStateUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPublishStateUpdate-int-)|发布资源状态变更的通知|
|[onPlayStateUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPlayStateUpdate-int-java.lang.String-)|播放状态变化的通知|
|[onAudioVolumeUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onAudioVolumeUpdate-java.util.ArrayList-)|音量变化回调|
|[onMediaSideInfoInPublishVideoFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onMediaSideInfoInPublishVideoFrame--)|是否需要在视频帧上附加其他媒体信息|
|[onDrawFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onDrawFrame-java.nio.ByteBuffer-int-int-int-java.lang.String-java.lang.String-)|收到远端视频数据回掉，如果为 SDK 设置了渲染视图，SDK 内部会自动将该视频帧渲染出来|
|[onExitRoomComplete](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onExitRoomComplete--)|房间退出成功回调|
|[onKickOff](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onExitRoomComplete--)|用户被踢出房间|

