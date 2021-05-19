# 媒体补充增强信息(SEI)

## <a name='1'></a>1、简介

在LinkV SDK 中 当推流的时候，远端拉流后会收到 OnDrawFrame 方法的回调，也就是收到远端视频数据的时候会回调这个方法。如果想要在推流的时候附加文本信息，然后在拉流端进行接收，就用到 sei 实现文本数据和音视频内容数据的同步。

一般可用于歌词同步，直播答题 等需要随视频数据下发同步文本的场景。

## <a name='2'></a>2、使用步骤

* 实现 loginRoom 的 delegate 方法，然后在推流方的代理方法中反馈对应的 sei 信息。

* 在拉流方的 远程视频数据回调的代理方法中接受到对应的 sei 数据信息。

### 2.2. 推流方

* SDK 发送视频时会回调下面方法，开发者可以返回需要随视频携带的信息即可。

* 此方法每一帧都会回调，会调用多次，需要控制处理。

```objc
// 是否需要在视频帧上附加其他媒体信息
// @param timestamp 当前要发送数据帧的时间戳
// @return 请返回要随当前视频帧发送的附加数据 （字符串最长长度 24 个字符）
- (NSString *)onMediaSideInfoInPublishVideoFrame:(NSUInteger)timestamp{
    return @"extra data";
}
```

### 2.3. 拉流方

* 远端用户收到该自定义数据时会收到自定义数据的通知

```objc
// 收到远端视频数据回掉，如果为 SDK 设置了渲染视图，SDK 内部会自动将该视频帧渲染出来
// @param pixelBuffer 已解码的视频数据
// @param uid 用户 ID
// @param sei 随视频数据携带的附加数据信息
// @return 建议返回当前渲染完成的时间戳，用以统计渲染延迟
// @discussion 注：如果用户实现该接口，则 SDK 内部的远端视频渲染会自动实现，渲染完全由外部进行实现
- (int64_t)OnDrawFrame:(CVPixelBufferRef)pixelBuffer
                   uid:(NSString *)uid
                   sei:(NSString *)sei{
	NSLog(@"%@", sei);                 
}
```