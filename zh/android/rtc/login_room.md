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

```java
/**
 * 加入音视频房间（音视频会议）
 * @param roomId    房间ID
 * @param userId    用户ID
 * @param isHost    是否是主持人
 * @param isOnlyAudio    是否以音频模式加入，以音频模式加入，则没有视频流
 * @param callback    房间回调监听
 */
mRtcEngine.loginRoom(roomId, userId, isHost, isOnlyAudio, (code, cmUsers) -> {
    if (code == LVErrorCode.SUCCESS) {
        // 登陆成功
    } else {
        // 登陆失败
    }
});
```

* userId
  * userId 用户 id，需要确保全局唯一，开发者可以将用户 id 和 app 业务账号进行关联。
* roomId
  * roomId 房间 id ，如果想要创建不同的直播房间，需要保证 roomId 信息的全局唯一，否则用户登录的就是相同的房间，相当于加入一个已存在的房间。
* isHost
  * 如果是主播开播一个新的房间，那么 isHost 需要传递 true。
  * 如果是观众加入一个已经存在的房间，那么 isHost 需要传递 false。
* isOnlyAudio
  * isOnlyAudio 可以决定是否以音频模式加入，或者视频模式加入。
  * 主播端
    * 如果作为主播登录房间 isOnlyAudio 传 ture 的时候，不会影响推流。音频流和视频流都会进行推。
  * 观众端（ isOnlyAudio 主要针对观众端）
    * 如果以音频模式加入 isOnlyAudio 传 true 时候，那么不会拉取到视频流只会拉取到音频流。
* callback
  * 可传递一个 LVResultCallback2 类型的实例化对象，loginRoom 登录房间后所有相应的房间事件状态都会通过 callback 对象传递。

> userId 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>
> roomId 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

### 登出房间

* 在退出房间的时候可调用此 api ，退出房间是否成功会通过 [退出房间错误码](/zh/android/rtc/ecode.md)返回。

```java
/**
* 退出房间
* @param   callback 离开房间结果回掉
*/
mRtcEngine.logoutRoom(callback);
```

* 退出房间会触发 **OnDeleteRemoter** 代理回调，在此回调中可做相关处理。

```java
/**
* 有成员离开的通知
* @param callback   离开用户ID
*/
public void onDeleteRemoter(String userId);
```

## <a name='5'></a>5、房间事件

### 5.1、登陆房间监听

通过 loginRoom 方法设置 LVResultCallback2 类型的对象作为监听，LVResultCallback2 对象在登陆房间后会回调相应的状态。

```java
/**
* 加入房间的回调
* @param code       加入房间状态码
* @param users      用户列表，如果房间中有用户存在，该列表会自动生效
*/
public interface LVResultCallback2<Integer, ArrayList<LVUser>>> {
    void onResult(Integer code, ArrayList<LVUser>> users);
}
```

### 5.2、登出房间监听

通过 logoutRoom 方法设置 LVResultCallback1 类型的对象作为监听，LVResultCallback1 对象在登出房间后会回调相应的状态。

```java
/**
* 退出房间的回调
* @param code       退出房间状态码
*/
public interface LVResultCallback1<Integer> {
    void onResult(Integer code);
}
```

### 5.3、其他房间监听

通过 setLiveRoomCallback 方法设置 LVRTCCallback 类型的对象作为监听，LVRTCCallback 对象会监听房间的相关状态，并回调对应的方法。

```java
/**
* 房间断开的通知，网络异常时 SDK 会自动进行重连，90 秒如果重连失败会触发该方法回掉
* @param code       错误码
*/
public void onRoomDisconnect(final int errorCode);

/**
 * 有成员加入房间
 * @param user      新加入房间的用户信息
 */
public void onAddRemoter(LVUser user);

/**
 * 有成员离开房间
 * @param userId        退出房间用户的ID
 */
public void onDeleteRemoter(String userId);

/**
 * 用户被踢出房间
 * @param reason        被踢原因
 * @param roomId        房间ID
 */
public void onKickOff(int reason, String roomId);

// 房间重连成功通知，SDK 在网络断开和恢复时会自动进行重连，重连结果通过该回调通知 APP
public void onRoomReconnect();
```

### 5.4、回调接口或方法解析

* LVResultCallback2接口
  * 调用 loginRoom 方法登录房间之后会回调此接口的 onResult 方法，在此方法中可进行做推流处理，如果登录房间失败，也会返回对应的错误码。

* LVResultCallback1接口
  * 调用 logoutRoom 方法退出房间之后会回调此接口的 onResult 方法，代表退出房间。
  
* onRoomDisconnect方法
  * 如果网络不好，房间断开，SDK 内部会自动自动进行重连，90 秒如果重连失败就会触发该方法回调此方法。
  
* onAddRemoter方法
  * 当在直播间内，有新成员调用 startPublishing 方法，发起推流的时候，房间内其它人就会触发此回调方法，在此方法内可以播放新成员的流处理添加视图渲染。
  
* onDeleteRemoter
  * 房间内有人退出房间的时候，就会回调此方法，可以在此方法内处理删除房间内成员视图，停止播放流等处理。
  
* onRoomReconnect
  *  房间重连成功通知，SDK 在网络断开和恢复时会自动进行重连，重连结果通过该回调通知 APP。
   
* onKickOff
  * 当用户被踢出的时候，会回调此方法，告知被踢出和原因。