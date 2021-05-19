#  自定义视频采集

## <a name='1'></a>1、简介

自定义视频采集的功能指的是由开发者自定义向 LinkV SDK 提供视频输入源输入视频数据，并由 LinkV SDK 进行编码推流的功能。

当用户开启自定义视频采集的功能后，本地摄像头采集预览会无效。

## <a name='2'></a>2、说明

#### 采集本地摄像头数据

* 采集本地摄像头数据，拉流端看到的是摄像头采集的数据。

<img src="https://dl.linkv.io/doc/zh/android/rtc/images/diy_video_extra.png" alt="iOS_Auth2" style="width:50%;" />

#### 自定义视频采集

* 自定义视频采集，拉流端看到的是推流端任意设置的推流的本地视频数据

<img src="https://dl.linkv.io/doc/zh/android/rtc/images/diy_video_extra2.png" width="iOS_Auth2" style="width:50%;" />

## <a name='3'></a>3、业务使用步骤

（1）打开外置视频采集功能

（2）登录房间并推流

（3）对外置视频进行解码

（4）调用发送发送外置视频数据

## <a name='4'></a>4、相关 API

### 4.1 发送外部采集视频数据 

调用此方法，发送解码后的外置视频数据。

```java
/** 
 * 外部采集的视频数据，目前只支持I420格式
 * @param data      ByteBuffer类型，I420格式的byte数组。
 * @param width      int类型，采集数据宽。
 * @param height      int类型，采集数据高。
 * @param rotate      int类型，采集数据方向信息。
 * @param format       int类型，格式请参考LVConstants.VideoFrameType，目前只支持I420格式。
 * @param timestamp      long类型，该帧frame时间戳，单位毫秒。
 * @param sei      String类型，该帧扩展信息。
 */
mRtcEngine.sendVideoFrame(data, width, height, rotate, format, timestamp, sei);
```

