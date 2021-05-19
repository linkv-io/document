# Live Streaming Across Rooms

## <a name='1'></a>1、Introduction

The function of co-hosting live streaming across rooms refers to the scenario where the streams of the host can be forwarded to multiple live streaming rooms at the same time, which implements the real-time interaction between the host and another host from another room. 

After the co-hosting live streaming across rooms is made, all the hosts will be able to see and hear each other, and the viewers/audience in the channels also can watch and hear all the hosts.

This function is often used in certain scenarios such as the Head to Head Live scenario and singing together in live broadcasting rooms, etc.

## <a name='2'></a>2、Description

#### Non-across stream situation

* Under non stream across situation，Viewers can only pull streams from individual studios，and the anchors can't talk to each other。

<img src="https://dl.linkv.io/doc/en/android/rtc/images/linkRoom1.png" width="iOS_Auth2" style="width:60%;" />

#### Live streaming across rooms

* The broadcaster 1 and the broadcaster 2 who started their own live streaming respectively, after the room is connected, the individual broadcasters from different rooms can see and talk to each other. The audience will be able to see all of the broadcasters in any one of the live broadcasting rooms.

<img src="https://dl.linkv.io/doc/en/android/rtc/images/linkRoom2.png" width="iOS_Auth2" style="width:60%;" />

## <a name='3'></a>3、Related API

### Start to Stream Across Rooms

* Call the linkRoom method to pull the streams from the other specific room to the original room.

> linkRoom will not trigger the callback method OnAddRemoter when someone joins in.

```java
/** 
 *  Between rooms PK（Inter-room microphone function）
 *  @param roomId Room ID
 */
mRtcEngine.linkRoom(roomId);
```

### Stop Streaming Across Rooms

* You can pass the room number when you cancel the connection，call unlinkRoom。

> unlinkRoom Won't trigger OnDeleteRemoter Callback when a member has left。

```java
/** 
 *  Cancel the function of connecting microphones across rooms
 *  @param roomId Room ID
 */
mRtcEngine.unlinkRoom(roomId);
```

## <a name='4'></a>4、Step

（1）host A starts a live streaming with room ID 1001

（2）host B starts a live streaming with room ID 1002

（3）host A call linkRom with room ID 1002(the room of host B)

（4）host B call linkRom with room ID 1001(the room of host A)

（5）hosts A and B built up the connection of across-rooms live streaming.

## <a name='5'></a>5、Demo

For the specific reference for the examples, you can view [interactive live Demo](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq) as the sample project

