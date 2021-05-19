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

```objective-c
// On or off the microphone
// @param enbale true On，false Off（Default as true）
// @return true succeeded，false failed
// @discussion call this API for parameter configuration when publishing the streams.
[[LVRTCEngine sharedInstance] enableMic:true]; 

``` 

### 2、Switch between speaker and headsets

This function can control the switching between the speaker and the headsets to play the audio.

```objective-c
// the function of switching between the speaker and the headsets
// @param enable true play with the speaker，false play with the headsets（default as true）
// @return true succeeded，false failed
[[LVRTCEngine sharedInstance] enableSpeaker:true];
```

### 3、Control the volume of the remote users

The muted audio function can be used to mute the remote user's audio directly, or control the volume of the remote user by setPlayVolume function.

```objective-c
// Mute the reomote user
// @param mute whether to mute the user
// @param userId User ID
[[LVRTCEngine sharedInstance] muteAudio:false userId:@""]; 

``` 

```objc
// control the volume of the remote audio streams (called after enter the room)
// @param volume the volume（0，100）
// @param userId The User ID who is being controlled.
[[LVRTCEngine sharedInstance] setPlayVolume:50 userId:@""];
```

### 4、Obtain users' volume information

Get the information about the volume of a remote user.

```objective-c
// Obtain the volume information
// @param userId user id
// @return The corresponding Volume information 

* (int)getSoundLevelByUserId:(NSString *)userId; 

``` 

### 5、Enable volume change monitoring

#### （1）API

```objective-c
// Turn on volume change monitoring and set callback frequency
[[LVRTCEngine sharedInstance] startSoundLevelMonitor:100];

// The callback parameter of the audio data
[[LVRTCEngine sharedInstance] setAudioRecordFlag:LVAudioRecordTypeNone];
```

#### （2）The callback of the volume change monitoring

The startSoundLevelMonitor will be activated when the volume change monitoring is enabled.

``` objc
/// The notification of the current user's volume change, this callback needs to enable the volume change monitoring to activate the startSoundLevelMonitor
/// @param captureSoundLevel

* (void)OnCaptureSoundLevelUpdate:(nonnull LVAudioVolume *)captureSoundLevel;

```

#### （3）The information of LVAudioVolume user's volume

* The OnCaptureSoundLevelUpdate will tell which user's volume has changed, and the changed information of the user's volume.

`

``` objc
/// User's volume information
@interface LVAudioVolume : NSObject

/// User id
@property (nullable, nonatomic, copy)     NSString*   userId;

/// volume
@property (nonatomic, assign) int       volume;

@end
````

#### （4）Set the call back of the audio data

* You can control the type of callback data by setting the callback of the audio data, for example, only the volume data of the remote user or local captured volume data can be recalled

``` objc
/**
 the callback type of the audio data（audio data recording mode）
 */
typedef NS_ENUM(NSInteger, LVAudioRecordType) {
    /**
        no need the callback of the audio data
     */
    LVAudioRecordTypeNone         = 0,
    /**
        Only the callback of the remote user can be triggered.
     */
    LVAudioRecordTypePlayBack     = 0x01,
    /**
        Only the callback of the captured data from the microphone
     */
    LVAudioRecordTypeMicrophone   = 0x02,
    /**
        Retrieve the audio data after mixing
     */
    LVAudioRecordTypeMix          = 0x04,
};
```

### 6、Stop the volume change monitoring

Call the stopSoundLevelMonitor method to notify the volume change monitoring.

```objective-c
// Disable the volume change monitoring
[[LVRTCEngine sharedInstance] stopSoundLevelMonitor]; 
```
