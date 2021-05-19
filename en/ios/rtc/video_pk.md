# Live Streaming Across Rooms

## <a name='1'></a>1、Introduction

The function of co-hosting live streaming across rooms refers to the scenario where the streams of the host can be forwarded to multiple live streaming rooms at the same time, which implements the real-time interaction between the host and another host from another room. 

After the co-hosting live streaming across rooms is made, all the hosts will be able to see and hear each other, and the viewers/audience in the channels also can watch and hear all the hosts.

This function is often used in certain scenarios such as the Head to Head Live scenario and singing together in live broadcasting rooms, etc.

## <a name='2'></a>2、Description

#### Live streaming in separate room

* In the case of separate rooms, the audience/viewers will only play to the streams of the individual live streaming, and the broadcasters can not talk to each others.

<img src="https://dl.linkv.io/doc/en/ios/rtc/images/linkRoom1.png" width="iOS_Auth2" style="width:60%; " />

#### Live streaming across rooms

* The broadcaster 1 and the broadcaster 2 who started their own live streaming respectively, after the room is connected, the individual broadcasters from different rooms can see and talk to each other. The audience will be able to see all of the broadcasters in any one of the live broadcasting rooms.

<img src="https://dl.linkv.io/doc/en/ios/rtc/images/linkRoom2.png" width="iOS_Auth2" style="width:60%; " />

## <a name='3'></a>3、API

### Start to Stream Across Rooms

* Call the linkRoom method to pull the streams from the other specific room to the original room.

> linkRoom will not trigger the callback method OnAddRemoter when someone joins in.

``` objc
//The Head-to-Head mode（Live streaming across rooms function） 
//@param roomId Room ID
[[LVRTCEngine sharedInstance] linkRoom:@""];
```

### Stop Streaming Across Rooms

* Call the unlinkRoom method with Room ID to stop streaming across rooms.

> unlinkRoom will not trigger the callback method OnDEleteRemoter when someone leaves.

``` objc
// stop streaming across rooms
// @param roomId RoomID
[[LVRTCEngine sharedInstance] unlinkRoom:@""];
```

## <a name='4'></a>4、Step

（1）host A starts a live streaming with room ID 1001

（2）host B starts a live streaming with room ID 1002

（3）host A call linkRom with room ID 1002(the room of host B)

（4）host B call linkRom with room ID 1001(the room of host A)

（5）hosts A and B built up the connection of across-rooms live streaming.

## <a name='5'></a>5、Demo

For the specific reference for the examples, you can view [interactive live Demo](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq) as the sample project
