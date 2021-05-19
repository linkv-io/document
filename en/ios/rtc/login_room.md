# The Livestream room Login

## <a name='1'></a>1、Introduction

After initializing the SDK, you need to join the room before starting the video call. The host need to create a Livestream room, and the audiences are free to join the room to watch the live broadcast and interact with the broadcasters.

## <a name='3'></a>3、Glossary

### Room/Host

* The room ID is unique. If the room ID is not in use, then the host can use that room ID to create a room and publish live streaming.

### Audience/Viewers

* If the room already exists, the user can input the room ID as an audience to join the certain room, and play the streaming to watch in that room.
* Audience will not be making video/voice calls when entered the room as default, But they will be able to initiate an invitation of the video call to interactwith with their broadcasters.

## <a name='4'></a>4、Procedures

### Log in to a Room

* - If a broadcaster has already started a live stream, the room will be logged in automatically.

```objective-c
// Join in the Audio-video room（Audio/video conference）
// @param userId user ID
// @param roomId Room ID
// @param isHost Is it the host
// @param isOnlyAudio IS it joined with audio mode only(the video streaming will not be activated)
// @param delegate delegate the room
[[LVRTCEngine sharedInstance] loginRoom:[LVRTCTool shareInstance].userId

                                 roomId:self.roomId
                                 isHost:self.isHost
                            isOnlyAudio:true
                               delegate:self];

``` 

* userId
  + The user id has to be globally unique, and the developer can associate the user id with the in-app account.
* roomId
  + ID of the room, if you want to create a different live broadcast room, you need to ensure that the roomID is globally unique, otherwise the user will log in to the same room, which means joining an existing room.
* isHost
  + If the host starts a new room, then isHost needs to set true.
  + If the audience enter an existing room, then isHost needs to set false.
* isOnlyAudio
  + isOnlyAudio can decide whether to join in with audio mode or video mode.
  + Host
    - On the end of the host, even the value of OnlyAudio is set to true, the video streaming is still published. 
  + Audience (this parameter only works for the audience)
    - If a audience enters the room with isOnlyAudio setting true, then only the audio stream will be published without video stream.
* delegate
  + We can pass the delegate object of LVRTCEngineDelegate. After loginRoom function is logged, all of the corresponding room events and status will be passed through the delegate object.

### Log out of a room 

* This API can be used when logging out of the room, to see if the exit was success will be returned by passing through the [error code of exiting the room](/?p=/zh/ios/rtc/ecode.md&k=WZsw8kGY) .

```objective-c
// logout the room
// @param completion Callback the result of logging out the room
[[LVRTCEngine sharedInstance] logoutRoom:^(LVErrorCode code) {
        NSLog(@"logoutRoom:%lu",(unsigned long)code);
}];
```

* Exiting the room will trigger the **OnDeleteRemoter** callback, the relevant process can be done during the callback.

``` objc
// Notification when someone exits
// @param uid The ID of the user who exited

* (void)OnDeleteRemoter:(NSString*)uid;

```

## <a name='5'></a>5、Events of a room

Calling the loginRoom method with LVRTCEngineDelegate delegate to receive corresponding callback events.

### Room event callbacks

```objective-c
// Callback of entering the room successully
// @param code The code that indicates the result of entering the room
// @param users the list of uusers will be activated when there is a user exists.

* (void)OnEnterRoomComplete:(LVErrorCode)code users:(nullable NSArray<LVUser*>*)users; 

// Exiting the room completed. the callback will be triggered when the users were using the method of logoutRoom or an abnormal logout was made, 

* (void)OnExitRoomComplete; 

// Notification of being disconnected，SDK will be reconnecting automatically when the network is erro ，the callback will be triggered if the reconnection was failed after 90 seconds.
// @param code erro code

* (void)OnRoomDisconnect:(LVErrorCode)code; 

// Notification when a new user is joined.
// @param users List of the users

* (void)OnAddRemoter:(NSArray<LVUser*>*)users; 

// Notification when someone left
// @param uid ID of the people who left

* (void)OnDeleteRemoter:(NSString*)uid; 

/// The user gets kicked out of the room
/// @param reason the reason being kicked
/// @param roomId Room ID

* (void)onKickOff:(NSInteger)reason roomId:(NSString *)roomId; 

// Notification when the room is reconnected，SDK will be reconnected automatically when being disconnnected and restored，The result of reconnection will be notified on the app through this callback

* (void)OnRoomReconnected; 

```

### Method parsing

* OnEnterRoomComplete
  + The method will be called after calling the loginRoom method. If the room login success, the stream publish can be performed. If the room login fails, the corresponding error code will also be returned.
* OnExitRoomComplete
  + After calling the logoutRoom method, the OnExitRoomComplete callback method will be triggered, which means that the room exit is successful.
* OnRoomDisconnect
  + If the network is not stable and the room is disconnected, the SDK will try to reconnect automatically. If the reconnection still fails after 90 seconds, this method will be triggered to call back.
* OnAddRemoter
  + When a new member starts to publish a stream in the room, other people in the room will trigger this callback method. In this method, the new member's stream can be played and rendered to the screen.
* OnDeleteRemoter
  + When someone exits the room, this method will be called back. This method can be used to delete the view of the members in the room, and stop playing the stream etc.
* OnRoomReconnected
  + When the network is disconnected and restored, the SDK will try to reconnect automatically. When the room is reconnected successfully, and the result will be notified on the app through this callback method.
* onKickOff
  + When the user is kicked out, this method will call back to notify the user who is kicked out and the reasons for it.
