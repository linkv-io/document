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

LinkV  SDK have the following functions and usage scenarios


|Type|The main function|Function description|Application scenario|
| --- | --- | :-- | --- |
| Common features | Live push and pull streaming | Support streaming on the host side and streaming on the viewer side | Live video<br/>Show live |
| | Audio and video beam | Support viewers and anchors to interact with the microphone | Live broadcast<br/>PK beam |
| | Audio beam | Support viewers and anchors to interact with beam | Live broadcast<br/>PK beam |
| | Audio and video preprocessing| Support preprocessing before sending audio and video，Such as beauty, watermark, subtitles, audio, etc.| show live<br/>Beauty Sticker |
| ||||
| advanced features | Custom additional data | Support to send the customized data with audio and video, to meet some audio and video special functions, such as lyrics synchronization, VR additional data, etc. | KTV Room<br/>Live video broadcast |
|| Customizing audio and video rendering|Support user-defined video rendering, customized audio playback function|Audio and Video processing|
|| Customizing the audio and video capture|Support user-defined video and audio capture functions, such as external microphones, external cameras, mixers, etc.|Movies<br/>Internet online education|
|| Stream mixing|Support the interaction of multi-beam audio and video to mix into singles stream.|Broadcaster interaction<br/>Muli-beam live stream|

## <a name='2'></a>2、Key indicator

|Characteristic|Platform and features|Index|
| --- | --- | --- |
| SDK package size | android | Size: 19.1MB |
| Multi-beam audio and video interaction|Video capture and transmission|1080p 30fps video data|
|Multi-beam audio and video interaction|Audio capture and transmission|48000 hz、 mono and stereo|
| Latency |Video|High quality network：< 20ms<br>ordinary network：200ms-1s|
| Latency |Audio|High quality network：< 20ms<br>ordinary network：< 200ms |

## <a name='3'></a>3、Integration Process

![](https://dl.linkv.io/doc/en/android/rtc/images/sdk_init.png)

First, you need to register a LinkV developer account. Then log into the developer platform after registering a developer account, , and create an application to obtain the corresponding AppKey. AppSecret will be used when initializing the SDK.

After obtaining the relevant Key, you can download the integrated SDK according to the integrated documents, and then initialize the SDK and use AppKey, AppSecret process the authentication, and after the initialization and authentication are successful, you can use the SDK to publish and play live streaming.

## <a name='4'></a>4、Demo

Demo contains the basic application functions of interactive live broadcast, group chat, and video call as 3 different application scenarios.

* [android Demo](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq)

