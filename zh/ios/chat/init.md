# 初始化

## <a name='1'></a>1、概述

集成 SDK 完成后，要想使用 SDK 的功能，需要先对SDK 进行`初始化`和`鉴权`，然后才能正常使用。

## <a name='2'></a>2、初始化步骤

### (1)申请AppID和AppSecret

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](http://doc.linkv.io/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV&m=ios)。

### (2)初始化SDK

```objective-c
[StrangerChat createEngine:your_app_id appKey:your_app_sign isTestEnv:NO completion:^(NSInteger code) {
  if (code == 0) {
		NSLog(@"SDK init succeed");
	}
 } delegate:self];
```

### (3)实现IM连接状态回调

```
- (void)onQueryIMToken {
	// 想你的服务端请求IMToken，你的服务端再向IM服务端请求IMToken，之后再返回给客户端，客户端再设置给SDK
	[[LVIMSDK sharedInstance] setIMToken:self.uid token:@"XXX"];
}

- (void)onIMTokenExpired:(NSString *)uid token:(NSString *)token owner:(NSString *)owner {
    // IMToken失效
}

- (void)onIMAuthSuccessed:(NSString *)uid token:(NSString *)token unReadMsgSize:(int)unReadMsgSize {
    // IM正常使用
    NSLog(@"[Wing] onIMAuthSuccessed");
}
```

## <a name='3'></a>3、呼叫、接听、挂断

![](https://raw.githubusercontent.com/linkv-io/StrangerChat/master/Snapshot/call_step.png)

(1) 传入某个用户的user_id进行呼叫

```
[self.engine call:"user_id" isAudio:NO extra:nil callback:nil];
```

(2) 被呼叫的用户会收到呼叫回调，在回调中进行接听或者挂断操作

```
- (int)onCallReceived:(NSString *)uid isAudio:(BOOL)isAudio timestamp:(int64_t)timestamp extra:(NSString *)extra {
	
 	// 接听电话
	[self.engine anwserCall:uid accept:NO isAudio:isAudio extra:@"time ount" callback:nil];
	return 0;
}
```

(3)接听或挂断某个用户的来电

```
// accept：YES接听，NO挂断
[self.engine anwserCall:uid accept:NO isAudio:isAudio extra:@"time ount" callback:nil];
```

(4) 收到某个用户接听或挂断的回调

```
- (int)onAnwserCallReceived:(NSString *)uid accept:(BOOL)accept isAudio:(BOOL)isAudio  timestamp:(int64_t)timestamp extra:(NSString *)extra {

	// 收到同意接听电话的回调
  return 0;
}

- (int)onHangupCallReceived:(NSString *)uid extra:(NSString *)extra {
    NSLog(@"[Wing] onHangupCallReceived uid = %@ extra = %@", uid, extra);
    
    // 收到挂断通话的回调
    return 0;
}
```

## <a name='4'></a>房间

1. 进入房间

```
[self.engine loginRoom:"user_id" roomId:"room_id" isHost:self.isCaller delegate:self];
```

2. 当收到onRoomConnected的时候表示进入房间成功
   1. 调用SDK的startPreview开始预览，startPreview返回的是视频流View，移动此View就能达到移动视频流的效果
   2. 调用SDK的startPublishing开始推流

```
// 进入房间成功
- (void)onRoomConnected:(NSString *)roomId {
    NSLog(@"[Wing] onLoginRoomSucceed thread %@", [NSThread currentThread]);
    
    // 开始预览
    self.meView = [self.engine startPreview:self.smallView];
    // 开始推流
    [self.engine startPublishing];    
}
```

3. 在收到onAddRemoter的时候调用SDK的startPlayingStream播放对方视频流， startPlayingStream返回的是对方视频流View，移动此View就能达到移动视频流的效果

```
// 收到对方视频流回调
- (void)onAddRemoterUser:(NSString *)uid {
    
    self.otherView = [self.engine startPlayingStream:uid inView:self.bigView];
    [self addNoCameraDefaultView:NO];
}
```

4. 在收到onRemoteLeave的回调时调用SDK的stopPlayingStream停止播放对方视频流

```
- (void)onRemoteLeave:(NSString *)uid {
    [self.engine stopPlayingStream:uid];    
}
```

5. 房间中的其它回调
   1. 对方关闭或者打开麦克风
   2. 对方关闭或者打开摄像头
   3. 收到礼物
   4. 房间断开连接

```
// 对方关闭或者打开麦克风的回调
- (int)onUserMicrophoneChanged:(NSString *)uid roomId:(NSString *)roomId open:(BOOL)isOpen {
    NSLog(@"[Wing] onUserMicrophoneChanged uid = %@ roomId = %@ open = %d", uid, roomId, isOpen);
    return 0;
}
// 对方关闭或打开摄像头的回调
- (int)onUserVideoCameraChanged:(NSString *)uid roomId:(NSString *)roomId open:(BOOL)isOpen {
    NSLog(@"[Wing] onUserVideoCameraChanged uid = %@ roomId = %@ open = %d", uid, roomId, isOpen);
    if (![uid isEqualToString:self.user.uid]) return 0;
    
    self.otherDefaultView.hidden = isOpen;
    return 0;
}
// 收到礼物消息
- (int)onGiftReceived:(NSString *)giftId count:(NSInteger)count sendUid:(NSString *)sendUid uid:(NSArray<NSString *> *)uids roomId:(NSString *)roomId extra:(NSString *)extra {
    NSLog(@"[Wing] onGiftReceived giftId = %@", giftId);
    
    int gid = [giftId intValue];
    LVGiftModel *gift = [LVHelper shared].gifts[gid];
    [self showGift: gift];
    
    [[LVHelper shared] changeBalance:-gift.giftPrice];
    
    return 0;
}

/**
 * 被踢出房间或断开房间链接
 * @param errorCode 错误码，参见Zego或LinkV错误码
 * @param roomId 房间id
 */
- (void)onRoomDisconnect:(int)errorCode roomId:(NSString *)roomId {
    NSLog(@"[Wing] onRoomDisconnect roomId = %@ errorCode = %@", roomId, @(errorCode));
}
```

