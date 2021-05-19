# 视频常用功能

## <a name='1'></a>1、功能简介

使用常用功能，包含 码率，帧率，分辨率的设置 和 切换前后置摄像头，自适应分辨率的功能，可以根据不同情况进行调整，以达到较好的用户体验。

## <a name='2'></a>2、基础属性设置

LinkV SDK 通过  **setAVConfig** 方法来设置视频相关的属性，其中包含视频分辨率、帧率、码率、等参数。

* bitrate
  * 设置最大码率（范围）
* min_bitrate
  * 设置最小码率（范围）
* fps
  * 设置帧率，一般为 15 帧。

#### （1）使用默认值

默认不指定会使用默认值

```objc
// 使用 默认 分辨率，码率，帧率 （ 640x480 分辨率  15帧   500000bps）
LVAVConfig *config = [[LVAVConfig alloc] init];
/*

默认帧率 fps            为：15 fps
默认最大码率 bitrate     为：500000 bps
默认最小码率 min_bitrate 为：500000 bps
默认 videoDegradationPreference 为0（码率自适应，带宽不足时，只会模糊，不降帧率分辨率）

*/
```

#### （2）手动配置

```objective-c
// 使用 SDK 内置的分辨率 （ 640x480 分辨率  15帧   500000bps）
LVAVConfig *config = [[LVAVConfig alloc] initWithVideoProfile:LVRTCVideoProfile_480P];

// 视频最大码率， 单位 bps
config.bitrate = 500000;

// 最小码率
config.min_bitrate = config.bitrate / 3.0;

// 视频帧率
config.fps = 15;

// 维持分辨率不变，也就网络糟糕的时候会降低视频帧率，保持视频分辨率不变
config.videoDegradationPreference = LVVideoDegradationPreference_MAINTAIN_RESOLUTION;

// 让配置生效
[[LVRTCEngine sharedInstance] setAVConfig:config];
```

## <a name='3'></a>3、相关内置策略配置

#### videoDegradationPreference 自适应降级策略

* 开启自适应策略后，可根据不同的场景字使用调整分辨率，码率等。以下是支持的配置

```objc
/**
 视频网络自适应降级策略
 */
typedef enum : NSUInteger {
    /**
        码率自适应，带宽不足时，只会模糊，不降帧率分辨率
    */
    LVVideoDegradationPreference_DISABLED = 0,
    /**
        维持帧率不变，网络糟糕时自动降低分辨率，保持帧率不变
     */
    LVVideoDegradationPreference_MAINTAIN_FRAMERATE = 1,
    
    /**
        维持分辨率不变，也就网络糟糕的时候会降低视频帧率，保持视频分辨率不变
     */
    LVVideoDegradationPreference_MAINTAIN_RESOLUTION = 2,
    
    /**
        根据网络状态自动降低分辨率和帧率（测试功能，请勿使用）
     */
    LVVideoDegradationPreference_BALANCE = 3
    
} LVVideoDegradationPreference;
```

#### LVRTCVideoProfile （SDK 内置支持的分辨率）

* 支持多种分辨率，码率，帧率配置策略，可在  [[LVAVConfig alloc] initWithVideoProfile:LVRTCVideoProfile_480P]; 中传递对应的配置枚举值进行设置。

```objective-c
typedef NS_ENUM(NSInteger, LVRTCVideoProfile) {
    /**
        无效视频参数
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

## <a name='4'></a>4、其它 API

### 切换摄像头

* 通过指定前后摄像头，调用切换摄像头接口可以切换推流视频的来源

```objective-c
// 切换摄像头 LVRTCCameraPositionBack | LVRTCCameraPositionFront
[[LVRTCEngine sharedInstance] switchCamera:LVRTCCameraPositionFront];
```

```objective-c
/**
 前后摄像头枚举
 */
typedef NS_OPTIONS(NSUInteger, LVRTCCameraPosition) {
    /**
        前置摄像头
     */
    LVRTCCameraPositionFront,
    /**
        后置摄像头
     */
    LVRTCCameraPositionBack,
};
```

### 设置是否自动调整视频输出方向

* 开启后，设备旋转那么视频输出方向也会自动旋转。开启后，setOutputVideoRotation 方法则会无效。

```objective-c
// 设置是否允许 SDK 自动根据设备的方向调整视频的输出方向
// @param enable 打开和关闭（默认是 YES）
[[LVRTCEngine sharedInstance] enableVideoAutoRotation:false];
```

### 手动管理视频输出方向

* 设置手动管理视频输出方向，该方法需要先调用 enableVideoAutoRotation，将自动旋转方法关闭设置为 false 才能生效

```objective-c
// @param rotation 视频输出方向，（默认是 LVVideoRotation_0）
[[LVRTCEngine sharedInstance] setOutputVideoRotation:LVVideoRotation_0];
```

## 5、常用分辨率、码率和帧率推荐

* 如果是多人连麦视频通话场景，建议分辨率可以低一些， 以减少贷款消耗和解码消耗。如果是一对一的场景下，分辨率和码率可以稍微高一些，增加清晰度。以下是推荐场景使用：

|                    一对一                    |                   多人连麦                   |
| :------------------------------------------: | :------------------------------------------: |
| 分辨率 320 x 240、帧率 15 fps、码率 200 Kbps | 分辨率 160 x 120、帧率 15 fps、码率 65 Kbps  |
| 分辨率 640 x 360、帧率 15 fps、码率 400 Kbps | 分辨率 320 x 180、帧率 15 fps、码率 140 Kbps |