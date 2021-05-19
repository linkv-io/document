# Initialization

## <a name='1'></a>1、Overview

In order to activate the functions of the SDK, You need to initialize and authenticate the SDK after the SDK integration process is completed

## <a name='2'></a>2、Initialization Procedures

![](https://dl.linkv.io/doc/en/android/rtc/images/sdk_auth.png)

### （1）Apply for the AppID Key

Please apply for the appid and signature required for SDK authentication from the [LinkV developer console](http://dev.linkv.sg/) . Here is the [guide for obtaining the AppID and AppSercret](/?p=%252Fen%252Fopen%252Fquick_start.md&k=R5tULcvV) .

### （2）Initialize SDK

Before calling other RTC APIs, you need to use the initSdk method to initialize the SDK.

```java
import com.linkv.rtc.LVRTCEngine;

// 初始化 SDK
LVRTCEngine rtcEngine = LVRTCEngine.getInstance(MyApplication.instance);
rtcEngine.initSDK();
```

### （3）SDK Authentication

After obtaining the AppID and AppSecret from the [LinkV developer console](http://dev.linkv.sg/)  , the SDK is authenticated.

```java
/**
 * sdk authentication
 * @param appId     The developer platform applied appId
 * @param skStr     The developer platform applied secret key
 * @param userId    User ID
 * @param callback  Authentication result callback
 */
rtcEngine.auth(appId, skStr, userId, integer -> {
    if (integer != LVErrorCode.SUCCESS) {
        LogUtils.d(TAG, getString(R.string.error_code) + integer);
    }
});
```

### Parameter analysis

### Parameter analysis

* auth
  * Set as the appId from [developer platform](http://dev.linkv.io)
* skStr
  * Set as the app encryption key from [developer platform](http://dev.linkv.io)
* userId
  * This parameter is optional. If there is a currently logged-in user id please input the currently logged-in user id, if not leave it blank.
* callback
  * If the authentication fails, the corresponding error code will be thrown，Please see [SDK Authentication error code](/?p=/en/android/rtc/ecode.md&k=WZsw8kGY)

> If the authentication is successful, please follow-up operations. If the authentication fails, the corresponding error code can be checked to find out the reason for the errors.

## <a name='3'></a>3、Other APIs

### Configuration for the international version

* If the app is not used in China, please enable the international version which will speed up the connection efficiently. (if the international version is enabled, the international version and the Chinese version are not interconnected.)

* The SDK uses the Chinese version by default, and domestic users do not need to call it.

```java
// Set whether to use the international version
LVRTCEngine.setUseInternationalEnv(false);
```

### Get SDK version number

* Obtain the SDK version number, you can find the corresponding SDK version number when debugging.

```java
// SDK version number
LVRTCEngine.versionName();

// SDK Internal version number
LVRTCEngine.buildVersion();
```
