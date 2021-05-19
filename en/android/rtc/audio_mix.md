# The Accompaniment Mixing

## <a name='1'></a>1、Introduction

The SDK supports the accompaniment mixing functions, such as adding sound effects or playing background music. The audio data and the microphone captured data can be mixed at the same time and send it after.

## <a name='2'></a>2、Description

After the accompaniment mixing is enabled, the side of pull stream will be able to play the audio-video data from the remote camera and the mixed accompaniment audio data simultaneously.

<img src="https://dl.linkv.io/doc/en/android/rtc/images/diy_audio_extra.png" width="iOS_Auth2" style="width:60%;" />

## <a name='3'></a>3、Procedures

### Enable the accompaniment mixing

After making sure to log in to the room and start pushing the streams, then specified a MP3 path and call the startAudioMixing method to start the mixing.

```java
/**
* Start playing music files and mixing (sound accompaniment)
 * @param filePath      String type，file path
 * @param replace       Boolean type，true: Only push the set local audio files, do not transmit the audio recorded by the microphone  false：The content of the audio file will be mixed with the audio stream collected by the microphone
 * @param loop      int type，Specify the number of times to loop the audio file，Positive integer：Number of cycles -1：Infinite loop
 * @return      int type，0 ： Method call succeeded，!0：Failed

 */
mRtcEngine.startAudioMixing("/assets/audio.mp3", false, -1);
```

### Pause/resume the mixing

```objc
/**
 * Pause playing music files and mixing. Please call this method in the room.

 * @return 0：Method call succeeded !0：Method call failed
 */
mRtcEngine.pauseAudioMixing();
```

### Stop the mixing

```java
/**
 * Stop playing music files and mixing. Please call this method in the room.
 * @return      int type，0：Method call succeeded !0：Method call failed

 */
mRtcEngine.stopAudioMixing();
```

## <a name='4'></a>4、API

###  Get the accompaniment volume information

```java
/**
 * Get the current accompaniment volume, please call it after the accompaniment starts.
 * @return      int type，-1：Accompaniment did not start 0～100：Current accompaniment volume
 */
mRtcEngine.getAudioMixingVolume();
```

### Adjust the playback volume of accompaniment music

```java
/**
 * Adjust the playback volume of music files。Call this method inside the room。
 * @param volume        int type，volume：0～100
 * @return      int type，0：Method call succeed !0：Method call failed
 */
mRtcEngine.adjustAudioMixingVolume(100);
```

### Set up the playback location of the music files

```java
/**
 * Set the playback position of music files。Call this method inside the room。
 * @param pos       int type，Progress bar position，The unit is milliseconds
 * @return      int type，0：Method call succeeded !0：Method call failed
 */
mRtcEngine.setAudioMixingPosition(200);
```

### Obtain the total duration/length of the current accompaniment file

```java
/**
 *  Get the total duration of the current accompaniment file in milliseconds. Please call this method in the room.
 *  @return      long type，Total file length
 */
mRtcEngine.getAudioMixingTotalLength();
```

### Obtain the current music playback progress

```java
/**
 *  Get the playback progress of music files。The unit is milliseconds。Call this method inside the room。
 *  @return      long type，<0：Method call failed >=0：The method is successfully called and returns to the accompaniment playback progress
 */
mRtcEngine.getAudioMixingCurrentPosition();
```

## <a name='5'></a>5、Demo

For the specific reference, please open the [foundation SDK demo](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq) as an example project.

