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

``` objc
// default resolution, bitrate and framerate （640x480 500000bps 15fps）
LVAVConfig *config = [[LVAVConfig alloc] init];
/*

Default framerate fps            为：15 fps
The default maximum bitrate     为：500000 bps
The default minimum bitrate 为：500000 bps
The defaut value of videoDegradationPreference as 0（The bitrate is adaptive，Insufficient network cuases the blur but the framerate and resolution will not be affected.

*/
```

#### （2）Manual configuration

```objective-c
// Use the preset profile of SDK（ 640x480 500000bps 15fps）
LVAVConfig *config = [[LVAVConfig alloc] initWithVideoProfile: LVRTCVideoProfile_480P]; 

// The maximum Video bitrate， unit: bps
config.bitrate = 500000; 

// The minimum Bitrate
config.min_bitrate = config.bitrate / 3.0; 

// Video Framerate
config.fps = 15; 

// The resolution will not be affected by the insufficient network.
config.videoDegradationPreference = LVVideoDegradationPreference_MAINTAIN_RESOLUTION; 

// Activate the Configuration
[[LVRTCEngine sharedInstance] setAVConfig:config]; 

``` 

## <a name='3'></a>3、Adaptive Strategy

#### videoDegradationPreference adaptive degradation strategy

* After the adaptive strategy is enabled, the resolution and bitrate can be adjusted according to the use in different scenarios. The followings are the supported configurations

```objc
/**
 Adaptive Video degaration strategy by insufficient network
 */
typedef enum : NSUInteger {
    /**
        The bitrate is adaptive，Insufficient network causes the blur but the framerate and resolution will not be affected.
    */
    LVVideoDegradationPreference_DISABLED = 0,
    /**
        Degrade the resolution automatically to keep the stability of the framerate under the terrible network condition
     */
    LVVideoDegradationPreference_MAINTAIN_FRAMERATE = 1,
    
    /**
        Drop down the framerate automatically to keep the current resolution under the terrible network condition
     */
    LVVideoDegradationPreference_MAINTAIN_RESOLUTION = 2,
    
    /**
        Degrading the resolution and the framerates according to the current network condition （beta function，please do not use）
     */
    LVVideoDegradationPreference_BALANCE = 3
    
} LVVideoDegradationPreference;
```

#### LVRTCVideoProfile (The preset profiles by SDK)

* Support various configuration strategies of the resolution, bitrate and framerate, which can be set by passing the corresponding configuration of the enumeration value in  [[LVAVConfig alloc] initWithVideoProfile: LVRTCVideoProfile_480P].

```objective-c
typedef NS_ENUM(NSInteger, LVRTCVideoProfile) {

    /**
        Invalid video parameter
     */
    LVRTCVideoProfile_Invalid = -1,
    /**
        160x128   15   65
     */
    LVRTCVideoProfile_120P = 0,
    /**
        120x120   15   50
     */
    LVRTCVideoProfile_120P_3 = 2,
    /**
        320x180   15   140
     */
    LVRTCVideoProfile_180P = 10,
    /**
        180x180   15   100
     */
    LVRTCVideoProfile_180P_3 = 12,
    /**
        240x180   15   120
     */
    LVRTCVideoProfile_180P_4 = 13,
    /**
        320x240   15   200
     */
    LVRTCVideoProfile_240P = 20,
    /**
        240x240   15   140
     */
    LVRTCVideoProfile_240P_3 = 22,
    /**
        424x240   15   220
     */
    LVRTCVideoProfile_240P_4 = 23,
    /**
        640x360   15   400
     */
    LVRTCVideoProfile_360P = 30,
    /**
        640x368   15   420
     */
    LVRTCVideoProfile_368P = 31,
    /**
        360x360   15   260
     */
    LVRTCVideoProfile_360P_3 = 32,
    /**
        640x360   30   600
     */
    LVRTCVideoProfile_360P_4 = 33,
    /**
        360x360   30   400
     */
    LVRTCVideoProfile_360P_6 = 35,
    /**
        480x360   15   320
     */
    LVRTCVideoProfile_360P_7 = 36,
    /**
        480x360   30   490
     */
    LVRTCVideoProfile_360P_8 = 37,
    /**
        640x360   15   800
     */
    LVRTCVideoProfile_360P_9 = 38,
    /**
        640x360   24   800
     */
    LVRTCVideoProfile_360P_10 = 39,
    /**
        640x360   24   1000
     */
    LVRTCVideoProfile_360P_11 = 100,
    /**
        640x480   15   500
     */
    LVRTCVideoProfile_480P = 40,
    /**
        480x480   15   400
     */
    LVRTCVideoProfile_480P_3 = 42,
    /**
        640x480   30   750
     */
    LVRTCVideoProfile_480P_4 = 43,
    /**
        480x480   30   600
     */
    LVRTCVideoProfile_480P_6 = 45,
    /**
        848x480   15   610
     */
    LVRTCVideoProfile_480P_8 = 47,
    /**
        848x480   30   930
     */
    LVRTCVideoProfile_480P_9 = 48,
    /**
        640x480   10   400
     */
    LVRTCVideoProfile_480P_10 = 49,
    /**
        960x540    15   900
     */
    LVRTCVideoProfile_540P = 50,
    /**
        960x540    30   1000
     */
    LVRTCVideoProfile_540P_1 = 51,
    /**
        1280x720  15   1130
     */
    LVRTCVideoProfile_720P = 60,
    /**
        1280x720  30   1710
     */
    LVRTCVideoProfile_720P_3 = 62,
    /**
        960x720   15   910
     */
    LVRTCVideoProfile_720P_5 = 64,
    /**
        960x720   30   1380
     */
    LVRTCVideoProfile_720P_6 = 65,
    /**
        1920x1080 15   2080
     */
    LVRTCVideoProfile_1080P = 70,
    /**
        1920x1080 30   3150
     */
    LVRTCVideoProfile_1080P_3 = 72,
    /**
        1920x1080 60   4780
     */
    LVRTCVideoProfile_1080P_5 = 74,
    /**
        2560x1440 30   4850
     */
    LVRTCVideoProfile_1440P = 76,
    /**
        2560x1440 60   7350
     */
    LVRTCVideoProfile_1440P_2 = 77,
    /**
        3840x2160 30   8190
     */
    LVRTCVideoProfile_4K = 80,
    /**
        3840x2160 60   13500
     */
    LVRTCVideoProfile_4K_3 = 82,
    /**
        LVRTCVideoProfile_360P
     */
    LVRTCVideoProfile_DEFAULT

}; 

``` 

## <a name='4'></a>4、Other APIs

### Switching the camera

* By specifying the front and rear cameras, calling the interface of switching camera can switch the source of the video publishing streams.

```objective-c
// switch the cameras LVRTCCameraPositionBack | LVRTCCameraPositionFront
[[LVRTCEngine sharedInstance] switchCamera:LVRTCCameraPositionFront];
```

```objective-c
/**
 Enumeration of the front and rear cameras
 */
typedef NS_OPTIONS(NSUInteger, LVRTCCameraPosition) {

    /**
        the front camera
     */
    LVRTCCameraPositionFront,
    /**
        The rear camera
     */
    LVRTCCameraPositionBack,

}; 

``` 

### Video output rotation automatically

* When this flag is turned on, the video output rotation will be changed when the device rotates. The setOutputVideoRotation method will be invalid after enabling.

```objective-c
// Whether to allow the SDK to adjust the output rotation of the video according to the rotation of the device
// @param enable Yes or false（default as YES）
[[LVRTCEngine sharedInstance] enableVideoAutoRotation:false];
```

### Manually manage the video output rotation

* To set the manual management video output rotation. It needs to set enableVideoAutoRotation as false first.

```objective-c
// @param rotation Video rotation，（default as LVVideoRotation_0）
[[LVRTCEngine sharedInstance] setOutputVideoRotation: LVVideoRotation_0]; 
```

## 5、Recommended Resolution, Bitrate and Framerate

* If it is group chat conference scenario, it is recommended to lower the resolution to reduce the load consumption and decoding consumption. In a one-to-one scenario, the resolution and bit rate can be slightly higher to increase the definition. The followings are recommended setting for different scenarios:

|                    One To One chat                    |                   Group chat                   |
| :------------------------------------------: | :------------------------------------------: |
| Resolution 320 x 240, frame rate 15 fps, bitrate 200 Kbps | Resolution 160 x 120, frame rate 15 fps, bitrate 65 Kbps  |
| Resolution 640 x 360, frame rate 15 fps, bitrate 400 Kbps | Resolution 320 x 180, frame rate 15 fps, bitrate 140 Kbps |
