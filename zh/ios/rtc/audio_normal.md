# 音频常用功能

## <a name='1'></a>1、概述

音频常用功能包含开关麦克风，扬声器听筒切换，设置远端用户静音，音量变化监听，等常用的功能。

## <a name='2'></a>2、常用功能

* 开启关闭麦克风
* 扬声器和听筒切换
* 设置远端用户音量
* 获取用户音量信息
* 开启音量变化监听

### 1、开启关闭麦克风

该接口可以将麦克风禁止或开启。

```objective-c
// 开启或关闭麦克风
// @param enbale true 开启，false 关闭（默认为 true）
// @return true 成功，false 失败
// @discussion 推流时可调用本 API 进行参数配置
[[LVRTCEngine sharedInstance] enableMic:true];
```

### 2、扬声器和听筒切换

该接口可以控制扬声器播放音频和听筒播放音频的切换。

```objective-c
// 扬声器和听筒切换功能
// @param enable true 视同扬声器播放音频，false 使用听筒播放音频。（默认 true）
// @return true 成功，false 失败
[[LVRTCEngine sharedInstance] enableSpeaker:true];
```

### 3、设置远端用户音量

通过 muteAudio 接口可以直接设置远端用户禁音，也可以通过setPlayVolume 接口 控制远端用户的音量。

```objective-c
// 设置远端用户禁音
// @param mute 是否禁音标识
// @param userId 用户 ID
[[LVRTCEngine sharedInstance] muteAudio:false userId:@""];
```

```objc
// 控制远端音频流音量, 加入房间成功后调用
// @param volume 音量大小（0，100）
// @param userId 被控制的用户ID
[[LVRTCEngine sharedInstance] setPlayVolume:50 userId:@""];
```

### 4、获取用户的音量信息

获取远端用户音量的信息。

```objective-c
// 获取用户的音量信息
// @param userId 用户 ID
// @return 用户 ID 对应的音量数据
- (int)getSoundLevelByUserId:(NSString *)userId;
```

### 5、开启音量变化监听

#### （1）API 调用

```objective-c
// 开启音量变化监听，并设置音量变化监听回掉频率
[[LVRTCEngine sharedInstance] startSoundLevelMonitor:100];

// 声音数据回调参数设置
[[LVRTCEngine sharedInstance] setAudioRecordFlag:LVAudioRecordTypeNone];
```

#### （2）音量变化监听回调

打开音量变化监听方法才会生效 startSoundLevelMonitor 执行

```objc
/// 当前用户音量变化的通知，该回调需要调用打开音量变化监听方法才会生效 startSoundLevelMonitor
/// @param captureSoundLevel 音量级别信息
- (void)OnCaptureSoundLevelUpdate:(nonnull LVAudioVolume *)captureSoundLevel;
```

#### （3）LVAudioVolume 用户音量信息类

* OnCaptureSoundLevelUpdate 回调 会告诉是哪个用户的音量变化了，和变化后的音量信息

````objc
/// 用户音量信息
@interface LVAudioVolume : NSObject

/// 用户标识
@property (nullable, nonatomic, copy)     NSString*   userId;

/// 音量
@property (nonatomic, assign) int       volume;

@end
````

#### （4）设置音频数据回调类型

* 通过设置音频数据回调类型，可以控制回调数据的类型，例如只回调远端用户音量数据或者本地采集的音量数据

```objc
/**
 音频数据回调类型（声音数据录制模式）
 */
typedef NS_ENUM(NSInteger, LVAudioRecordType) {
    /**
        不需要回掉音频数据
     */
    LVAudioRecordTypeNone         = 0,
    /**
        只回掉远端用户数据
     */
    LVAudioRecordTypePlayBack     = 0x01,
    /**
        只回掉本地 mic 采集的数据
     */
    LVAudioRecordTypeMicrophone   = 0x02,
    /**
        回掉混音之后的音频数据
     */
    LVAudioRecordTypeMix          = 0x04,
};
```

### 6、停止音量变化的监听

调用 stopSoundLevelMonitor 方法就可以通知音量变化监听。

```objective-c
// 停止音量变化的监听
[[LVRTCEngine sharedInstance] stopSoundLevelMonitor];
```

