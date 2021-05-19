# The Accompaniment Mixing

## <a name='1'></a>1、Introduction

The SDK supports the accompaniment mixing functions, such as adding sound effects or playing background music. The audio data and the microphone captured data can be mixed at the same time and send it after.

## <a name='2'></a>2、Description

After the accompaniment mixing is enabled, the side of pull stream will be able to play the audio-video data from the remote camera and the mixed accompaniment audio data simultaneously.


## <a name='3'></a>3、Procedures

### Enable the accompaniment mixing

After making sure to log in to the room and start pushing the streams, then specified a MP3 path and call the startAudioMixing method to start the mixing.

``` objc
// The MP3 path
NSString *audioPath = [[NSBundle mainBundle] pathForResource:@"audio" ofType:@"mp3"];
             
// Start playing music files and mixing（audio accompaniment）
// @param filePath
// @param replace true: Push the local audio file without the recorded audio by the microphone  false：mix the contents of local audio file and the captured audio streams by microphone
// @param loop Specify the number of times the audio file loops，positive integers：the number of times to loop -1：infinite loop
// @return 0 ： the callback succeeded，!0：failed
[[LVRTCEngine sharedInstance] startAudioMixing:audioPath replace:NO loop:-1];
```

### Pause/resume the mixing

``` objc
/// Pause the music files and the mixing. Please call this method in the room.
/// @return 0：succeeded !0：failed
-(int)pauseAudioMixing;
```

### Stop the mixing

``` objc
// stop the music files and the mixing. Please call this method in the room.
// @return 0：succeeded !0：failed
[[LVRTCEngine sharedInstance] stopAudioMixing];
```

## <a name='4'></a>4、API

###  Get the accompaniment volume information

``` objc
// obtain the current volume of the accompaniment, please call after the accompaniment started.
// @return -1：have not started 0～100：The current volume
[[LVRTCEngine sharedInstance] getAudioMixingVolume];
```

### Adjust the playback volume of accompaniment music

``` objc
// adjust the volume of the music file, please call this method in the room
// @param volume volume：0～100
// @return 0：succeeded !0：failed
[[LVRTCEngine sharedInstance] adjustAudioMixingVolume:20];
```

### Set up the playback location of the music files

``` objc
/// Set up the location of the music files. please call this method in the room
/// @param pos integers.process bar positjion, unit: ms
/// @return 0：succeeded !0：failed
[[LVRTCEngine sharedInstance] setAudioMixingPosition:200];
```

### Obtain the total duration/length of the current accompaniment file

``` objc
// obtain the total duration/length，unit:ms please call this method in the room
// @return the file's length
[[LVRTCEngine sharedInstance] getAudioMixingTotalLength];
```

### Obtain the current music playback progress

``` objc
/// Obtain the current music playback progress. unit:ms please call this method in the room
/// @return <0：failed >=0：Succeeded and return to the playback progress of the accompaniment.
[[LVRTCEngine sharedInstance] getAudioMixingCurrentPosition];
```

## <a name='5'></a>5、Demo

For the specific reference, please open the [foundation SDK demo](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq) as an example project.

