# 混音伴奏

## <a name='1'></a>1、概述

SDK 支持混音功能，比如添加音效，或者播放背景音乐等，使用 SDK 混音伴奏功能，可以同时将音频数据和麦克风采集的数据混音之后进行发送。

## <a name='2'></a>2、说明

开启混音伴奏后，拉流端可以同时播放远端摄像头音视频数据和混音伴奏音频数据。

<img src="https://dl.linkv.io/doc/zh/android/rtc/images/diy_audio_extra.png" width="iOS_Auth2" style="width:60%;" />

## <a name='3'></a>3、使用步骤

### 开启混音伴奏

在确保登录房间并已经开始推流后，获取指定一个 MP3 路径，然后调用 startAudioMixing 方法，就可以开启混音。

```java
/**
 * 开始播放音乐文件及混音（声音伴奏）
 * @param filePath      String类型，文件路径
 * @param replace       布尔类型，true: 只推动设置的本地音频文件，不传输麦克风收录的音频  false：音频文件内容将会和麦克风采集的音频流进行混音
 * @param loop      int类型，指定音频文件循环播放的次数，正整数：循环的次数 -1：无限循环
 * @return      int类型，0 ： 方法调用成功，!0：失败
 */
mRtcEngine.startAudioMixing("/assets/audio.mp3", false, -1);
```

### 暂停/恢复混音

```objc
/**
 * 暂停播放音乐文件及混音。请在房间内调用该方法。
 * @return 0：方法调用成功 !0：方法调用失败
 */
mRtcEngine.pauseAudioMixing();
```

### 停止混音

```java
/**
 * 停止播放音乐文件及混音。请在房间内调用该方法。
 * @return      int类型，0：方法调用成功 !0：方法调用失败
 */
mRtcEngine.stopAudioMixing();
```

## <a name='4'></a>4、相关 API

###  获取伴奏音量

```java
/**
 * 获取当前伴奏音量，请在伴奏开始后调用。
 * @return      int类型，-1：伴奏未开始 0～100：当前伴奏音量
 */
mRtcEngine.getAudioMixingVolume();
```

### 调整伴奏音乐播放音量

```java
/**
 * 调节音乐文件的播放音量。请在房间内调用该方法。
 * @param volume        int类型，音量：0～100
 * @return      int类型，0：方法调用成功 !0：方法调用失败
 */
mRtcEngine.adjustAudioMixingVolume(100);
```

### 设置音乐文件的播放位置

```java
/**
 * 设置音乐文件的播放位置。请在房间内调用该方法。
 * @param pos       int类型，进度条位置，单位为毫秒
 * @return      int类型，0：方法调用成功 !0：方法调用失败
 */
mRtcEngine.setAudioMixingPosition(200);
```

### 获取当前伴奏文件总时长

```java
/**
 *  获取当前伴奏文件总时长，单位毫秒。请在房间内调用该方法。
 *  @return      long类型，文件总时长
 */
mRtcEngine.getAudioMixingTotalLength();
```

### 获取当前音乐播放进度

```java
/**
 *  获取音乐文件的播放进度。单位为毫秒。请在房间内调用该方法。
 *  @return      long类型，<0：方法调用失败 >=0：方法调用成功并返回伴奏播放进度
 */
mRtcEngine.getAudioMixingCurrentPosition();
```

## <a name='5'></a>5、示例 Demo

具体参考使用示例，可查看 [基础 SDK 演示 ](/?p=/zh/android/rtc/download_sdk.md&k=LKdNguJq)示例项目

