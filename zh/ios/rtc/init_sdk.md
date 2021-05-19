# 初始化

## <a name='1'></a>1、概述

集成 SDK 完成后，要想使用 SDK 的功能，需要先对 SDK 进行初始化 和 鉴权，然后才能继续使用

## <a name='2'></a>2、初始化步骤

### （1）申请 AppID Key

请在 [LinkV 开发者后台](http://dev.linkv.sg/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV)。

### （2）初始化 SDK

在调用其他 RTC API 前，需要调用 initSdk 方法，进行对 SDK 的一个初始化。

```objective-c
#import <LinkV/LinkV.h>

// 初始化 SDK
[LVRTCEngine initSdk];
```

### （3）鉴权 SDK

从  [LinkV 开发者后台](dev.linkv.sg) 申请 获取 AppID 与 AppSecret 后，对 SDK 进行鉴权。

```objective-c
// SDK 鉴权
// @param appId 开发者平台申请的 appId
// @param skStr  开发者平台申请的 秘钥
// @param userId 用户 ID
// @param completion 鉴权完成回调
[[LVRTCEngine sharedInstance] auth:[CMKeyCenter AppId]
                                    skStr:[CMKeyCenter Token]
                                userId:[LVRTCTool shareInstance].userId
                               completion:^(LVErrorCode code) {
        NSLog(@"[CMSDK-Demo] auth:%lu",(unsigned long)code);
}];
```

> userId 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

### 参数解析

* auth
  * 设置为从 [开发者平台](dev.linkv.sg) 申请的 appId
* skStr
  * 设置为从 [开发者平台](dev.linkv.sg) 申请的 app秘钥
* userId
  * 非必传参数，如果有当前登录的用户 id 可传当前登录的用户 id，如果没有可留空。
* completion
  * 如果鉴权失败，会抛出对应的错误码，可查看 [SDK 鉴权错误码](/?p=/zh/ios/rtc/ecode.md&k=WZsw8kGY)

> 鉴权成功后，即可进行后续操作，鉴权失败的话可查看对应错误码检查错误。

## <a name='3'></a>3、其它 API

### 设置使用国际版本

* 如果 app 是在海外环境，设置开启国际版本会加快速度（如果开启了国际版本，那么国际版本和国内版本不互通.）

* SDK 默认使用中国版本，国内用户不用调用。

```objective-c
// 设置是否使用国际版本
[LVRTCEngine setUseInternationalEnv:NO];
```

### 获取 SDK 版本号

* 获取 sdk 版本号，在调试的时候可查看 sdk 对应版本号。

```objective-c
// SDK 版本号
[LVRTCEngine version];

// SDK 内部版本号
[LVRTCEngine build_version];
```
