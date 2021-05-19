# Publishing Streams

## <a name='1'></a>1、Introduction

In the scenarios such as group calls and interactive live broadcasting, to make other people be able to see their own pictures and hear their own voices, they need to publish their own audio and video to the cloud server. Then the peer receives the audio and video streams from the cloud to acquire the video and voices.

## <a name='3'></a>3、Procedures

### The publishing stream API

* You will be able to publish the streams once you have logged into the room. **You have to enable camera capture before publishing the audio and video streams**.

* If the isOnlyAudio parameter is YES, then only the audio data will be sent. Which means the peer can only receive the audio data.

``` objc
// Publish the video data（publish stream）
[[LVRTCEngine sharedInstance] startPublishing];

// Stop publishing video data
[[LVRTCEngine sharedInstance] stopPublishing];
```

### Callback method for publishing stream

* After calling **startPublishing** to publish the streams, the SDK will trigger the callback to notify whether it is successful or return the corresponding error code.

* Error codes may refer to  [the callback erro codes for the status change of push streams](/?p=/en/ios/rtc/ecode.md&k=WZsw8kGY).

```objective-c
// the callback will be triggered after calling startPublishing method
// @param code Status code

* (void)OnPublishStateUpdate:(LVErrorCode)code; 

``` 

## <a name='4'></a>4、Steps in the business scenario

#### The steps of publishing stream can be referred to as follows:

* **Host - create a live room and start to publish stream**

  1. startCapture: enable the camera capture

  2. addDisplayView: add the binding for rendering the displayview of the publish streams

  3. loginRoom: log in to the room and wait to publish in OnEnterRoomComplete.

  4. **startPublishing:** start streaming

* **Audience - participate in the live room and start to publish stream**
  1. loginRoom: log in to the room, and play all the streams of the room in OnEnterRoomComplete.

  2. addDisplayView: add the binding for rendering the displayview of publish streams and specify the displayview uid. 

  3. startPlayingStream: play the streams of the room.

## <a name='5'></a>5、Other APIs

#### Configure the callback frequency for the publish stream data

* The publish stream status changed can be notified by callback method OnPublishQualityUpdate
* By setting the frequency of publishing quality callback method, you can find the quality information from the OnPublishQualityUpdate.

```objective-c
// setting the callback frequenct of the publish stream data,（Must be set before logging in the room)
[LVRTCEngine setPublishQualityMonitorCycle:1];

//SDK will collect the statistical quality data of the publishing stream periodically, the app can obtian the statistical quality data by this method
// @param quality quality data

* (void)OnPublishQualityUpdate:(LVVideoStatistic *)quality;

```

#### LVVideoStatistic: statistical quality data information

* This contains the relevant data information of the publishing stream, including the frame rate, resolution, code rate, etc.

```objective-c
// the frame of video encode
@property (nonatomic, assign) int       videoEncodeFrames; 

// total amount of video packets sent
@property (nonatomic, assign) int       videoSentPackets; 

// total amount of video bytes sent
@property (nonatomic, assign) long long videosentKbytes; 

// video frame rate
@property (nonatomic, assign) int       videoFps; 

// total amount of video packets lost
@property (nonatomic, assign) int       videoLostPackets; 

// total amount of audio packets lost
@property (nonatomic, assign) int       audioLostPackets; 

// the current available send bandwidth
@property (nonatomic, assign) int       availableSendBandwidth; 

// video bitrate， bps
@property (nonatomic, assign) int       videobitratebps; 

// audio bitrate， bps
@property (nonatomic, assign) int       audiobitratebps; 

// elapsed time for video encode， ms
@property (nonatomic, assign) int       videoAvgEncodeCostMs; 

// audio packets RTT， ms
@property (nonatomic, assign) int       audioRtt; 

// video packets RTT， ms
@property (nonatomic, assign) int       videoRtt; 

// the percnect of video lost
@property (nonatomic, assign) int       videoLostPercent; 

// the percnect of audio lost
@property (nonatomic, assign) int       audioLostPercent; 

// publish：video encoded frame width ， play： received video frame width
@property (nonatomic, assign) int       frameWidth; 

// publish：video encode frame height， play： received video frame height
@property (nonatomic, assign) int       frameHeight; 
```

## Demo

* For the specific examples of publishing streams please refer to [basic SDK demo](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq).
