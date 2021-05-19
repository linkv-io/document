# 初始化

## <a name='1'></a>1、概述

集成 SDK 完成后，要想使用 SDK 的功能，需要先对 SDK 进行初始化 和 鉴权，然后才能继续使用

## <a name='2'></a>2、初始化步骤

###  （1）申请 AppID Key

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV)。

### （2）初始化 SDK

在调用其他 RTC API 前，需要调用 initSdk 方法，进行对 SDK 的一个初始化。

```java
import com.linkv.rtc.LVRTCEngine;

// 初始化 SDK
LVRTCEngine rtcEngine = LVRTCEngine.getInstance(MyApplication.instance);
rtcEngine.initSDK();
```

### （3）鉴权 SDK

从  [LinkV 开发者后台]() 申请 获取 AppID 与 AppSecret 后，对 SDK 进行鉴权。

```java
/**
 * sdk鉴权
 * @param appId     开发者平台申请的 appId
 * @param skStr     开发者平台申请的 秘钥
 * @param userId    用户ID
 * @param callback  鉴权结果回调
 */
rtcEngine.auth(appId, skStr, userId, integer -> {
    if (integer != LVErrorCode.SUCCESS) {
        LogUtils.d(TAG, getString(R.string.error_code) + integer);
    }
});
```

> userId 格式要求：字符串类型，长度不超过32，仅允许包含下横线 _ 
>

### 参数解析

* auth
  * 设置为从 [开发者平台](http://dev.linkv.io/) 申请的 appId
* skStr
  * 设置为从 [开发者平台](http://dev.linkv.io/) 申请的 app秘钥
* userId
  * 非必传参数，如果有当前登录的用户 id 可传当前登录的用户 id，如果没有可留空。
* callback
  * 如果鉴权失败，会抛出对应的错误码，可查看 [SDK 鉴权错误码](/?p=/zh/android/rtc/ecode.md&k=WZsw8kGY)

> 鉴权成功后，即可进行后续操作，鉴权失败的话可查看对应错误码检查错误。

## <a name='3'></a>3、其它 API

### 设置使用国际版本

* 如果 app 是在海外环境，设置开启国际版本会加快速度（如果开启了国际版本，那么国际版本和国内版本不互通.）

* SDK 默认使用中国版本，国内用户不用调用。

```java
// 设置是否使用国际版本
LVRTCEngine.setUseInternationalEnv(false);
```

### 获取 SDK 版本号

* 获取 sdk 版本号，在调试的时候可查看 sdk 对应版本号。

```java
// SDK 版本号
LVRTCEngine.versionName();

// SDK 内部版本号
LVRTCEngine.buildVersion();
```
