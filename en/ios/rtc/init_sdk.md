# Initialization

## <a name='1'></a>1、Overview

In order to activate the functions of the SDK, You need to initialize and authenticate the SDK after the SDK integration process is completed


### （1）Apply for the AppID Key

Please apply for the appid and signature required for SDK authentication from the [LinkV developer console](http://dev.linkv.sg/) . Here is the [guide for obtaining the AppID and AppSercret](/?p=%252Fen%252Fopen%252Fquick_start.md&k=R5tULcvV) .

### （2）Initialize SDK

Before calling other RTC APIs, you need to use the initSdk method to initialize the SDK.

```objective-c
#import <LinkV/LinkV.h>

// Initialize the SDK
[LVRTCEngine initSdk]; 

``` 

### （3）SDK Authentication

After obtaining the AppID and AppSecret from the [LinkV developer console](http://dev.linkv.sg/)  , the SDK is authenticated.

```objective-c
// SDK Authenticatin
// @param appId appId from the developer platform
// @param skStr  The encrytion key from developer platform
// @param userId User ID
// @param completion the authentication finished the calling
[[LVRTCEngine sharedInstance] auth:[CMKeyCenter AppId]
                                    skStr:[CMKeyCenter Token]
                                userId:[LVRTCTool shareInstance].userId
                               completion:^(LVErrorCode code) {
        NSLog(@"[CMSDK-Demo] auth:%lu",(unsigned long)code);
}];
```

### Parameter analysis

* auth
  * Set as the appId from [developer platform](http://dev.linkv.sg)
* skStr
  * Set as the app encryption key from [developer platform](http://dev.linkv.sg)
* userId
  * This parameter is optional. If there is a currently logged-in user id please input the currently logged-in user id, if not leave it blank.
* completion
  * If the authentication was failed, the corresponding error code will be thrown, you can find it in the [SDK authentication error code](/?p=/en/ios/rtc/ecode.md&k=WZsw8kGY)

> If the authentication is successful, please follow-up operations. If the authentication fails, the corresponding error code can be checked to find out the reason for the errors.

## <a name='3'></a>3、Other APIs

### Configuration for the international version

* If the app is not used in China, please enable the international version which will speed up the connection efficiently. (if the international version is enabled, the international version and the Chinese version are not interconnected.)

* The SDK uses the Chinese version by default, and domestic users do not need to call it.

```objective-c
// Set to enable the international version
[LVRTCEngine setUseInternationalEnv: NO]; 

``` 

### Get SDK version number

* Obtain the SDK version number, you can find the corresponding SDK version number when debugging.

```objective-c
// SDK Version number
[LVRTCEngine version];

// SDK Internal Version
[LVRTCEngine build_version];
```
