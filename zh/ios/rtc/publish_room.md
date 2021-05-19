# 推流

## <a name='1'></a>1、功能简介

在多人通话和互动直播等场景中，如果想要其他人能够看到自己的画面和听到自己的声音，那么就需要先推送自己的音视频画面和声音到 云端服务上。然后对端再从 云端服务 上拉取音视频流，才可以获取到视频画面和听到声音。

## <a name='3'></a>3、步骤

### 推流相关 API

* 登录房间成功后即可进行推流操作，**如果要推音频和视频流则必须先开启本地摄像头采集**。

* 如果登录房间的时候 isOnlyAudio 参数为 YES 则只发送音频数据，视频数据不会发送，拉流方只能拉取到音频数据。

```objc
// 发布音视频数据（推流）
[[LVRTCEngine sharedInstance] startPublishing];

// 停止发布音视频数据
[[LVRTCEngine sharedInstance] stopPublishing];
```

### 推流状态变更的通知

* 调用 **startPublishing** 推流之后 SDK 会回调推流是否成功返回对应的错误码。

* 错误码可参考  [推流状态回调错误码](/?p=/zh/ios/rtc/ecode.md&k=WZsw8kGY)

```objective-c
// 发布资源状态变更的通知，调用 startPublishing 之后会触发该方法回掉，发布资源状态的变更会通过该方法进行通知
// @param code 状态码
- (void)OnPublishStateUpdate:(LVErrorCode)code;
```

## <a name='4'></a>4、推流在具体业务场景中处理

#### 具体在业务场景中的处理抽象步骤可参考如下：

* **开播端 - 推流**

  1. startCapture 开启摄像头采集

  2. addDisplayView 添加绑定渲染推流视图

  3. loginRoom 登录房间，在OnEnterRoomComplete 中进行处理。

  4. **startPublishing** 开始推流

* 加入端
  1. loginRoom 登录房间，拉取房间所有流，在OnEnterRoomComplete 中进行处理。

  2. addDisplayView 添加绑定渲染推流视图，指定视图 uid。

  3. startPlayingStream 播放房间内的流。

## <a name='5'></a>5、其它 API

#### 设置推流信息回调频率

* 推流状态的变更通过 OnPublishStateUpdate 方法进行回调。
* 通过设置推流信息回调频率，在OnPublishQualityUpdate 拿到相关质量信息。

```objective-c
// 设置推流时数据统计信息回掉的频率（必须在登录房间之前设置）
[LVRTCEngine setPublishQualityMonitorCycle:1];

// 推流质量状态变化的通知，SDK 内部会定时统计推流的质量信息，APP 可以实现该方法获取推流的视频质量信息统计，回掉的频率可以通过 +setPublishQualityMonitorCycle 进行设置
// @param quality 质量信息
- (void)OnPublishQualityUpdate:(LVVideoStatistic *)quality;
```

#### LVVideoStatistic 数据信息回调类

* 此类包含了推流的相关数据信息，包含当前帧率，分辨率，码率 等。

```objective-c
// 视频编码帧数量
@property (nonatomic, assign) int       videoEncodeFrames;

// 视频总发送包数量
@property (nonatomic, assign) int       videoSentPackets;

// 视频总发送字节数
@property (nonatomic, assign) long long videosentKbytes;

// 视频输入帧率（视频帧率）
@property (nonatomic, assign) int       videoFps;

// 视频丢包总数
@property (nonatomic, assign) int       videoLostPackets;

// 音频丢包总数
@property (nonatomic, assign) int       audioLostPackets;

// 当前可用的发送带宽
@property (nonatomic, assign) int       availableSendBandwidth;

// 视频码率
@property (nonatomic, assign) int       videobitratebps;

// 音频码率
@property (nonatomic, assign) int       audiobitratebps;

// 视频编码耗时（单位毫米），仅对视频发送方有效
@property (nonatomic, assign) int       videoAvgEncodeCostMs;

// 音频包 RTT，单位 ms
@property (nonatomic, assign) int       audioRtt;

// 视频包 RTT，单位 ms
@property (nonatomic, assign) int       videoRtt;

// 累计视频丢包百分比
@property (nonatomic, assign) int       videoLostPercent;

// 累计音频丢包百分比
@property (nonatomic, assign) int       audioLostPercent;

// 推流：编码视频宽，拉流：输入视频帧宽
@property (nonatomic, assign) int       frameWidth;

// 推流：编码视频高，拉流：输入视频帧高
@property (nonatomic, assign) int       frameHeight;
```

## 示例 Demo 

* 拉流的使用，具体使用示例可参考  [基础 SDK 演示](/?p=/zh/ios/rtc/download_sdk.md&k=LKdNguJq)

