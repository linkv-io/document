# Common Audio Functions

## <a name='1'></a>1、Introduction

The common audio functions include the on-off control for the microphone, switching the speaker and handset, controlling the remote users to mute, monitoring the volume change, and other common functions.

## <a name='2'></a>2、Common functions

* On-off control for the microphone
* Speaker and handset switching
* Controlling the volume of the remote users
* Obtaining users' volume information
* Enabling the volume change monitoring

### 1、On-off control for the microphone

This function can disable or enable the microphone function.

```java
/**
 *  Turn the microphone on or off
 *  @param enbale       true open，false close（Default is true）
 */
mRtcEngine.enableMic(enable);
```

### 2、Switch between speaker and headsets

This function can control the switching between the speaker and the headsets to play the audio.

```java
/**
 *  Speaker and receiver switching function
 *  @param enable       true play audio as if on the speaker，false Use the receiver to play audio。（Default true）
 */
mRtcEngine.enableSpeakerphone(false);
```

### 3、Control the volume of the remote users

The muted audio function can be used to mute the remote user's audio directly, or control the volume of the remote user by setPlayVolume function.

```java
/**
 *  Set the remote user volume，Call after successfully joining the room
 *  @param userId       String type，The controlled user ID
 *  @param volume       int type，volume size，range 0 to 100
 */
mRtcEngine.setPlayVolume(userId, 100);
```

### 4、Obtain users' volume information

Get the information about the volume of a remote user.

```java
/**
 *  Gets the user's volume size
 *  @param userId       String type，Controlled user id

 *  return       int type，volume size，range 0 to 100
 */
mRtcEngine.getSoundLevelByUserId(userId);
```

### 5、Enable volume change monitoring

#### （1）API

```java
/**
 *  Turn on volume monitoring callback，You will receive LVRTCCallback after opening.onAudioVolumeUpdate(ArrayList)
 *  @param timeInMs       int type，Callback interval，In milliseconds
 */
mRtcEngine.startSoundLevelMonitor(100);

/**
 *  Set audio recording mode，Multiple recording modes can be set at the same time，The recording result will be called back through LVRTCCallback.onAudioMixStream()
 *  @param types      AudioRecordType enumeration type，Audio recording mode
 */
mRtcEngine.setAudioRecordFlag(LVConstants.AudioRecordType.NONE);
```

#### （2）The callback of the volume change monitoring

Turn on the volume change monitoring method to take effect. startSoundLevelMonitor executes
```java
/**
 *  Notification of current user volume change，This callback needs to call the open volume change monitoring method to take effect startSoundLevelMonitor
 *  @param volumes      Volume level information
 */
void onAudioVolumeUpdate(ArrayList<LVAudioVolume> volumes);
```

#### （3）The information of LVAudioVolume user's volume

* onAudioVolumeUpdate The callback will tell which user's volume has changed，and changed volume information


````java
/// User volume information
public class LVAudioVolume {

    /// User ID
    public String userId;
    
    /// Volume
    public int volume;

}
````

#### （4）Set the call back of the audio data

* You can control the type of callback data by setting the callback of the audio data, for example, only the volume data of the remote user or local captured volume data can be recalled

```java
/**
Audio data callback type (sound data recording mode)
 */
public static enum AudioRecordType {
    /**
     * No need to drop back audio data

     */
    NONE(0),
    
    /**
     * Return only remote user data
     */
    PLAYBACK(1),
    
    /**
* Only return the data collected by the local mic
     */
    MICPHONE(2),
    
    /**
     * Return the audio data after mixing
     */
    MIX(4);
}
```

### 6、Stop the volume change monitoring

Call the stopSoundLevelMonitor method to notify the volume change monitoring.

```java
/**
 * Stop volume monitoring callback
 */
mRtcEngine.stopSoundLevelMonitor();
```

