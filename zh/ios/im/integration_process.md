# 集成

SDK 目前仅支持手动集成，后期会支持 CocoaPods 方式集成。

## <a name='1'></a>1、开发环境

* iOS 9.0 或更高版本。
* Xcode 10.0 或以上版本。

## <a name='2'></a>2、集成SDK

## Cocoapods 方式集成

\> *在执行以下步骤之前，请确保已安装 CocoaPods。 请参阅* [*CocoaPods 官网*](https://cocoapods.org/)

在工程 Podfile 文件中添加下列依赖，然后执行 `pod install` 即可添加 LinkV 的音视频库到工程中（如果搜索不到可以 pod repo update 更新下索引库）

```
pod 'LinkVIMLib'
```

## 手动集成

### 2.1 下载SDK

从 [LVIMLib iOS](/?p=/zh/ios/im/download_demo.md&k=kzhMLAye) 下载 SDK

### 2.2 添加 LVIMLib 到工程中

XcodeFile —> Add Files to "Your Project"，在弹出Panel选中所LVIMLib.framework－>Add。（注：选中“Copy items if needed”）

![img](https://dl.linkv.io/doc/zh/ios/im/images/im_add_sdk.jpg)

![img](https://dl.linkv.io/doc/zh/ios/im/images/im_add_sdk_1.jpg)

### 2.3 添加SDK依赖库

Xcode - Build Phases - Link Binary With Libraries - +号 - Add Other - 选择LVIMLib Framework 下的 

| 名称                |
| ------------------- |
| libcares.a          |
| libopencore-amrnb.a |
| libprotobuf-lite.a  |

![img](https://dl.linkv.io/doc/zh/ios/im/images/dependent_1.jpg)

![img](https://dl.linkv.io/doc/zh/ios/im/images/dependent_2.jpg)

### 2.4 添加系统依赖库

Xcode - Build Phases - Link Binary With Libraries - +号 - 选择添加以下系统依赖库

| 名称            |
| --------------- |
| libsqlite3.tbd  |
| libresolv.9.tbd |
| libz.tbd        |
| libc++.tbd      |

![img](https://dl.linkv.io/doc/zh/ios/im/images/dependent_3.jpg)

### 2.5 关闭bitcode

- LVIMLib SDK 不支持bitcode，使用此SDK，需要关闭项目bitcode

- 关闭方法：Target->Build Setting,  搜索 bitcode，”Enable Bitcode” 该Yes为No

![img](https://dl.linkv.io/doc/zh/ios/im/images/im_bitcode.jpg)

### 2.6 测试是否集成成功

- 项目中导入头文件 #import <LVIMLib/LVIMLib.h> 
-  [[LVIMSDK sharedInstance] initWithAppId:@"" secret:@""] 进行编译，查看是否编译成功

![img](https://dl.linkv.io/doc/zh/ios/im/images/im_incloud_status.jpg)