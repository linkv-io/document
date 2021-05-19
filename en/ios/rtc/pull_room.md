# Playing Streams

## <a name='1'></a>1、Introduction

In the scenarios such as group calls and interactive live broadcasting, to be able to watch the video and hear the audio from the push streams  , you need to perform the pull stream operation to achieve the video and hear the sound from them.

## <a name='3'></a>3、Procedures

### 3.1 Join the room and play the steams

If there was a broadcasting room, all of the streams of the room would be played automatically. The method is shown as follows , refer to the [LoginRoom](/?p=/zh/ios/rtc/login_room.md&k=lD5BR0Hz) Introduction.

``` objc
// Entered the room（audio and video conference）
// @param userId UID
// @param roomId RoomID
// @param isHost Is it the host
// @param isOnlyAudio IS it joined with audio mode only(the video streaming will not be activated)
// @param delegate Room callback delegate

* (void)loginRoom:(NSString *)userId

           roomId:(NSString *)roomId
           isHost:(bool)isHost
      isOnlyAudio:(bool)isOnlyAudio
         delegate:(id<LVRTCEngineDelegate>)delegate;
```

### 3.2 Handle the LoginRoom callback: OnEnterRoomComplete

When **loginRoom** is called to login to the room, the OnEnterRoomComplete will be triggered with a **users** array. And it contains all users' data in the room.

``` objc
// The callback when entered the room sucessfully 
// @param code The erro codes of whether it is sucessful to login to the room
// @param users the list of the users who in the room will be activated when there is an exiting user in the room

* (void)OnEnterRoomComplete:(LVErrorCode)code users:(nullable NSArray<LVUser*>*)users

```

### 3.3 Start to play the streams

Start to play the stream of the specified user by StartPlayingStream.

```objective-c
// start to play a video stream
// @param userId the UID who playing the pulled streams
[[LVRTCEngine sharedInstance] startPlayingStream:user.userId]; 

``` 

### 3.4 Stop playing the streams

Stop playing the stream of the specified user by stopPlayingStream.

```objective-c
// Stop playing a Video stream
// @param userId the UID who stops the steams
[[LVRTCEngine sharedInstance] stopPlayingStream:uid];
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

* The play stream status change can be notified by callback method OnPlayQualityUpate
* By setting the frequency of publishing quality callback method, you can find the quality information from the OnPlayQualityUpate.

```objective-c
// setting the callback frequenct of the play stream data, （Must be set before logging in the room)
[LVRTCEngine setPlayQualityMonitorCycle:1]; 

// SDK will collect the statistical quality data of the play stream periodically, the app can obtian the statistical quality data by this method
// @param quality quality data
// @param userId User ID

* (void)OnPlayQualityUpate:(LVVideoStatistic *)quality userId:(NSString*)userId; 

``` 

#### LVVideoStatistic data information callback

* This contains the relevant data information of the play stream, including the frame rate, resolution, code rate, etc.

```objective-c
// the frame of video encode
@property (nonatomic, assign) int       videoEncodeFrames;

// total amount of videoSentPackets
@property (nonatomic, assign) int       videoSentPackets;

// total amount of videosentKbytes
@property (nonatomic, assign) long long videosentKbytes;

// video frame rate
@property (nonatomic, assign) int       videoFps;

// total amount of video packets lost
@property (nonatomic, assign) int       videoLostPackets;

//total amount of audio packets lost
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

* For the specific examples of playing streams please refer to [basic SDK demo](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq).
