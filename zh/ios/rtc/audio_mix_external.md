# 自定义音频采集

## <a name='1'></a>1、介绍

实时音视频传输过程中默认会采集摄像头的音视频数据，如果app 有自己音频输入源，希望能够单独输入音频数据源，并且不希望是混音伴奏环境，那么就可以使用自定义音频采集数据源。

## <a name='2'></a>2、说明

自定义音频采集，拉流端听到的是推流端推的自定义音频流。

## <a name='3'></a>3、步骤

（1）打开外置音频采集功能

（2）登录房间并推流

（3）对音频进行解码

（4）调用发送发送外置音频数据

## <a name='4'></a>4、相关 API

#### 打开和关闭外置音频采集功能 （加入房间之前设置）

```objc
// 打开和关闭外置音频采集功能，该参数如果打卡会自动将 SDK 内置麦克风功能禁用，由用户向 SDK 输入音频 PCM 数据。
// @param enable true: 打卡，false: 关闭
[[LVRTCEngine sharedInstance] enableExternalAudioInput:true]; 
```

#### 发送外置音频数据

```objc
// 发送外置音频数据，注：只有调用 enableExternalAudioInput 打开外部音频输入接口之后才会生效
// @param audioFrameBuffer 音频数据
// @param length 音频数据长度（int16_t 数组数据长度）
// @return 发送成功与否
[[LVRTCEngine sharedInstance] sendAudioFrame:buffer length:(int)length];
```

#### 设置外置音频数据参数

```objc
/// 设置外置音频数据参数
/// @param audioConfig 音频参数
-(void)setExternalAudioConfig:(LVAudioRecordConfig *)audioConfig;
```

#### LVAudioRecordConfig 外置音频参数

* 开启外置音频后可自定义外置音频采样率, 频道等。如果不设置，那么默认走默认值。

```objc
/// 外置音频采集参数配置
@interface LVAudioRecordConfig : NSObject

/// 外置音频采集输入采样率（默认 48000）
@property (nonatomic,assign)int sampleRate;

/// 外置音频采集输入频道数 （默认 1）
@property (nonatomic,assign)int channels;

/// 每个 buffer 输入的数据长度（该参数必须和 sendAudioBuffer 的接口传入的数据长度一致）
@property (nonatomic,assign)int framesPerBuffer;

@end
```

## <a name='5'></a>5、示例Demo

具体参考使用示例，可查看 [基础 SDK 演示 ](/?p=/zh/ios/rtc/download_sdk.md&k=LKdNguJq)示例项目

