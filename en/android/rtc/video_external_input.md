#  Custom Video Capture

## <a name='1'></a>1、Introduction

Custom video capture means the developer captures the video source themself and provides the video source to the LinkV SDK, then LinkV SDK will encode the data and publish the streams.

When the user uses custom video capture, the displayView of the local camera capture will be invalid.

## <a name='2'></a>2、Description

#### Capturing the local camera data

* Capturing local camera data, and the side of pull streams will be able to see the data from the camera capture.

<img src="https://dl.linkv.io/doc/en/android/rtc/images/diy_video_extra.png" alt="iOS_Auth2" style="width:50%;" />

#### Custom video capture

* Custom video capture, the side of pull stream will be able to the push stream data of the local video data that been set by the side of push stream.

<img src="https://dl.linkv.io/doc/en/android/rtc/images/diy_video_extra2.png" width="iOS_Auth2" style="width:50%;" />

## <a name='3'></a>3、Steps

（1）Turn on the external video capture function

（2）Log in to the room and push the streams

（3）Decode external video

（4）Call to send the external video data

## <a name='4'></a>4、API

### 4.1 Turn on and off external video capture

When the external input is turned on, the displayview of the local camera will be invalid, The developers need to implement the displayview function of the external input video.

```java
/** 
 * Externally collected video data，Currently only supports I420 format
 * @param data      ByteBuffer type，I420 format byte array。
 * @param width      int type，Acquisition data width。
 * @param height      int type，High data collection。
 * @param rotate      int type，Collect data direction information。
 * @param format       int type，for the format, please refer to LVConstants.VideoFrameType, currently only I420 format is supported。
 * @param timestamp      long type，The frame timestamp of the frame, in milliseconds。
 * @param sei      String type，extended information。
 */
mRtcEngine.sendVideoFrame(data, width, height, rotate, format, timestamp, sei);
```

