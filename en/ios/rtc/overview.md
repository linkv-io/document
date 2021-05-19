# Real-time Audio and Live video broadcast SDK

## Linkv SDK Introduction

LinkV SDK provides multi-platform with fast connectivity, high-definition video fluency, low latency, high concurrency and scalable audio-video services，Live stream, one-to-many and many-to-many real-time audio-video call, video conference and other occasions. The audio-video service is global deployment, to meet the different countries and regions of audio-video functional access.

## Application Scenarios

The LinkV SDK provides three application scenarios by default:

* Interactive Live broadcast
  + Users of interactive live broadcast scenarios are divided into broadcasters and audience. The broadcasters can create the live broadcast room, the audience are free to join, and the broadcasters can speak freely, and the audience can initiate a chat invitation and connect with the broadcasters.
* Group voice calls
  + The group voice call is suitable for video conference, voice chat and other application scenarios. A group of people can start the real-time voicecall in a chat room.
* video calls
  + The video call does not distinguish between the broadcasters and the audience, and mutual users can speak freely.

## <a name='1'></a>1、Function and Scenario

LinkV SDK has the following features, and the application scenarios.

|Category|Features|Function description|Typical application scenarios|
| --- | --- | :-- | --- |
| common function | Publish-play live streaming | Support the push-stream on the side of broadvasters and the pull-stream on the side of audience | Live video Broadcast<br/>Live show broadcast |
| | Audio-Video Multi-beam | Support the audience and broadcasters interact with each other through multi-beam video/audio broadcast mode. | Multi-beam Live video Broadcast<br/>Multi-beam video broadcast PK mode. |
| | Multi-beam Audio broadcast | Support the audience and broadcasters interact with each other through multi-beam audio broadcast mode. |  Mult-beam live audio broadcast<br/>Multi-beam audio broadcast PK mode |
| | Audio-video pre-possessing | Support the pre-processing before sending audio and video, such as beauty filters/stickers, watermark, subtitle, audio change, reverb, ear-return effect, etc. | Live show<br/>beauty stickers |
| | Audio-Video Post-processing | Support audio and video offline save and replay | Video replay<br/>Video on Demand Function (VOD) |
| ||||
| advanced features | Custom additional data | Support to send the customized data with audio and video, to meet some audio and video special functions, such as lyrics synchronization, VR additional data, etc. | KTV Room<br/>Live video broadcast |
|| Customizing audio and video rendering|Support user-defined video rendering, customized audio playback function|Audio and Video processing|
|| Customizing the audio and video capture|Support user-defined video and audio capture functions, such as external microphones, external cameras, mixers, etc.|Movies<br/>Internet online education|
|| Stream mixing|Support the interaction of multi-beam audio and video to mix into singles stream.|Broadcaster interaction<br/>Muli-beam live stream|

## <a name='2'></a>2、Key indicator

|Characteristic|Platform and features|Index|
| --- | --- | --- |
| SDK package size | iOS | Size: 33.1M |
| Multi-beam audio and video interaction|Video capture and transmission|1080p 30fps video data|
| Multi-beam audio and video interaction|Audio capture and transmission|48000 hz、 mono and stereo|
| Latency |Video|High quality network：< 20ms<br>ordinary network：200ms-1s|
| Latency |Audio|High quality network：< 20ms<br>ordinary network：<200ms|

## <a name='3'></a>3、Integration Process

![](https://dl.linkv.io/doc/en/ios/rtc/images/sdk_init.png)

First, you need to register a LinkV developer account. Then log into the developer platform after registering a developer account, , and create an application to obtain the corresponding AppKey. AppSecret will be used when initializing the SDK.

After obtaining the relevant Key, you can download the integrated SDK according to the integrated documents, and then initialize the SDK and use AppKey, AppSecret process the authentication, and after the initialization and authentication are successful, you can use the SDK to publish and play live streaming.

## <a name='4'></a>4、Demo

Demo contains the basic application functions of interactive live broadcast, group chat, and video call as 3 different application scenarios.

* [iOS Demo](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq)
