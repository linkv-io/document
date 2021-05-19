# 媒体补充增强信息(SEI)

## <a name='1'></a>1、简介

在LinkV SDK 中 当推流的时候，远端拉流后会收到 onDrawFrame 方法的回调，也就是收到远端视频数据的时候会回调这个方法。如果想要在推流的时候附加文本信息，然后在拉流端进行接收，就用到 sei 实现文本数据和音视频内容数据的同步。

一般可用于歌词同步，直播答题 等需要随视频数据下发同步文本的场景。

## <a name='2'></a>2、使用步骤

* 调用 LVRTCEngine 的 setLiveRoomCallback 方法设置实现接口 LVRTCCallback，然后在推流方的代理方法中反馈对应的 sei 信息。

* 在拉流方的远程视频数据回调的代理方法中接受到对应的 sei 数据信息。

### 2.2. 推流方

* SDK 发送视频时会回调下面方法，开发者可以返回需要随视频携带的信息即可。

* 此方法每一帧都会回调，会调用多次，需要控制处理。

```java
/**
 *  是否需要在视频帧上附加其他媒体信息
 *  @return     请返回要随当前视频帧发送的附加数据（字符串最长长度 24 个字符）
 */
 String onMediaSideInfoInPublishVideoFrame() {
    return data;
}
```

### 2.3. 拉流方

* 远端用户收到该自定义数据时会收到自定义数据的通知

```java
/**
 *  收到远端视频数据回掉，如果为 SDK 设置了渲染视图，SDK 内部会自动将该视频帧渲染出来
 *  @param i420Buffer       ByteBuffer类型，i420 byte数组
 *  @param width        int类型，视频帧宽
 *  @param height       int类型，视频帧高
 *  @param stride       int类型，该帧数据stride
 *  @param userId       String类型，该帧数据对应的用户id
 *  @param ext          String类型，随视频数据携带的附加数据信息
 *  @return     long类型，建议返回当前渲染完成的时间戳，用以统计渲染延迟
 */
long onDrawFrame(ByteBuffer i420Buffer, final int width, final int height, int strideY, final String userId, String ext)
```