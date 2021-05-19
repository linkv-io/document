# The Livestream room Login

## <a name='1'></a>1、Introduction

After initializing the SDK, you need to join the room before starting the video call. The host need to create a Livestream room, and the audiences are free to join the room to watch the live broadcast and interact with the broadcasters.

## <a name='2'></a>2、Operation procedures

![](https://dl.linkv.io/doc/en/android/rtc/images/video_time.png)

## <a name='3'></a>3、Glossary

### Room/Host

* The room ID is unique. If the room ID is not in use, then the host can use that room ID to create a room and publish live streaming.

### Audience/Viewers

* If the room already exists, the user can input the room ID as an audience to join the certain room, and play the streaming to watch in that room.
* Audience will not be making video/voice calls when entered the room as default, But they will be able to initiate an invitation of the video call to interactwith with their broadcasters.

## <a name='4'></a>4、Procedures

### Log in to a Room

* - If a broadcaster has already started a live stream, the room will be logged in automatically.

```java
/**
 *Join the audio and video room (audio and video conference)
 * @param roomId room ID
 * @param userId user ID
 * @param isHost is the host
 * @param isOnlyAudio Whether to join in audio mode, if join in audio mode, there is no video stream
 * @param callback Room callback monitoring
 */
mRtcEngine.loginRoom(roomId, userId, isHost, isOnlyAudio, (code, cmUsers) -> {
    if (code == LVErrorCode.SUCCESS) {
        // Landed successfully
    } else {
        // Login failed
    }
});
```

* userId
  + The user id has to be globally unique, and the developer can associate the user id with the in-app account.
* roomId
  + ID of the room, if you want to create a different live broadcast room, you need to ensure that the roomID is globally unique, otherwise the user will log in to the same room, which means joining an existing room.
* isHost
  + If the host starts a new room, then isHost needs to set true.
  + If the audience enter an existing room, then isHost needs to set false.
* isOnlyAudio
  * isOnlyAudio can decide whether to join in with audio mode or video mode.
  * Host
    * On the end of the host, even the value of OnlyAudio is set to true, the video streaming is still published. 
  * Audience (this parameter only works for the audience)
    - If a audience enters the room with isOnlyAudio setting true, then only the audio stream will be published without video stream.
* callback
* An instantiated object of type LVResultCallback2 can be passed. After loginRoom logs in to the room, all corresponding room event states will be passed through the callback object.

> userId format requirements: string type, length does not exceed 32, only allowed to contain underscore _
>
> roomId format requirements: string type, length does not exceed 32, only allowed to contain underscore _ 
>

### Log out of a room 

* This API can be used when logging out of the room, to see if the exit was success will be returned by passing through the [error code of exiting the room](/?p=/zh/ios/rtc/ecode.md&k=WZsw8kGY) .

```java
/**
* Logout room
* @param   callback callback leave room result
*/
mRtcEngine.logoutRoom(callback);
```

* Exiting the room triggers a **OnDeleteRemoter** proxy callback in which processing can be done.

```java
/**
* There was a notice that the members were leaving
* @param callback   Left user ID
*/
public void onDeleteRemoter(String userId);
```

## <a name='5'></a>5、Events of a room

Calling the loginRoom method with LVRTCEngineDelegate delegate to receive corresponding callback events.

An LVResultCallback2 object is set as a listener through the loginRoom method. The LVResultCallback2 object will call back the corresponding state after logging in the room。

```java
/**
* Callback to join the room
* @param code       join room status code

* @param users      User list, if there are users in the room, the list will take effect automatically
*/
public interface LVResultCallback2<Integer, ArrayList<LVUser>>> {
    void onResult(Integer code, ArrayList<LVUser>> users);
}
```

### 5.2、Log out of the room to monitor

Set an object of type LVResultCallback1 as a listener through the logoutRoom method, and the LVResultCallback1 object will call back the corresponding state after logging out of the room.

```java
/**
* Callback for exiting the room
* @param code       Exit room status code
*/
public interface LVResultCallback1<Integer> {
    void onResult(Integer code);
}
```

### 5.3、Other room monitoring、

Set an object of type LVRTCCallback as a monitor through the setLiveRoomCallback method. The LVRTCCallback object will monitor the relevant state of the room and call back the corresponding method.

```java
/**
* When the room is disconnected, the SDK will automatically reconnect when the network is abnormal, and the method will be triggered if the reconnection fails within 90 seconds.
* @param code       Error code
*/
public void onRoomDisconnect(final int errorCode);

/**
 * A member joins the room
 * @param user      User information newly added to the room
 */
public void onAddRemoter(LVUser user);

/**
 * A member leaves the room
 * @param userId        ID of the user who left the room
 */
public void onDeleteRemoter(String userId);

/**
 * User is kicked out of the room
 * @param reason        Reason for being kicked
 * @param roomId        Room ID
 */
public void onKickOff(int reason, String roomId);

// Notification of successful room reconnection，SDK It will automatically reconnect when the network is disconnected and restored, and the result of the reconnection will be notified through this callback APP
public void onRoomReconnect();
```

### Method parsing

* LVResultCallback2 interface 
* After calling the loginRoom method to log in to the room, the onResult method of this interface will be called back. In this method, push streaming can be performed. If the login to the room fails, the corresponding error code will also be returned.

* LVResultCallback1 interface
* After calling the logoutRoom method to exit the room, the onResult method of this interface will be called back, which means exiting the room.  
* onRoomDisconnect method
  + If the network is not stable and the room is disconnected, the SDK will try to reconnect automatically. If the reconnection still fails after 90 seconds, this method will be triggered to call back.
  
* onAddRemoter method
  + When a new member starts to publish a stream in the room, other people in the room will trigger this callback method. In this method, the new member's stream can be played and rendered to the screen.
  
* onDeleteRemoter
  + When someone exits the room, this method will be called back. This method can be used to delete the view of the members in the room, and stop playing the stream etc.
  
* onRoomReconnect
  + When the network is disconnected and restored, the SDK will try to reconnect automatically. When the room is reconnected successfully, and the result will be notified on the app through this callback method.
   
* onKickOff
  + When the user is kicked out, this method will call back to notify the user who is kicked out and the reasons for it.
