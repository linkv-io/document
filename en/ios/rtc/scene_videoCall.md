# Video call

## <a name='1'></a>一、Scene introduction

The video call scenario is mainly applicable to the scenario of a two-person call. In the example code, the logic of preventing a third person from joining can be processed to realize a two-person video call.
## <a name='2'></a>二、Push stream implementation


（1）Initialization SDK

（2）Initialize the rendering view


（3）Start collecting local camera


（4）Login room

（5）Push stream


When a member pushed stream to video call in the room，render and play the stream of new members
。

## <a name='3'></a>Third、Pull stream implement

（1）Initialization SDK

（2）Login room

（3）Play host video stream。

（4）Carry out mic operation（after receiving message of the pulled stream, play call-in streamers's stream)
## <a name='4'></a>Fourth、Demo Demo


Refer to the usage example for details，Please see [Video call ](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq)Demo project

