# The Common Video Functions

## <a name='1'></a>1、Introduction

The Common functions include the configurations of bitrate, frame rate, resolution and the function of switching the front/rear cameras, adaptive resolution which can be adjusted according to different situations to achieve the better user experience.

## <a name='2'></a>2、Basic properties

LinkV SDK uses the  **setAVConfig** method to configure the video-related properties, including video resolution, frame rate, bit rate, and other parameters.

* bitrate
  + Set the maximum bit rate (range)
* min_bitrate
  + Set the minimum bit rate (range)
* fps
  + Set the frame rate, generally 15 fps.

#### （1）Default value

Use the default value when it is unspecified.

```java
// Use the default resolution, bit rate, frame rate (960x540 resolution 15 frames 1200000bps
）
LVAVConfig mAVConfig = new LVAVConfig();
/*

Default frame rate videoFrameRate            is：15 fps
Default maximum bit rate videoTargetBitrate     is：1200000 bps
Default minimum bit rate videoMinBitrate is：400000 bps
Default videoDegradationPreference is 0（The bit rate is adaptive, when the bandwidth is insufficient, it will only blur, without reducing the frame rate resolution）

*/
```

#### （2）Manual configuration

```java
// Use SDK built-in resolution (960x540 resolution 15 frames 1200000bps)

LVAVConfig mAVConfig = new LVAVConfig(LVAVConfig.PROFILE_540P);

// Maximum video bit rate, unit bps

mAVConfig.setVideoTargetBitrate(1200000);

// Minimum bit rate

mAVConfig.setVideoMinBitrate(mAVConfig.getVideoTargetBitrate() / 3);

// Video frame rate

mAVConfig.setVideoFrameRate(15);

// Keep the resolution unchanged, so when the network is bad, the video frame rate will be reduced, and the video resolution will remain unchanged

mAVConfig.setVideoDegradationPreference(LVAVConfig.MAINTAIN_RESOLUTION);

// Set audio and video parameters

mRtcEngine.setAVConfig(mAVConfig);
```

## <a name='3'></a>3、Adaptive Strategy

#### videoDegradationPreference adaptive degradation strategy

* After the adaptive strategy is enabled, the resolution and bitrate can be adjusted according to the use in different scenarios. The followings are the supported configurations

```java
/**
 * Video network adaptive degradation strategy

 */
public class LVAVConfig {
  
    /**
     * Keep the frame rate unchanged, automatically reduce the resolution when the network is bad, and keep the frame rate unchanged

    public static final int MAINTAIN_FRAMERATE = 1;
    
    /**
     * Keep the resolution unchanged, so when the network is bad, the video frame rate will be reduced, and the video resolution will remain unchanged

     */
    public static final int MAINTAIN_RESOLUTION = 2;
    
}
```

#### LVAVConfig （SDK Built-in supported resolution）

* Support a variety of resolution, bit rate, frame rate configuration strategy, you can pass the corresponding configuration enumeration value in new LVAVConfig(LVAVConfig.PROFILE_540P) for setting。

```java
public class LVAVConfig {

    /**
     *   320x180   15   300000
     */
    public static final int PROFILE_180P = 0;
    
    /**
     *   480x270   15   500000
     */
    public static final int PROFILE_270P = 1;
    
    /**
     *   640x360   15   800000
     */
    public static final int PROFILE_360P = 2;
    
    /**
     *   960x540   15   1200000
     */
    public static final int PROFILE_540P = 3;
    
    /**
     *   1280x720  15   1800000
     */
    public static final int PROFILE_720P = 4;
    
};
```

## <a name='4'></a>4、其它 API

### Switch camera


* By specifying front and rear cameras，Call the switch camera interface to switch the source of the push video

```java
// Switch camera LVConstants.CMRTCCameraPosition.FRONT | LVConstants.CMRTCCameraPosition.BACK
mRtcEngine.switchCamera(LVConstants.CMRTCCameraPosition.FRONT);
```

```java
/**
 *  Camera type enumeration
 */
public static enum CMRTCCameraPosition {
    /**
     *   rear camera

     */
    BACK(0),
    /**
     *   Front camera

     */
    FRONT(1),
    /**
     *   External camera

     */
    EXTERNAL(2);
};
```

### Set whether to automatically adjust the video output direction

* When the device is turned on, the video output direction will also rotate automatically. After opening, the setOutputVideoRotation method will be invalid.


```objective-c
/**
 * Set whether to allow the SDK to automatically adjust the output direction of the video according to the direction of the device

 * @param enable        Open and close (default is true)

 */
mRtcEngine.enableVideoAutoRotation(false);
```

### Manually manage the video output direction

* Set manual management of video output direction，This method needs to be called enableVideoAutoRotation first ，set the automatic rotation method off to false to take effect

```java
/**
 * Set the manual management video output direction, this method needs to call enableVideoAutoRotation first, and turn off the automatic rotation method to take effect

 * @param rotation      Video output direction, (default is LVConstants.CMVideoRotation.ROTATION_0））
 */
mRtcEngine.setOutputVideoRotation(LVConstants.CMVideoRotation.ROTATION_0);
```

## <a name='5'></a>5、Common resolution, bit rate and frame rate recommendation

* If it is a multi-person video call with microphones, it is recommended that the resolution be lower to reduce loan consumption and decoding consumption. If it is a one-to-one scene, the resolution and bit rate can be slightly higher to increase clarity. The following are recommended scenarios:

|                   One-to-one | Multiplayer with wheat |
| :------------------------------------------: | :--- ---------------------------------------: |
| Resolution 320 x 240, frame rate 15 fps, bit rate 200 Kbps | Resolution 160 x 120, frame rate 15 fps, bit rate 65 Kbps |
| Resolution 640 x 360, frame rate 15 fps, bit rate 400 Kbps | Resolution 320 x 180, frame rate 15 fps, bit rate 140 Kbps |