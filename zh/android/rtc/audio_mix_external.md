# 自定义音频采集

## <a name='1'></a>1、介绍

实时音视频传输过程中默认会采集摄像头的音视频数据，如果app 有自己音频输入源，希望能够单独输入音频数据源，并且不希望是混音伴奏环境，那么就可以使用自定义音频采集数据源。

## <a name='2'></a>2、说明

自定义音频采集，拉流端听到的是推流端推的自定义音频流。

<img src="https://dl.linkv.io/doc/zh/android/rtc/images/diy_audio_extra2.png" width="iOS_Auth2" style="width:50%;" />

## <a name='3'></a>3、步骤

（1）打开外置音频采集功能

（2）登录房间并推流

（3）对音频进行解码

（4）调用发送发送外置音频数据

## <a name='4'></a>4、相关 API

#### 打开和关闭外置音频采集功能 （加入房间之前设置）

```java
/**
 * 打开和关闭外置音频采集功能，该参数如果打卡会自动将 SDK 内置麦克风功能禁用，由用户向 SDK 输入音频 PCM 数据。
 * @param enable        布尔类型，true: 打卡，false: 关闭
 */
mRtcEngine.enableExternalAudioInput(true);
```

#### 发送外置音频数据

```java
/**
 *  发送外置音频数据，注：只有调用 enableExternalAudioInput 打开外部音频输入接口之后才会生效
 * @param data          byte数组类型，音频数据
 * @return      int类型，0表示失败；!0表示成功。
 */
mRtcEngine.sendAudioFrame(audioData);
```

#### 设置外置音频数据参数

```java
/**
 * 设置外置音频数据参数
 * @param audioConfig       音频参数
 */
mRtcEngine.setExternalAudioConfig(audioConfig);
```

#### LVAudioRecordConfig 外置音频参数

* 开启外置音频后可自定义外置音频采样率, 频道等。如果不设置，那么默认走默认值。

```java
// 外置音频采集参数配置
public class LVExternalAudioConfig {

    // 外置音频采集输入采样率（默认 4800000）
    private int sampleRate = 4800000;
    
    // 外置音频采集输入频道数 （默认 1）
    private int channels = 1;

}
```

## <a name='5'></a>5、示例Demo

具体参考使用示例，可查看 [基础 SDK 演示 ](/?p=/zh/android/rtc/download_sdk.md&k=LKdNguJq)示例项目

