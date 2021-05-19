# Integrate the SDK

LinkV SDK provides two integration methods, manual integration and CocoaPods integration.
LinkV RTCEngine SDK supports iOS 9.0 and above. Xcode 9 or above is recommended.

## Integration

* Manual integration
* CocoaPods integration

## <a name='1'></a>1、Preparation

#### Please ensure that the development environment meets the following technical requirements:

* Apple Xcode 9.0 or above
* iOS 9.0 or above
* The iOS devices supporting audio and video functions

## <a name='2'></a>2、Import the project

### CocoaPods integration

> Before running the following steps, make sure that CocoaPods is installed. Please refer to [CocoaPods official website](https://cocoapods.org/)

Add the following dependencies in the project Podfile file, and then execute **pod install** to add LinkV's audio and video library to the project (if you can't find it, you canrun pod repo update to update the local index)

```objective-c
pod 'LinkV'

``` 

### Manual integration

> The dynamic library downloaded and integrated here is only supported by iOS 8.0 and above.

1. Download SDK

   * Please download the SDK from [LinkV RTC Engine](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq).

2. Import the configure SDK

   * After decompression, drag the SDK into the project and run it. Note that the way to add the library is **Embed & Sign** . 
   * In Xcode, select: Project TARGET -> General -> Frameworks, Libraries, and Enbedded Content, add LinkV.framework, and set Embed to **Embed & Sign** .

![](https://dl.linkv.io/doc/en/ios/rtc/images/iOS_import_RTC.png)

## <a name='3'></a>3、Set up the configuration

### Adding permissions

Copy the following code, paste it into info.plist, and add the permission description.

```xml
<key>NSCameraUsageDescription</key>
<string>LinkV requires camera permission to publish live video or co-streaming with the host. </string>
<key>NSMicrophoneUsageDescription</key>
<string>LinkV requires camera permission to publish live audio or co-streaming with the host.</string>
```

![](https://dl.linkv.io/doc/en/ios/rtc/images/iOS_Auth2.png)

### Disable App Transport Security (ATS)

> Since the SDK still needs to use the http as the domain name, therefore the ATS needs to be closed.

Copy the following codes and paste them into info.plist, and set NSAllowsArbitraryLoads to yes.

``` 
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```

![](https://dl.linkv.io/doc/en/ios/rtc/images/iOS_ATS2.png)

### Disable Bitcode

> Since the current SDK does not support bitcode, therefore you need to disable bitcode.

1. Select the target of the current Xcode project
2. Select Build Settings-Enable Bitcode and set it to **No**.

![](https://dl.linkv.io/doc/en/ios/rtc/images/iOS_bitcode.png)

## <a name='4'></a>4、Test the integration

Import the first LinkV file, and then run initSdk. If there is no problem with the operation, the integration is successful.

``` objc
#import <LinkV/LinkV.h>

* (void)viewDidLoad {

    [super viewDidLoad];
    
    // Initialization SDK
    [LVRTCEngine initSdk];
}
```
