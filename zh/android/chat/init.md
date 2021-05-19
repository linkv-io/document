# 初始化

## 1、概述

集成 SDK 完成后，要想使用 SDK 的功能，需要先对SDK 进行`初始化`和`鉴权`，然后才能正常使用。

## 2、初始化步骤

### (1)申请AppID和AppSecret

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](http://dev.linkv.io/)。

### (2)初始化SDK

```java
StrangerChat mEngine = StrangerChat.createEngine(application, Constants.APP_ID, Constants.APP_SECRET, false,
                i -> {
                    LogUtils.d(TAG, "onInitResult code = " + i);
                }, this);
```

### (3)实现IM连接状态回调

```
 @Override
    public void onQueryIMToken() {
    		// 此处传入token，token由您的服务器获取。
        LVIMSDK.sharedInstance().setIMToken("登录IM的userId", "xxx");
    }

    @Override
    public void onIMAuthFailed(String uid, String token, int ecode, int rcode, boolean isTokenExpired) {
        // IM鉴权失败
    }

    @Override
    public void onIMAuthSucceed(String uid, String token, long unReadMsgSize) {
				// IM鉴权成功

    }

    @Override
    public void onIMTokenExpired(String uid, String token) {
        // IM Token过期
    }

```

## 3、呼叫、接听、挂断

![](https://raw.githubusercontent.com/linkv-io/StrangerChat/master/Snapshot/call_step.png)

(1) 传入某个用户的user_id进行呼叫

```java
mEngine.call(tid, false, "", null);
```

(2) 被呼叫的用户会收到呼叫回调，在回调中进行接听或者挂断操作

```java
@Override
public int onCallReceived(String uid, boolean isAudio, long timestamp, String extra) {
    mRingTonCallPlayer.stopRingtone();
    IncomingCallActivity.actionStart(this, uid);
    return 0;
}
```

(3)接听或挂断某个用户的来电

```java
// 第2个参数传true为接听，false为挂断
mEngine.answerCall(”对方用户ID“, true, false, "", null);
```

(4) 收到某个用户接听或挂断的回调

```java
@Override
public int onAnswerCallReceived(String uid, boolean accept, boolean isAudio, long timestamp, String extra) {
    // 收到同意接听电话的回调
    return 0;
}

@Override
public int onHangupCallReceived(String uid, String extra) {
    // 收到同意接听电话的回调
    return 0;
}

```

## 房间

1. 进入房间

```
mEngine.loginRoom("登录用户的id", mRoomId, true);
```

2. 当收到onRoomConnected的时候表示进入房间成功
   1. 调用SDK的startPreview开始预览，startPreview返回的是视频流View，移动此View就能达到移动视频流的效果
   2. 调用SDK的startPublishing开始推流

```
// 进入房间成功
 @Override
 public void onRoomConnected(String s) {
     // 进入房间成功，开启预览。
     mStrangerChatEngine.startPreview("登录用户的id", mContainerVideoSmall, true);
     // 开始推流
     mStrangerChatEngine.startPublishing();
 }
```

3. 在收到onRemoteStreamAdd的时候调用SDK的startPlayingStream播放对方视频流， startPlayingStream返回的是对方视频流View，移动此View就能达到移动视频流的效果

```java
// 收到对方视频流回调
@Override
public void onRemoteStreamAdd(String userId) {
    LogUtils.d(TAG, "onRemoteStreamAdd = " + userId);
    // 拉流
    mEngine.startPlayingStream(userId, mContainerVideoLarge, false);
}
```

4. 在收到onRemoteStreamEnd的回调时调用SDK的stopPlayingStream停止播放对方视频流

```java
    public void onRemoteStreamEnd(String userId) {
        // 远端流退出,停止拉流。
        mEngine.stopPlayingStream();
    }
```

5. 房间中的其它回调
   1. 对方关闭或者打开麦克风
   2. 对方关闭或者打开摄像头
   3. 收到礼物
   4. 房间断开连接

```java
// 收到某个用户发送给一批用户的礼物消息
int onGiftReceived(String giftId, int count, String sendUid, List<String> uids, String roomId, String extra);

// 某个用户的麦克风状态发生了变化
int onUserMicrophoneChanged(String uid, String roomId, boolean isOpen);

// 某个用户的摄像头状态发生了变化
int onUserVideoCameraChanged(String uid, String roomId, boolean isOpen);
```

