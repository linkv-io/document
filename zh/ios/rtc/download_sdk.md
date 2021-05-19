# 实时音频 / 视频直播  SDK

**更新时间：2020-06-09**

## <a name='1'></a>1、介绍

LinkV  实时音视频 基于 WebRTC 协议以及 LinkV 自研的音视频编解码技术，提供可靠的实时音视频服务。

## <a name='2'></a>2、服务端 SDK 下载

LinkV 提供 以下语言的SDK，请下载**最新**版本的tag

| 语言 | 版本 |  |
| --- | --- | ---     |
|Golang | >= 1.8 | [下载](https://github.com/linkv-io/go-sdk) |
| Python2 | >=2.7.9 | [下载](https://github.com/linkv-io/python2-sdk) |
| Python3 | 3.5｜3.6｜3.7｜3.8 | [下载](https://github.com/linkv-io/python-sdk) |
| PHP | 5.* ｜ 7.* | [下载](https://github.com/linkv-io/php-sdk) |
| Node | >=10.15.3 | [下载](https://github.com/linkv-io/node-sdk) |
| Dart | >=2.5.0 ｜ <3.0.0 |[下载](https://github.com/linkv-io/dart-sdk) |

> 现有服务端SDK中并没有您所使用的服务端语言 请参照 [API文档]() 进行编写对接
>

## <a name='3'></a>3、客户端SDK 下载

[LinkV SDK v1.0](https://dl.linkv.io/static/iOS/RTC/LinkV.zip)

## <a name='4'></a>4、示例 Demo

示例场景 Demo 主要分为互动直播场景，多人连麦场景，视频通话场景，和基础 SDK 场景。

[基础 SDK 演示](https://dl.linkv.io/static/iOS/RTC/BaseLinkVDemo-iOS.zip)

* 包含基本的推流，拉流，伴奏播放，外置音频推流等功能。
* 里面有最基本的代码演示，可供参考。
* 在集成 SDK 的时候可参考此 Demo 快速清晰的接入 SDK，了解 SDK。

[互动直播场景](https://dl.linkv.io/static/iOS/RTC/Group-Video-Live-iOS.zip)

* 互动直播场景用户分为主播和观众，主播可开启直播间，观众进行加入，主播可以自由发言，观众可以发起和主播连麦。

[多人连麦场景](https://dl.linkv.io/static/iOS/RTC/LinkV-GroupVideoCall-iOS.zip)

* 多人连麦场景适合于视频会议，多人语音等功场景，一个房间内可有多个用户进行连麦实时通话。

[视频通话场景](https://dl.linkv.io/static/iOS/RTC/LinkV-1to1-iOS.zip)

* 视频通话场景不区分主播和观众，相互的用户可以自由发言。

![](https://dl.linkv.io/doc/zh/ios/rtc/images/sdk_demo_ui.png)

