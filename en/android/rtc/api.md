# The API Summary

###### This summary mainly includes methods for initializing SDK and the basic audio-video communication, and is suitable for the application scenarios such as voice calls, video calls, and voice/video live streaming etc.

## <a name='1'></a> The basic functions
###### This category mainly includes methods for initializing SDK and basic audio and video communication, and is suitable for application scenarios such as voice calls, video calls, and voice/video live broadcast etc.

### <a name='1.1'></a> Initialization

| Methods | Description |
| --- | --- |
|[getInstance](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getInstance-Context-)|Obtain the LVRTCEngine singleton|
|[initSDK](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#initSDK--)|Initialize the SDK before using the SDK|
|[unInitSDK](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#unInitSDK--)|Release SDK and the related resources|
|[setISOCountryCode](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setISOCountryCode-java.lang.String-)|Set the country code, SDK supported information(optional)|
|[setLogLevel](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setLogLevel-int-)|Set the log level|
|[setUseTestEnv](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setUseTestEnv-boolean-)|Set whether to use the test environment|
|[setUseInternationalEnv](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setUseInternationalEnv-boolean-)|Whether to use the international version (SDK uses the China version by default)|
|[setDebugServerIp](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setDebugServerIp-java.lang.String-)|Set the debugging service IP(optional)|
|[setLiveRoomCallback](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setLiveRoomCallback-com.linkv.rtc.callback.LVRTCCallback-)|Set decoding pixel format|

### <a name='1.2'></a> Authentication, log in/out

| Methods | Description |
| --- | --- |
| [auth](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#auth-java.lang.String-java.lang.String-java.lang.String-com.linkv.rtc.callback.LVResultCallback1-) | SDK authentication, the authentication must be successful before using SDK |
|[loginRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#loginRoom-java.lang.String-java.lang.String-boolean-boolean-com.linkv.rtc.callback.LVResultCallback2-)| Log in to the room , you need to log in to the room before publishing resources, making the voice/video calls, and starting to play the video stream, and set the delegate callback for the RTC engine |
|[logoutRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#logoutRoom-com.linkv.rtc.callback.LVResultCallback1-)|Log out of the room and clean up resources|

### <a name='1.3'></a> Publishing Stream

| Methods | Description |
| --- | --- |
|[startPublishing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startPublishing--)|Start to publish the live streaming, the audience can also call this function to connect with the host, please note that this function needs to be used with startCapture |
|[stopPublishing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopPublishing--)|Stop the push stream|
|[startCapture](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startCapture--)|Start video capture|
|[stopCapture](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopCapture--)|Stop video capture|
|[addDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#addDisplayView-Context-com.linkv.rtc.render.LVDisplayView-)|Set a dislpayview for specific users|
|[enableMic](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableMic-boolean-)|on/off the microphone|
|[switchCamera](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#switchCamera-com.linkv.rtc.LVConstants.CMRTCCameraPosition-)|Switching the cameras|
|[enableVideoAutoRotation](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableVideoAutoRotation-boolean-)|Whether to enable the video rotation automatically by the rotation change of the device, default is enabled|
|[setOutputVideoRotation](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setOutputVideoRotation-com.linkv.rtc.LVConstants.CMVideoRotation-)|Set the video output rotation, you need to disable the automatic rotation to activate this function.|
|[setAVConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setAVConfig-com.linkv.rtc.entity.LVAVConfig-)|Set the parameters such as video encoding, bitrate and resolution|
|[getAVConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAVConfig--)|Obtain parameter configuration such as video capture, encoding, and publishing stream|
|[setVideoEncoderMode](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setVideoEncoderMode-int-)|设置视频编码器模式|
|[setLVRenderCallback](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setLVRenderCallback-com.linkv.rtc.callback.LVRenderCallback-)|设置视频渲染回调|
|[setPublishQualityMonitorCycle](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPublishQualityMonitorCycle-int-)|Set the frequency for the statistic data of publishing stream callback|

### <a name='1.4'></a> Playing Stream

| Methods | Description |
| --- | --- |
|[startPlayingStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startPlayingStream-java.lang.String-)|Start to play stream|
|[stopPlayingStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopPlayingStream-java.lang.String-)|Stop playing steam|
|[enableSpeakerphone](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableSpeakerphone-boolean-)|on/off the speaker|
|[isSpeakerphoneOn](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#isSpeakerphoneOn--)|Is the speaker turned on|
|[setAudioRecordFlag](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setAudioRecordFlag-com.linkv.rtc.LVConstants.AudioRecordType...-)|Set audio recording mode，Multiple recording modes can be set at the same time|
|[startSoundLevelMonitor](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startSoundLevelMonitor-int-)|Enable the notification for changing the volume|
|[stopSoundLevelMonitor](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopSoundLevelMonitor--)|Stop the volume change monitoring|
|[getSoundLevelByUserId](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getSoundLevelByUserId-java.lang.String-)|obtain user's volume data|
|[setVideoDecoderMode](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setVideoDecoderMode-int-)|Set video decoder mode|
|[setPlayQualityMonitorCycle](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPlayQualityMonitorCycle-int-)|Set the frequency for the statistic data of playing stream callback|
|[setPlayVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPlayVolume-int-)|Control the volume of the remote audio stream, call after successfully joining the room|
|[setPlayVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setPlayVolume-java.lang.String-int-)|Control the volume of all remote audio streams, Called after successfully joining the room|

### <a name='1.5'></a> Version

| Methods | Description |
| --- | --- |
|[versionNumber](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#versionNumber--)|Get the SDK version number|
|[versionName](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#versionName--)|Get the SDK build version number|
|[buildVersion](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#buildVersion--)|Get the SDK compiled version number|

## <a name='2'></a> Advanced Features

### <a name='2.1'></a> Audio Mixing function

| Methods | Description |
| --- | --- |
|[startAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#startAudioMixing-java.lang.String-boolean-int-)|Enable the mixing function, and configure the audio mixing and the loop mode|
|[stopAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopAudioMixing--)|Stop the mixing|
|[pauseAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#pauseAudioMixing--)|Pause the mixing|
|[resumeAudioMixing](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#resumeAudioMixing--)|Resume the mixing|
|[getAudioMixingVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAudioMixingVolume--)|Obtain the mixing volume|
|[adjustAudioMixingVolume](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#adjustAudioMixingVolume-int-)|Adjust the mixing volume|
|[getAudioMixingTotalLength](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAudioMixingTotalLength--)|Get the total duration/length of the current accompaniment file in ms. Please call this method in the room.|
|[getAudioMixingCurrentPosition](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getAudioMixingCurrentPosition--)|Get the playback progress of music files. Unit: ms. Please call this method in the room.|
|[setAudioMixingPosition](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setAudioMixingPosition-int-)|Set the path location of the music files. Please call this method in the room.|

### <a name='2.2'></a> External audio and video capture

###### This group of methods provides the developers with the ability to customize video capture sources, which is suitable for live broadcasting scenarios.

| Methods | Description |
| --- | --- |
|[enableExternalAudioInput](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#enableExternalAudioInput-boolean-)|On/Off the external audio capture function|
|[setExternalAudioConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#setExternalAudioConfig-com.linkv.rtc.entity.LVExternalAudioConfig-)|Set up the external audio capture parameters|
|[getExternalAudioConfig](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#getExternalAudioConfig--)|Get the configuration for the external audio capture parameter|
|[sendAudioFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#sendAudioFrame-byte:A-)|Send external audio data|
|[sendVideoFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#sendVideoFrame-java.nio.ByteBuffer-int-int-int-int-long-java.lang.String-)|Send external video data，External input byte format video data，Currently only supports I420 format|
|[sendVideoFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#sendVideoFrame-int-int-int-float:A-long-java.lang.String-)|Send external video data and attach the additional information|

### <a name='2.3'></a> Stream mixing

| Methods | Description |
| --- | --- |
|[mixStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#mixStream-com.linkv.rtc.entity.LVMixStreamConfig-)|Start the mixed streams and configuring the mixed stream parameters|
|[stopMixStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#stopMixStream--)|Stop the mixing|

## <a name='3'></a> Scenarios

### <a name='3.1'></a> Across room live streaming

| Methods | Description |
| --- | --- |
|[linkRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#linkRoom-java.lang.String-)|Start to link room|
|[unlinkRoom](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#unlinkRoom-java.lang.String-)|Cancel the room link|

### <a name='3.2'></a> Displayview settings (local displayview and remote video displayview)

| Methods | Description |
| --- | --- |
|[addDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#addDisplayView-Context-com.linkv.rtc.render.LVDisplayView-)|Add the dispalyview for a specific user|
|[removeDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#removeDisplayView-com.linkv.rtc.render.LVDisplayView-)|Remove the dispayview|
|[removeDisplayView](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/LVRTCEngine.html#removeDisplayView-java.lang.String-)|Remove display view based on uid|

### <a name='3.3'></a> In-room events

| Methods | Description |
| --- | --- |
|[onRoomReconnected](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onRoomReconnected--)|Reconnected room successfully|
|[onRoomDisconnected](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onRoomDisconnected-int-)|Room disconnect notification, SDK will automatically reconnect when the network is abnormal|
|[onAddRemoter](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onAddRemoter-com.linkv.rtc.entity.LVUser-)|Notification of someone have joined the room|
|[onDeleteRemoter](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onDeleteRemoter-java.lang.String-)|Notification when someone left|
|[onMixComplete](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onMixComplete-boolean-)|Notification when the stream mixing is completed. The user can mix the audio and video by calling the stream mixing method. please refer to mixStream|
|[onAudioMixStream](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onAudioMixStream-byte:A-int-int-int-int-com.linkv.rtc.LVConstants.AudioRecordType-)|The mixed recording data is returned, this method needs to turn on the recording function to trigger the return setAudioRecordFlag:|
|[onPublishQualityUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPublishQualityUpdate-com.linkv.rtc.entity.LVVideoStatistic-)|Notification of statistic quality of publishing streaming|
|[onPlayQualityUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPlayQualityUpdate-com.linkv.rtc.entity.LVVideoStatistic-java.lang.String-)|Notification of statistic quality of playing streaming|
|[onPublishStateUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPublishStateUpdate-int-)|Notification of changes in publishing status|
|[onPlayStateUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onPlayStateUpdate-int-java.lang.String-)|Notification of changes in playing status|
|[onAudioVolumeUpdate](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onAudioVolumeUpdate-java.util.ArrayList-)|Notification of remote user volume changes|
|[onMediaSideInfoInPublishVideoFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onMediaSideInfoInPublishVideoFrame--)|whether to attach additional information to the other media data|
|[onDrawFrame](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onDrawFrame-java.nio.ByteBuffer-int-int-int-java.lang.String-java.lang.String-)|The callback of receiving the remote video data, if the rendering view is setted for the SDK, the video frame will be rendered inside the SDK automatically|
|[onExitRoomComplete](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onExitRoomComplete--)|Room exit successfully callback|
|[onKickOff](https://dl.linkv.io/static/Android/RTC/api/com/linkv/rtc/callback/LVRTCCallback.html#onExitRoomComplete--)|Users get kicked out of the room|

