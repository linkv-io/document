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

```java
/**
 *  开启或关闭麦克风
 *  @param enbale       true 开启，false 关闭（默认为 true）
 */
mRtcEngine.enableMic(enable);
```

### 2、扬声器和听筒切换

该接口可以控制扬声器播放音频和听筒播放音频的切换。

```java
/**
 *  扬声器和听筒切换功能
 *  @param enable       true 视同扬声器播放音频，false 使用听筒播放音频。（默认 true）
 */
mRtcEngine.enableSpeakerphone(false);
```

### 3、设置远端用户音量

以通过setPlayVolume 接口控制远端用户的音量。

```java
/**
 *  设置远端用户音量，加入房间成功后调用
 *  @param userId       String类型，被控制的用户id
 *  @param volume       int类型，音量大小，范围0到100
 */
mRtcEngine.setPlayVolume(userId, 100);
```

### 4、获取用户的音量信息

获取远端用户音量的信息。

```java
/**
 *  获取用户音量大小
 *  @param userId       String类型，被控制的用户id
 *  return       int类型，音量大小，范围0到100
 */
mRtcEngine.getSoundLevelByUserId(userId);
```

### 5、开启音量变化监听

#### （1）API 调用

```java
/**
 *  开启音量监听回调，开启后会收到LVRTCCallback.onAudioVolumeUpdate(ArrayList)
 *  @param timeInMs       int类型，回调时间间隔，单位毫秒
 */
mRtcEngine.startSoundLevelMonitor(100);

/**
 *  设置音频录制模式，可同时设置多种录制模式，录制结果会通过LVRTCCallback.onAudioMixStream() 回调
 *  @param types      AudioRecordType枚举类型，音频录制模式
 */
mRtcEngine.setAudioRecordFlag(LVConstants.AudioRecordType.NONE);
```

#### （2）音量变化监听回调

打开音量变化监听方法才会生效 startSoundLevelMonitor 执行

```java
/**
 *  当前用户音量变化的通知，该回调需要调用打开音量变化监听方法才会生效 startSoundLevelMonitor
 *  @param volumes      音量级别信息
 */
void onAudioVolumeUpdate(ArrayList<LVAudioVolume> volumes);
```

#### （3）LVAudioVolume 用户音量信息类

* onAudioVolumeUpdate 回调会告诉是哪个用户的音量变化了，和变化后的音量信息

````java
/// 用户音量信息
public class LVAudioVolume {

    /// 用户ID
    public String userId;
    
    /// 音量
    public int volume;

}
````

#### （4）设置音频数据回调类型

* 通过设置音频数据回调类型，可以控制回调数据的类型，例如只回调远端用户音量数据或者本地采集的音量数据

```java
/**
 音频数据回调类型（声音数据录制模式）
 */
public static enum AudioRecordType {
    /**
     * 不需要回掉音频数据
     */
    NONE(0),
    
    /**
     * 只回掉远端用户数据
     */
    PLAYBACK(1),
    
    /**
     * 只回掉本地 mic 采集的数据
     */
    MICPHONE(2),
    
    /**
     * 回掉混音之后的音频数据
     */
    MIX(4);
}
```

### 6、停止音量变化的监听

调用 stopSoundLevelMonitor 方法就可以通知音量变化监听。

```java
/**
 * 停止音量监听回调
 */
mRtcEngine.stopSoundLevelMonitor();
```

