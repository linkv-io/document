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

```java
// 使用 默认 分辨率，码率，帧率 （ 960x540 分辨率  15帧   1200000bps）
LVAVConfig mAVConfig = new LVAVConfig();
/*

默认帧率 videoFrameRate            为：15 fps
默认最大码率 videoTargetBitrate     为：1200000 bps
默认最小码率 videoMinBitrate 为：400000 bps
默认 videoDegradationPreference 为0（码率自适应，带宽不足时，只会模糊，不降帧率分辨率）

*/
```

#### （2）手动配置

```java
// 使用 SDK 内置的分辨率 （ 960x540 分辨率  15帧   1200000bps）
LVAVConfig mAVConfig = new LVAVConfig(LVAVConfig.PROFILE_540P);

// 视频最大码率， 单位 bps
mAVConfig.setVideoTargetBitrate(1200000);

// 最小码率
mAVConfig.setVideoMinBitrate(mAVConfig.getVideoTargetBitrate() / 3);

// 视频帧率
mAVConfig.setVideoFrameRate(15);

// 维持分辨率不变，也就网络糟糕的时候会降低视频帧率，保持视频分辨率不变
mAVConfig.setVideoDegradationPreference(LVAVConfig.MAINTAIN_RESOLUTION);

// 设置音视频参数
mRtcEngine.setAVConfig(mAVConfig);
```

## <a name='3'></a>3、相关内置策略配置

#### videoDegradationPreference 自适应降级策略

* 开启自适应策略后，可根据不同的场景字使用调整分辨率，码率等。以下是支持的配置

```java
/**
 * 视频网络自适应降级策略
 */
public class LVAVConfig {
  
    /**
     * 维持帧率不变，网络糟糕时自动降低分辨率，保持帧率不变
     */
    public static final int MAINTAIN_FRAMERATE = 1;
    
    /**
     * 维持分辨率不变，也就网络糟糕的时候会降低视频帧率，保持视频分辨率不变
     */
    public static final int MAINTAIN_RESOLUTION = 2;
    
}
```

#### LVAVConfig （SDK 内置支持的分辨率）

* 支持多种分辨率，码率，帧率配置策略，可在 new LVAVConfig(LVAVConfig.PROFILE_540P) 中传递对应的配置枚举值进行设置。

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

### 切换摄像头

* 通过指定前后摄像头，调用切换摄像头接口可以切换推流视频的来源

```java
// 切换摄像头 LVConstants.CMRTCCameraPosition.FRONT | LVConstants.CMRTCCameraPosition.BACK
mRtcEngine.switchCamera(LVConstants.CMRTCCameraPosition.FRONT);
```

```java
/**
 *  摄像头类型枚举
 */
public static enum CMRTCCameraPosition {
    /**
     *   后置摄像头
     */
    BACK(0),
    /**
     *   前置摄像头
     */
    FRONT(1),
    /**
     *   外置摄像头
     */
    EXTERNAL(2);
};
```

### 设置是否自动调整视频输出方向

* 开启后，设备旋转那么视频输出方向也会自动旋转。开启后，setOutputVideoRotation 方法则会无效。

```objective-c
/**
 * 设置是否允许 SDK 自动根据设备的方向调整视频的输出方向
 * @param enable        打开和关闭（默认是 true）
 */
mRtcEngine.enableVideoAutoRotation(false);
```

### 手动管理视频输出方向

* 设置手动管理视频输出方向，该方法需要先调用 enableVideoAutoRotation，将自动旋转方法关闭设置为 false 才能生效

```java
/**
 * 设置手动管理视频输出方向，该方法需要先调用 enableVideoAutoRotation，将自动旋转方法关闭才能生效
 * @param rotation      视频输出方向，（默认是 LVConstants.CMVideoRotation.ROTATION_0））
 */
mRtcEngine.setOutputVideoRotation(LVConstants.CMVideoRotation.ROTATION_0);
```

## <a name='5'></a>5、常用分辨率、码率和帧率推荐

* 如果是多人连麦视频通话场景，建议分辨率可以低一些， 以减少贷款消耗和解码消耗。如果是一对一的场景下，分辨率和码率可以稍微高一些，增加清晰度。以下是推荐场景使用：

|                    一对一                    |                   多人连麦                   |
| :------------------------------------------: | :------------------------------------------: |
| 分辨率 320 x 240、帧率 15 fps、码率 200 Kbps | 分辨率 160 x 120、帧率 15 fps、码率 65 Kbps  |
| 分辨率 640 x 360、帧率 15 fps、码率 400 Kbps | 分辨率 320 x 180、帧率 15 fps、码率 140 Kbps |