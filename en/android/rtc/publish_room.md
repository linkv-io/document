# Publishing Streams

## <a name='1'></a>1、Introduction

In the scenarios such as group calls and interactive live broadcasting, to make other people be able to see their own pictures and hear their own voices, they need to publish their own audio and video to the cloud server. Then the peer receives the audio and video streams from the cloud to acquire the video and voices.

## <a name='2'></a>2、Process

![](https://dl.linkv.io/doc/en/android/rtc/images/video_publish.png)

## <a name='3'></a>3、Procedures

### The publishing stream API

* You will be able to publish the streams once you have logged into the room. **You have to enable camera capture before publishing the audio and video streams**.

* If the isOnlyAudio parameter is YES, then only the audio data will be sent. Which means the peer can only receive the audio data.

```java
// Publish audio and video data (push stream)
mRtcEngine.startPublishing();

// Stop publishing audio and video data

mRtcEngine.stopPublishing();
```

### Callback method for publishing stream

* After calling **startPublishing** to publish the streams, the SDK will trigger the callback to notify whether it is successful or return the corresponding error code.

* Error codes may refer to  [the callback erro codes for the status change of push streams](/?p=/en/android/rtc/ecode.md&k=WZsw8kGY)

```java
/**
 * The notification of the push stream status change. After calling startPublishing, the method will be triggered to return, and the publishing resource status change will be notified through this method

 * @param state         status code
 */
void onPublishStateUpdate(final int state);
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

* The push state change is called back through the OnPublishStateUpdate method.
* By setting the push-stream information callback frequency, you can get relevant quality information in OnPublishQualityUpdate。

```java
// Set the frequency at which statistics are returned during a stream push（Must be set before logging in to the room）
mRtcEngine.setPublishQualityMonitorCycle(1);

/**
Notification of the quality status change of the push stream, the SDK will regularly count the quality information of the push stream, the APP can implement this method to obtain the video quality information statistics of the push stream, and the frequency of return can be set through setPublishQualityMonitorCycle
 * @param quality       Quality information

 */
void onPublishQualityUpdate(LVVideoStatistic stats);
```

#### LVVideoStatistic Data information callback class


* This category contains the relevant data information of the push stream, including the current frame rate, resolution, bit rate and so on.

```java
// Number of video encoding frames

public int videoEncodeFrames;

// Total number of video packets sent

public int videoSentPackets;

// Total video bytes sent

public long videoSentKBytes;

//Video input frame rate (video frame rate）
public int videoFps;

// Total video loss
public int videoLostPackets;

// Total number of audio packets lost
public int audioLostPackets;

// Currently available sending bandwidth
public int availableSendBandwidth;

// Video bitrate
public int videoBitrateBps;

// Audio bit rate
public int audioBitrateBps;

// Video encoding time (in millimeters), only valid for the video sender
public int videoAvgEncodeCostMs;

// Audio package RTT, unit ms
public int audioRtt;

// Video package RTT, unit ms
public int videoRtt;

// Cumulative video packet loss percentage
public int videoLostPercent;

// Cumulative audio packet loss percentage
public int audioLostPercent;

//Push stream: encode video width, pull stream: input video frame width
public int frameWidth;

// Push stream: encoded video high, pull stream: input video frame height
public int frameHeight;
```

## Demo

* For the specific examples of publishing streams please refer to [basic SDK demo](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq)

