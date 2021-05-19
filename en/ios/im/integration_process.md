# Integration

The SDK currently only supports manual integration, and support the CocoaPods integration in the future.

## <a name='1'></a>1、Development environment

* iOS 9.0 or later.
* Xcode 10.0 or above.

## <a name='2'></a>2、Integrated SDK

### 2.1 Download SDK

Download SDK from  [LVIMLib iOS](/?p=/zh/ios/im/download_demo.md&k=kzhMLAye) .

### 2.2 Add LVIMLib to the project

XcodeFile —> Add Files to “Your Project”, select LVIMLib.framework->add from the pop-up Panel. (Note: Select "Copy items if needed")

![img](https://dl.linkv.io/doc/en/ios/im/images/im_add_sdk.jpg)

![img](https://dl.linkv.io/doc/en/ios/im/images/im_add_sdk_1.jpg)

### 2.3 Add SDK dependency libraries

Xcode - Build Phases - Link Binary With Libraries - click + - Add Other - select the followings under the LVIMLib Framework

| name                |
| ------------------- |
| libcares.a          |
| libopencore-amrnb.a |
| libprotobuf-lite.a  |

![img](https://dl.linkv.io/doc/en/ios/im/images/dependent_1.jpg)

![img](https://dl.linkv.io/doc/en/ios/im/images/dependent_2.jpg)

### 2.4 Add the system dependency libraries

Xcode-Build Phases-Link Binary With Libraries-click the + sign- add the following system dependent libraries

| name            |
| --------------- |
| libsqlite3.tbd  |
| libresolv.9.tbd |
| libz.tbd        |
| libc++.tbd      |

![img](https://dl.linkv.io/doc/en/ios/im/images/dependent_3.jpg)

### 2.5 Disable bitcode

* The bitcode is not supported by LVIMLib SDK , you need to disable the bitcode from the project to use the SDK.

* Disabling the Bitcode: Target->Build Setting, and search for bitcode, Set the "Enable Bitcode", from Yes to No

![img](https://dl.linkv.io/doc/en/ios/im/images/im_bitcode.jpg)

### 2.6 Test whether the integration is successful

* Import the first files in the project #import <LVIMLib/LVIMLib.h> 
*  [[LVIMSDK sharedInstance] initWithAppId:@"" secret:@""] Compile and check whether the compilation is successful

![img](https://dl.linkv.io/doc/en/ios/im/images/im_incloud_status.jpg)
