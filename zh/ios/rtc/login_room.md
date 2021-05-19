# 登录房间

## <a name='1'></a>1、介绍

初始化 SDK 完成之后，在开始音视频通话前，需要先进行登录房间。主播创建登录房间，观众可以加入登录房间观看直播和主播进行互动。


## <a name='3'></a>3、相关概念

### 房间 / 主播

* 每一个房间的房间号都是唯一的，如果房间号对应的房间没有开播，那么主播可以指定房间号创建一个房间，然后推流。

### 观众

* 如果房间已经存在，用户可以指定房间号作为观众加入某个房间，在房间内进行拉流观看。
* 默认观众，加入房间后无法进行视频通话连麦，观众可以主动发起视频连麦与主播进行互动。

## <a name='4'></a>4、使用步骤

### 登录房间

* 如果已经有主播开播，会自动加入房间。

```objective-c
// 加入音视频房间（音视频会议）
// @param userId 用户 ID
// @param roomId 房间 ID
// @param isHost 是否是主持人
// @param isOnlyAudio 是否以音频模式加入，以音频模式加入，则没有视频流
// @param delegate 房间回调代理
[[LVRTCEngine sharedInstance] loginRoom:[LVRTCTool shareInstance].userId
                                 roomId:self.roomId
                                 isHost:self.isHost
                            isOnlyAudio:true
                               delegate:self];
```

* userId
  * userId 用户 id，需要确保全局唯一，开发者可以将用户 id 和 app 业务账号进行关联。
* roomId
  * roomId 房间 id ，如果想要创建不同的直播房间，需要保证 roomID 信息的全局唯一，否则用户登录的就是相同的房间，相当于加入一个已存在的房间。
* isHost
  * 如果是主播开播一个新的房间，那么 isHost 需要传递 true。
  * 如果是观众加入一个已经存在的房间，那么 isHost 需要传递 false。
* isOnlyAudio
  * isOnlyAudio 可以决定是否以音频模式加入，或者视频模式加入。
  * 主播端
    * 如果作为主播登录房间 isOnlyAudio 传 ture 的时候，不会影响推流。音频流和视频流都会进行推。
  * 观众端（ isOnlyAudio 主要针对观众端）
    * 如果以音频模式加入 isOnlyAudio 传 true 时候，那么不会拉取到视频流只会拉取到音频流。
* delegate
  * 可传递一个 遵循 LVRTCEngineDelegate 协议的代理对象，loginRoom 登录房间后所有相应的房间事件状态都会通过 delegate 对象传递。

> userId 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>
> roomId 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

### 登出房间

* 在退出房间的时候可调用此 api ，退出房间是否成功会通过 [退出房间错误码](/?p=/zh/ios/rtc/ecode.md&k=WZsw8kGY) 返回。

```objective-c
// 退出房间
// @param completion 离开房间结果回掉
[[LVRTCEngine sharedInstance] logoutRoom:^(LVErrorCode code) {
        NSLog(@"logoutRoom:%lu",(unsigned long)code);
}];
```

* 退出房间会触发 **OnDeleteRemoter** 代理回调，在此回调中可做相关处理。

```objc
// 有成员离开的通知
// @param uid 离开用户 ID
- (void)OnDeleteRemoter:(NSString*)uid;
```

## <a name='5'></a>5、房间事件

通过 loginRoom 方法调用，遵循  LVRTCEngineDelegate 代理的回调，在不同的回调里面可以做不同的业务处理。

### 相关事件回调

```objective-c
// 加入房间成功的回调
// @param code 加入房间是否成功错误码
// @param users 用户列表，如果房间中有用户存在，该列表会自动生效
- (void)OnEnterRoomComplete:(LVErrorCode)code users:(nullable NSArray<LVUser*>*)users;

// 退出房间完成，异常退出和用户主动调用 logoutRoom 方法会触发该回掉方法
- (void)OnExitRoomComplete;

// 房间断开的通知，网络异常时 SDK 会自动进行重连，90 秒如果重连失败会触发该方法回掉
// @param code 错误码
- (void)OnRoomDisconnect:(LVErrorCode)code;

// 有成员加入的通知
// @param users 成员列表
- (void)OnAddRemoter:(NSArray<LVUser*>*)users;

// 有成员离开的通知
// @param uid 离开用户 ID
- (void)OnDeleteRemoter:(NSString*)uid;

/// 用户被踢出房间
/// @param reason 被踢原因
/// @param roomId 房间号
- (void)onKickOff:(NSInteger)reason roomId:(NSString *)roomId;

// 房间重连成功通知，SDK 在网络断开和恢复时会自动进行重连，重连结果通过该回掉通知 APP
- (void)OnRoomReconnected;
```

### 方法解析

* OnEnterRoomComplete
  * 调用 loginRoom 方法登录房间之后 会回调此代理方法，在此方法中可进行做推流处理，如果登录房间失败，也会返回对应的错误码。

* OnExitRoomComplete
  * 调用 logoutRoom 方法后，会触发 OnExitRoomComplete 此回调方法，代表退出房间成功。
* OnRoomDisconnect
  * 如果网络不好，房间断开，SDK 内部会自动自动进行重连，90 秒如果重连失败就会触发该方法回调此方法。
* OnAddRemoter
  * 当在直播间内，有新成员 startPublishing 发起推流的时候，房间内其它人就会触发此回调方法，在此方法内可以播放新成员的流处理添加视图渲染。
* OnDeleteRemoter
  * 房间内有人退出房间的时候，就会回调此方法，可以在此方法内处理删除房间内成员视图，停止播放流等处理。
* OnRoomReconnected
  *  房间重连成功通知，SDK 在网络断开和恢复时会自动进行重连，重连结果通过该回掉通知 APP。
* onKickOff
  * 当用户被踢出的时候，会回调此方法，告知被踢出和原因。