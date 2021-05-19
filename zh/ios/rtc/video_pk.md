# 跨房间连麦

## <a name='1'></a>1、功能描述

跨直播间连麦功能，指的是主播的流可以同时转发到多个直播房间内，实现主播跨房间与其它直播间的主播进行实时互动的场景。

连麦成功后，频道中的所有主播可以看见彼此，并听到彼此的声音，频道中的观众可以看到所有主播，并听到主播的声音。

该功能常用于 PK 连麦场景，直播间合唱等场景。

## <a name='2'></a>2、说明

#### 未连麦情况下

* 未连麦情况下，观众只能拉取到各个单独直播间的流，并且主播之间不能相互通话连麦。


#### 连麦情况下

* 主播 1 和 主播 2 分别开播自己的直播间，然后连麦过后，不同房间的主播即可相互通话和看到对方的画面，观众进入任意直播间也看看到直播间内所有主播。


## <a name='3'></a>3、相关 API

### 跨房间连麦

* 调用 linkRoom 方法，即可拉取指定房间的流到本房间。

> linkRoom 不会触发 OnAddRemoter有成员加入的回调。

```objc
// 房间之间 PK（跨房间连麦功能）
// @param roomId 房间 ID
[[LVRTCEngine sharedInstance] linkRoom:@""];
```

### 取消跨房间连麦

* 取消连麦的时候即可传递房间号，调用 unlinkRoom。

> unlinkRoom 不会触发 OnDeleteRemoter 有成员离开的回调。

```objc
// 取消跨房间连麦功能
// @param roomId 房间 ID
[[LVRTCEngine sharedInstance] unlinkRoom:@""];
```

## <a name='4'></a>4、业务参考步骤

（1）A 主播开播（房间号1001）

（2）B 主播开播（房间号1002）

（3）A 主播 linkRom (B主播房间号1002)

（4）B 主播 linkRom (B主播房间号1001)

（5）A ,B 主播跨房间连麦成功。

## <a name='5'></a>5、示例 Demo

具体参考使用示例，可查看 [互动直播 Demo ](/?p=/zh/ios/rtc/download_sdk.md&k=LKdNguJq)示例项目

