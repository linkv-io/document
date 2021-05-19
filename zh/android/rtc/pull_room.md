# 拉流

## <a name='1'></a>1、功能简介

在多人通话和互动直播等场景中，如果想要看到推流方推送的音视频画面声音，那么就需要进行拉流操作，才可以获取到视频画面和听到声音。

## <a name='3'></a>3、步骤

### 3.1 加入房间拉流

如果已经有一个开播的房间，那么  **新的用户** 加入房间的时候就会自动把房间里面的所有流拉下来。方法具体介绍，可参考 [登录房间](/?p=/zh/android/rtc/login_room.md&k=lD5BR0Hz)

```java
/**
 * 加入音视频房间（音视频会议）
 * @param roomId    房间Id
 * @param userId    用户Id
 * @param isHost    是否是主持人
 * @param isOnlyAudio    是否以音频模式加入，以音频模式加入，则没有视频流
 * @param callback    加入房间结果回调
 */
mRtcEngine.loginRoom(roomId, userId, isHost, isOnlyAudio, (code, cmUsers) -> {
    if (code == LVErrorCode.SUCCESS) {
        // 登陆成功
    } else {
        // 登陆失败
    }
});
```

### 3.2 加入房间回调

当调用 **loginRoom** 加入房间后，就会自动回调 LVResultCallback2 接口的 onResult方法，把房间内的所有用户都通过 **users** 集合回调出来。

```java
/**
 * 加入房间成功的回调
 * @param code      加入房间是否成功错误码
 * @param users     用户列表，如果房间中有用户存在，该列表会自动生效
 */
public interface LVResultCallback2<Integer, ArrayList<LVUser>>{
    void onResult(Integer code, ArrayList<LVUser>> users)
}
```

### 3.3 加入房间回调处理 - 播放拉下来的流

通过 startPlayingStream 可以播放指定用户的流。

```java
/**
 * 开始播放一路音视频流，播放状态的变更通过 onPlayStateUpdate 回调
 * @param userId        要播放的音视频流用户 ID
 */
mRtcEngine.startPlayingStream(userId);
```

### 3.4 停止播放流

stopPlayingStream 可以停止指定用户的流。

```java
/**
 * 停止播放一路音视频流
 * @param uid       要停止播放的音视频流用户 ID
 */
mRtcEngine.stopPlayingStream(uid);
```

## <a name='4'></a>4、拉流在具体业务场景中处理

### 业务场景中的处理抽象步骤可参考如下：

* 开播端

  1. startCapture 开启摄像头采集

  2. addDisplayView 添加绑定渲染推流视图

  3. loginRoom 登录房间，在 LVResultCallback2 接口的 onResult 方法中进行处理。

  4.  startPublishing 开始推流

* 加入端 - 拉流**

  1. loginRoom 登录房间，拉取房间所有流，在 LVResultCallback2 接口的 onResult 方法中进行处理。

  2. addDisplayView 添加绑定渲染推流视图，指定视图 uid。

  3. **startPlayingStream** 播放拉取的流

## <a name='5'></a>5、其他 API

#### 设置拉流时数据信息回调频率

* 拉流状态的变更通过 onPlayStateUpdate 方法进行回调。
* 通过设置拉流信息回调频率，在 onPlayStateUpdate 拿到相关质量信息。

```java
// 设置拉流时数据统计信息回掉的频率（必须在登录房间之前设置）
mRtcEngine.setPlayQualityMonitorCycle(1);

/**
 * 播放质量变化的通知，SDK 内部会定时统计拉流质量信息，APP 可以实现该方法获取拉流的视频质量信息统计，回掉的频率可以通过 setPlayQualityMonitorCycle 进行设置
 * @param stats         质量信息
 * @param userId        用户 ID
 */
void onPlayQualityUpdate(final LVVideoStatistic stats, final String userId);
```

#### LVVideoStatistic 数据信息回调类

* 此类包含了拉流的相关数据信息，包含当前帧率，分辨率，码率 等。

```java
// 视频编码帧数量
public int videoEncodeFrames

// 视频总发送包数量
public int videoSentPackets

// 视频总发送字节数
public long videoSentKBytes

// 视频输入帧率（视频帧率）
public int videoFps

// 视频丢包总数
public int videoLostPackets

// 音频丢包总数
public int audioLostPackets

// 当前可用的发送带宽
public int availableSendBandwidth

// 视频码率
public int videoBitrateBps

// 音频码率
public int audioBitrateBps

// 视频编码耗时（单位毫米），仅对视频发送方有效
public int videoAvgEncodeCostMs

// 音频包 RTT，单位 ms
public int audioRtt

// 视频包 RTT，单位 ms
public int videoRtt

// 累计视频丢包百分比
public int videoLostPercent

// 累计音频丢包百分比
public int audioLostPercent

// 推流：编码视频宽，拉流：输入视频帧宽
public int frameWidth

// 推流：编码视频高，拉流：输入视频帧高
public int frameHeight
```

## 示例 Demo 

* 拉流的使用，具体使用示例可参考  [基础 SDK 演示](/?p=/zh/android/rtc/download_sdk.md&k=LKdNguJq)

