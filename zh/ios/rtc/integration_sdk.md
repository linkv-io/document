# 集成 SDK

LinkV  SDK 提供有两种集成方式，手动集成和 CocoaPods 方式集成。 LinkV SDK 支持 iOS 9.0 或以上版本系统，Xcode 建议使用 Xcode 9.0 或以上版本。

## 集成方式

* 手动集成
* CocoaPods 集成

## <a name='1'></a>1、准备环境

#### 请确保开发环境满足以下技术要求：

- Xcode 9.0 或以上版本
- iOS 9.0 或以上版本
- 支持音视频功能的真机

## <a name='2'></a>2、导入工程

### CocoaPods集成

> 在执行以下步骤之前，请确保已安装 CocoaPods。 请参阅 [CocoaPods 官网](https://cocoapods.org/)

在工程 Podfile 文件中添加下列依赖，然后执行 **pod install** 即可添加 LinkV 的音视频库到工程中（如果搜索不到可以 pod repo update 更新下索引库）

```objective-c
pod 'LinkVRtcLib'
```

### 手动集成

> 此处下载集成的是动态库，iOS 8.0 及以上版本才支持。

1. 下载

   * 从  [LinkV RTC Engine](/?p=/zh/ios/rtc/download_sdk.md&k=LKdNguJq)  下载 SDK。
2. 导入并配置 SDK
   * 解压之后将 SDK 拖入工程中即可运行，注意设置库的添加方式为 **Embed&Sign** 方式。 
   * 在 Xcode 中，选择：项目 TARGET -> General -> Frameworks,Libraries,and Enbedded Content 中，添加 LinkV.framework，Embed 设置为 **Embed & Sign**。

![](https://dl.linkv.io/doc/zh/ios/rtc/images/iOS_import_RTC.png)

## <a name='3'></a>3、设置工程配置

### 添加权限

复制以下代码，粘贴到 info.plist 里面，添加权限（摄像头，麦克风） 描述。

```xml
<key>NSCameraUsageDescription</key>
<string>LinkV 需要使用摄像头权限，否则无法发布视频直播，无法与主持人视频连麦</string>
<key>NSMicrophoneUsageDescription</key>
<string>LinkV 需要使用麦克风权限，否则无法发布音频直播，无法与主持人音频连麦</string>
```

![](https://dl.linkv.io/doc/zh/ios/rtc/images/iOS_Auth2.png)

### 关闭 ATS

> 由于目前 SDK 还需要使用 http 域名，所以需要关闭 ATS。

复制以下代码，粘贴到 info.plist 里面，设置 NSAllowsArbitraryLoads 为 YES。

```
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```

![](https://dl.linkv.io/doc/zh/ios/rtc/images/iOS_ATS2.png)

### 关闭 bitcode

> 由于 SDK 目前没有支持 bitcode，所以需要关闭 bitcode

1. 选择当前 Xcode工程的 target
2. 选择Build Settings - Enable Bitcode 设置为 **No**

![](https://dl.linkv.io/doc/zh/ios/rtc/images/iOS_bitcode.png)

## <a name='4'></a>4、测试集成

导入 **LinkV.h** 头文件，然后 执行  **initSdk** ，运行如果没问题，那么代表集成成功。

```objc
#import <LinkV/LinkV.h>
- (void)viewDidLoad {
    [super viewDidLoad];
    
    // 初始SDK
    [LVRTCEngine initSdk];
}
```
