# 客户端集成

**更新时间：2020-08-19**

LiveMe 社交娱乐SDK目前仅支持手动方式集成，未来会开放CocoaPods方式集成，SDK支持iOS 9.0或以上版本系统，Xcode建议使用 Xcode 10.0或以上版本

## <a name='1'></a>1、 环境准备

##### 请确保满足以下开发环境：

- Xcode 10.0 或以上版本。
- iOS 9.0 或更高版本。

## <a name='2'></a>2、 导入工程

### <a name='2.1'></a>2.1 下载SDK

请从 [LiveMeSDK下载地址](https://dl.linkv.io/static/iOS/LiveMe/LiveMeSDK.zip)下载SDK，SDK包含如下文件。

![](https://dl.linkv.io/doc/zh/ios/live/images/linkv_sdk.png)

### <a name='2.2'></a>2.2 导入文件和运行脚本

将 Imsdk.bundle 和 copyresource _ lite.sh 放入与工作区文件相同的路径中。

![step_1](https://dl.linkv.io/doc/zh/ios/live/images/step_1.jpg)

### <a name='2.3'></a>2.3 导入Framework

将LiveMeSDK.framework、YYKit.framework、ZegoLiveRoom.framework拖入工程。

![step_2](https://dl.linkv.io/doc/zh/ios/live/images/step_2.jpg)

## <a name='3'></a>3、设置工程配置

### <a name='3.1'></a>3.1 设置Build Phases

 将如下framework添加到Build Phases ->  Link Binary With Libraries 下。

​	![step_3](https://dl.linkv.io/doc/zh/ios/live/images/step_3.jpg)

### <a name='3.2'></a>3.2 设置Libraries Embedded

将如下framework添加到 General -> Frameworks,Libraries,and Embedded Content下,注意framework的Embed方式为 **Embed&Sign**。

​	![step_4](https://dl.linkv.io/doc/zh/ios/live/images/step_4.jpg)

### <a name='3.3'></a>3.3 添加运行脚本

在构建阶段，添加新的运行脚本，并运行 step1中的CopyResource_lite.sh。

```
//添加如下运行脚本：
sh ${SRCROOT}/copyResource_lite.sh
```

​	![step_5](https://dl.linkv.io/doc/zh/ios/live/images/step_5.jpg)

### <a name='3.4'></a>3.4 关闭bitcode

> 由于 SDK 目前没有支持 bitcode，所以需要关闭 bitcode

TARGETS > Build Settings 搜索bitcode，将Enable Bitcode设置为NO

​	![bitcode](https://dl.linkv.io/doc/zh/ios/live/images/bitcode.jpg)

## <a name='4'></a>4、修改info.plist

> 为方便修改请通过Source Code显示info.plist数据内容

选择项目 -> Info.plist -> 右键点击Info.plist -> Open As -> Source Code

![plist](https://dl.linkv.io/doc/zh/ios/live/images/plist.jpg)

### <a name='4.1'></a>4.1 权限添加

1. 复制以下代码

```
   <key>NSCameraUsageDescription</key>
   <string>LiveMeSDK 需要使用摄像头权限，否则无法发布视频直播</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>LiveMeSDK 需要使用麦克风权限，否则无法发布音频直播</string>
```

2. 粘贴到 info.plist 里面，添加权限描述，如下图：

   ![step_6](https://dl.linkv.io/doc/zh/ios/live/images/step_6.jpg)

### <a name='4.1'></a>4.2 关闭 ATS

> 由于目前 SDK 还需要使用 http 域名，所以需要关闭 ATS。

1. 复制以下代码

```
   <key>NSAppTransportSecurity</key>
   <dict>
   	<key>NSAllowsArbitraryLoads</key>
   	<true/>
   </dict>
```

2. 粘贴到 info.plist 里面，如下图：

   ![step_7](https://dl.linkv.io/doc/zh/ios/live/images/step_7.png)

### 

