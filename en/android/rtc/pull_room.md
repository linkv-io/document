# Playing Streams

## <a name='1'></a>1、Introduction

In the scenarios such as group calls and interactive live broadcasting, to be able to watch the video and hear the audio from the push streams  , you need to perform the pull stream operation to achieve the video and hear the sound from them.

## <a name='2'></a>2、Process

![](https://dl.linkv.io/doc/en/android/rtc/images/video_pull.png)

## <a name='3'></a>3、Procedures

### 3.1 Join the room and play the steams

If there was a broadcasting room, all of the streams of the room would be played automatically. The method is shown as follows , refer to the [LoginRoom](/?p=/en/android/rtc/login_room.md&k=lD5BR0Hz)

```java
/**
 * Join the audio and video room (audio and video conference）
 * @param roomId    room Id
 * @param userId    user Id
 * @param isHost    is it host
 * @param isOnlyAudio    Whether to join in audio mode, join in audio mode, there is no video stream

 * @param callback    Add room result callback

 */
mRtcEngine.loginRoom(roomId, userId, isHost, isOnlyAudio, (code, cmUsers) -> {
    if (code == LVErrorCode.SUCCESS) {
        // Login successfully
    } else {
        // Login failed
    }
});
```

### 3.2 Handle the LoginRoom callback: OnEnterRoomComplete

When **loginRoom** is called to login to the room, the OnEnterRoomComplete will be triggered with a **users** array. And it contains all users' data in the room.

```java
/**
 * Callback for success in joining the room
 * @param code      joined room successfully error code
 * @param users     User list, if there are users in the room, the list will take effect automatically
 */
public interface LVResultCallback2<Integer, ArrayList<LVUser>>{
    void onResult(Integer code, ArrayList<LVUser>> users)
}
```

### 3.3 Start to play the streams

Start to play the stream of the specified user by StartPlayingStream.

```java
/**
 * Start playing an audio and video stream, and the change of the playback state is called back through onPlayStateUpdate

 * @param userId        Audio and video stream users to be played ID
 */
mRtcEngine.startPlayingStream(userId);
```

### 3.4 Stop playing the streams

Stop playing the stream of the specified user by stopPlayingStream.

```java
/**
 * Stop playing an audio and video stream
 * @param uid       The audio and video stream user who wants to stop playing ID
 */
mRtcEngine.stopPlayingStream(uid);
```

## <a name='4'></a>4、Steps in the business scenario

### The steps of playing stream can be referred to as follows:

* **Host**

  1. startCapture: enable the camera capture

  2. addDisplayView: add the binding for rendering the displayview of the push streams

  3. loginRoom: log in to the room and process it in OnEnterRoomComplete.

  4. **startPublishing:** start streaming

* **Audience - enter the live room and play streams**

  1. loginRoom: log in to the room, and play all the streams of the room in OnEnterRoomComplete.

  2. addDisplayView: add the binding for rendering the displayview of publish streams and specify the displayview uid.

  3. **startPlayingStream:** play the streams of the room.

## <a name='5'></a>5、Other APIs

#### Configure the callback frequency for the play stream data

* The change of the streaming state is called back through the onPlayStateUpdate method.
* By setting the pull-back information callback frequency, you can get the relevant quality information in onPlayStateUpdate.
```java
// Set the frequency at which data statistics are returned when streaming (must be set before logging in to the room)
mRtcEngine.setPlayQualityMonitorCycle(1);

/**
 * For notifications of changes in playback quality, the SDK will regularly count the quality information of the streaming. APP can implement this method to obtain the statistics of the video quality information of the streaming. The frequency of returning can be set through setPlayQualityMonitorCycle

 * @param stats        Quality information
 * @param userId        User ID
 */
void onPlayQualityUpdate(final LVVideoStatistic stats, final String userId);
```

#### LVVideoStatistic Data information callback class

* This category contains the relevant data information of the pull stream, including the current frame rate, resolution, bit rate and so on.


```java
// Number of video encoding frames
public int videoEncodeFrames

// Total number of video packets sent
public int videoSentPackets

// Total number of bytes sent in video
public long videoSentKBytes

// Video input frame rate (video frame rate)）
public int videoFps

// Total number of video packet loss
public int videoLostPackets

// Total number of audio packets lost
public int audioLostPackets

// Currently available sending bandwidth
public int availableSendBandwidth

// Video bitrate
public int videoBitrateBps

// Audio bitrate
public int audioBitrateBps

//Video encoding time (in millimeters), only valid for the video sender
public int videoAvgEncodeCostMs

// Audio package RTT, unit ms
public int audioRtt

// Video package RTT, unit ms
public int videoRtt

// Cumulative video packet loss percentage
public int videoLostPercent

// Cumulative audio packet loss percentage
public int audioLostPercent

// Push stream: encode video width, pull stream: input video frame width
public int frameWidth

//  Push stream: encoded video high, pull stream: input video frame height
public int frameHeight
```

## Demo

* For the specific examples of playing streams please refer to [basic SDK demo](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq)

