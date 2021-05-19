# 下载SDK

**更新时间：2020-08-19**

## <a name='1'></a>1、客户端 SDK下载

前往 [LiveMeSDK](https://dl.linkv.io/static/iOS/LiveMe/LiveMeSDK.zip) 下载最新LiveMeSDK, 然后解压，压缩包内包含

* LiveMeSDK.framework
* YYKit.framework
* ZegoLiveRoom.framework
* lmsdk.bundle
* copyResource_lite.sh

![](https://dl.linkv.io/doc/zh/ios/live/images/linkv_sdk.png)

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

## <a name='3'></a>3、示例工程下载

LiveMeSDK提供示例项目，请前往  [LiveMeSDKSample](https://dl.linkv.io/static/iOS/LiveMe/SampleProject.zip )  下载。在实现相关功能前，你可以下载并查看源代码，这对于您接入和使用本SDK有较大帮助。示例代码中包含，登录、获取直播列表、开播功能。

![demo_sample](https://dl.linkv.io/doc/zh/ios/live/images/demo_sample.jpg)


## <a name='5'></a>4、快速登录方法

为了方便快捷的体验SDK功能，和演示登录的流程，示例工程中提供了快速登录的bindingTokenWithUid方法，详细使用方法在示例工程的LoginVC.m文件中

```
[[LiveMeSDK sharedInstance] bindingTokenWithUid:uid userName:uname compelet:^(NSString *originId, NSString *uid, NSString *token) {
    if (originId && uid && token) {
        [MBProgressHUD showMsg:@"登录成功"];
    }
    [[LiveMeSDK sharedInstance] onLoginSuccessWithOriginUid:originId uid:uid token:token];
}];
```

> 示例代码中提供了SDK鉴权需要的测试appid和secret，不可以在正式环境中使用。示例代码中的所有功能需要在登录完成之后才能正常使用
>

