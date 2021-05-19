# The API Summary

###### This summary mainly includes methods for initializing SDK and the basic audio-video communication, and is suitable for the application scenarios such as voice calls, video calls, and voice/video live streaming etc.

## <a name='1'></a> The basic functions
###### This category mainly includes methods for initializing SDK and basic audio and video communication, and is suitable for application scenarios such as voice calls, video calls, and voice/video live broadcast etc.

### <a name='1.1'></a> Initialization

| Methods | Description |
| --- | --- |
|[sharedInstance](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sharedInstance)|Obtain the LVRTCEngine singleton|
|[initSdk](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/initSdk)|Initialize the SDK before using the SDK|
|[unInitSDK](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/unInitSDK)|Release SDK and the related resources|
|[setISOCountryCode](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setISOCountryCode:)|Set the country code, SDK supported information(optional)|
|[setLogLevel:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setLogLevel:)|Set the log level|
|[setUseTestEnv:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setUseTestEnv:)|Set whether to use the test environment|
|[setUseInternationalEnv:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setUseInternationalEnv:)|Whether to use the international version (SDK uses the China version by default)|
|[setDebugServerIp:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setDebugServerIp:)|Set the debugging service IP(optional)|
|[setDecoderPixelType:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setDecoderPixelType:)|Set decoding pixel format|

### <a name='1.2'></a> Authentication, log in/out

| Methods | Description |
| --- | --- |
| [auth:skStr:userId:completion](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/auth:skStr:userId:completion:) | SDK authentication, the authentication must be successful before using SDK |
|[loginRoom:roomId:isHost:isOnlyAudio:delegate](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/loginRoom:roomId:isHost:isOnlyAudio:delegate:)| Log in to the room , you need to log in to the room before publishing resources, making the voice/video calls, and starting to play the video stream, and set the delegate callback for the RTC engine |
|[logoutRoom:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/logoutRoom:)|Log out of the room and clean up resources|

### <a name='1.3'></a> Publishing Stream

| Methods | Description |
| --- | --- |
|[startPublishing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startPublishing)|Start to publish the live streaming, the audience can also call this function to connect with the host, please note that this function needs to be used with startCapture |
|[stopPublishing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopPublishing)|Stop the push stream|
|[startCapture](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startCapture)|Start video capture|
|[stopCapture](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopCapture)|Stop video capture|
|[addDisplayView:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/addDisplayView:)|Set a dislpayview for specific users|
|[enableMic:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableMic:)|on/off the microphone|
|[switchCamera:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/switchCamera:)|Switching the cameras|
|[enableVideoAutoRotation:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableVideoAutoResolution:)|Whether to enable the video rotation automatically by the rotation change of the device, default is enabled|
|[setOutputVideoRotation:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setOutputVideoRotation:)|Set the video output rotation, you need to disable the automatic rotation to activate this function.|
|[setAVConfig](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setAVConfig:)|Set the parameters such as video encoding, bitrate and resolution|
|[getAVConfig](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAVConfig)|Obtain parameter configuration such as video capture, encoding, and publishing stream|
|[setDegradationPreference:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setDegradationPreference:)|Set adaptive streaming mode|
|[setPublishQualityMonitorCycle](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setPublishQualityMonitorCycle:)|Set the frequency for the statistic data of publishing stream callback|

### <a name='1.4'></a> Playing Stream

| Methods | Description |
| --- | --- |
|[startPlayingStream:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startPlayingStream:)|Start to play stream|
|[stopPlayingStream:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopPlayingStream:)|Stop playing steam|
|[enableSpeakerphone:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableSpeakerphone:)|on/off the speaker|
|[setAudioRecordFlag:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setAudioRecordFlag:)|Set the callback method for audio data|
|[startSoundLevelMonitor:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startSoundLevelMonitor:)|Enable the notification for changing the volume|
|[stopSoundLevelMonitor](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopSoundLevelMonitor)|Stop the volume change monitoring|
|[getSoundLevelByUserId:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getSoundLevelByUserId:)|obtain user's volume data|
|[setPlayQualityMonitorCycle:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setPlayQualityMonitorCycle:)|Set the frequency for the statistic data of playing stream callback|

### <a name='1.5'></a> Version

| Methods | Description |
| --- | --- |
|[versionNumber](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/versionName)|Get the SDK version number|
|[versionName](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/versionName)|Get the SDK build version number|
|[buildVersion](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/buildVersion)|Get the SDK compiled version number|

## <a name='2'></a> Advanced Features

### <a name='2.1'></a> Audio Mixing function

| Methods | Description |
| --- | --- |
|[startAudioMixing:replace:loop](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/startAudioMixing:replace:loop:)|Enable the mixing function, and configure the audio mixing and the loop mode|
|[stopAudioMixing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopAudioMixing)|Stop the mixing|
|[pauseAudioMixing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/pauseAudioMixing)|Pause the mixing|
|[resumeAudioMixing](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/resumeAudioMixing)|Resume the mixing|
|[getAudioMixingVolume](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAudioMixingVolume)|Obtain the mixing volume|
|[adjustAudioMixingVolume](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/adjustAudioMixingVolume:)|Adjust the mixing volume|
|[getAudioMixingTotalLength](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAudioMixingTotalLength)|Get the total duration/length of the current accompaniment file in ms. Please call this method in the room.|
|[getAudioMixingCurrentPosition](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getAudioMixingCurrentPosition)|Get the playback progress of music files. Unit: ms. Please call this method in the room.|
|[setAudioMixingPosition](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setAudioMixingPosition:)|Set the path location of the music files. Please call this method in the room.|

### <a name='2.2'></a> External audio and video capture

###### This group of methods provides the developers with the ability to customize video capture sources, which is suitable for live broadcasting scenarios.

| Methods | Description |
| --- | --- |
|[enableExternalAudioInput](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/enableExternalAudioInput:)|On/Off the external audio capture function|
|[setExternalAudioConfig:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/setExternalAudioConfig:)|Set up the external audio capture parameters|
|[getExternalAudioConfig](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/getExternalAudioConfig)|Get the configuration for the external audio capture parameter|
|[sendAudioFrame:length](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sendAudioFrame:length:)|Send the external audio data|
|[sendVideoFrame:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sendVideoFrame:)|Send the external video data|
|[sendVideoFrame:sei:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/sendVideoFrame:sei:)|Send external video data and attach the additional information|

### <a name='2.3'></a> Stream mixing

| Methods | Description |
| --- | --- |
|[mixStream:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/mixStream:)|Start the mixed streams and configuring the mixed stream parameters|
|[stopMixStream](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/stopMixStream)|Stop the mixing|

## <a name='3'></a> Scenarios

### <a name='3.1'></a> Across room live streaming

| Methods | Description |
| --- | --- |
|[linkRoom:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/linkRoom:)|Start to link room|
|[unlinkRoom:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/unlinkRoom:)|Cancel the room link|

### <a name='3.2'></a> Displayview settings (local displayview and remote video displayview)

| Methods | Description |
| --- | --- |
|[addDisplayView:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/addDisplayView:)|Add the dispalyview for a specific user|
|[removeDisplayView:](https://dl.linkv.io/static/iOS/RTC/api/Classes/LVRTCEngine.html#//api/name/removeDisplayView:)|Remove the dispayview|

### <a name='3.3'></a> In-room events

| Methods | Description |
| --- | --- |
|[OnRoomReconnected](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnRoomReconnected)|Reconnected room successfully|
|[OnEnterRoomComplete:users](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnEnterRoomComplete:users:)|Enter room successfully|
|[OnExitRoomComplete](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnExitRoomComplete)|Exit room successfully|
|[OnRoomDisconnected:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnRoomDisconnected:)|Notification of room disconnection, SDK will automatically reconnect when the network is insufficient|
|[OnAddRemoter:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAddRemoter:)|Notification of someone have joined the room|
|[OnDeleteRemoter:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnDeleteRemoter:)|Notification when someone left|
|[OnMixComplete:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnMixComplete:)|Notification when the stream mixing is completed. The user can mix the audio and video by calling the stream mixing method. please refer to mixStream|
|[OnAudioData:audio_data:bits_per_sample:sample_rate:number_of_channels:number_of_frames](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAudioData:audio_data:bits_per_sample:sample_rate:number_of_channels:number_of_frames:)|The callback of single audio stream|
|[OnAudioMixStream:samples:nchannel:flag](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAudioMixStream:samples:nchannel:flag:)|The mixed recording data is returned. This method needs to enable the recording function to trigger the setAudioRecordFlag:|
|[OnPublishQualityUpdate:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPublishQualityUpdate:)|Notification of statistic quality of publishing streaming|
|[OnPlayQualityUpate:userId:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPlayQualityUpate:userId:)|Notification of statistic quality of playing streaming|
|[OnPublishStateUpdate:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPublishStateUpdate:)|Notification of changes in publishing status|
|[OnPlayStateUpdate:userId:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnPlayStateUpdate:userId:)|Notification of changes in playing status|
|[OnAudioVolumeUpdate:](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnAudioVolumeUpdate:)|Notification of remote user volume changes|
|[OnMediaSideInfoInPublishVideoFrame:]()|whether to attach additional information to the other media data|
|[OnDrawFrame:uid:sei](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnDrawFrame:uid:sei:)|The callback of receiving the remote video data, if the rendering view is setted for the SDK, the video frame will be rendered inside the SDK automatically|
|[OnKickOff](https://dl.linkv.io/static/iOS/RTC/api/Protocols/LVRTCEngineDelegate.html#//api/name/OnKickOff:roomId:)|Users get kicked out of the room|
