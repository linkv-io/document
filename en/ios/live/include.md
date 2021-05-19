# Quick Start (Integration)

**Update date：2020-08-27**

The LiveMe social entertainment SDK currently only supports manual integration. And the CocoaPods integration will be supported in the future. 

The SDK supports iOS 9.0 or above. Xcode recommends using Xcode 10.0 or above

## <a name='1'></a>1、 Development Environment Preparation

##### Please ensure that the development environment meets the following technical requirements:：

* Xcode 10.0 or above.
* iOS 9.0 or higher.

## <a name='2'></a>2、 Import the SDK

### 2.1 Download the SDK

Please download the SDK from the [LinkVSDK download address](https://dl.linkv.io/static/iOS/LiveMe/LiveMeSDK.zip) The SDK contains the following files.

![](https://dl.linkv.io/doc/en/ios/live/images/linkv_sdk.png)

### 2.2 Import files and run scripts

Put Imsdk.bundle and copyresource _ lite.sh in the same path as the workspace file.

![step_1](https://dl.linkv.io/doc/en/ios/live/images/step_1.jpg)

### 2.3 Import The Framework

Drag LiveMeSDK.framework, YYKit.framework, ZegoLiveRoom.framework into the project

![step_2](https://dl.linkv.io/doc/en/ios/live/images/step_2.jpg)

## <a name='3'></a>3、Set up the project configuration

### 3.1 Set up the Build phases

Add the following framework to Build Phases -> Link Binary With Libraries

![step_3](https://dl.linkv.io/doc/en/ios/live/images/step_3.jpg)

### 3.2 Set up the Libraries Embedded

Add the following framework to General -> Frameworks, Libraries, and Embedded Content. Note that the Embed method of the framework is **Embed&Sign**.

![step_4](https://dl.linkv.io/doc/en/ios/live/images/step_4.jpg)

### 3.3 Add the runscript

In the build phase, add a new runscript phase and run CopyResource_lite.sh in step1

``` 
//add the following runscript：
sh ${SRCROOT}/copyResource_lite.sh
```

​![step_5](https://dl.linkv.io/doc/en/ios/live/images/step_5.jpg)

### 3.4 Disable the bitcode

> Since the current SDK does not support bitcode, therefore you need to disable bitcode.

TARGETS> Build Settings Search bitcode, set the Enable Bitcode as NO

​![bitcode](https://dl.linkv.io/doc/en/ios/live/images/bitcode.jpg)

## <a name='4'></a>4、Modify the info.plist

> Please open the content of info.plist data as Source Code for the easier modification.

Select the project -> Info.plist -> right click on Info.plist -> Open As -> Source Code

![plist](https://dl.linkv.io/doc/en/ios/live/images/plist.jpg)

### 4.1 Add the permissions

1. Select the project -> Info.plist -> right click on Info.plist -> Open As -> Source Code

2. Copy the following code
``` 
   <key>NSCameraUsageDescription</key>
   <string>LiveMeSDK  permission needed to access the camera, otherwise can not broadcast the live video</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>LiveMeSDK permission needed to access the microphone, otherwise can not broadcast the audio broadcast</string>
```

3. Paste into info.plist, add the permission description, as shown below:

![step_6](https://dl.linkv.io/doc/en/ios/live/images/step_6.jpg)

### 4.2 Disable the ATS

> Since the SDK still needs to use the HTTP domain name, therefore the ATS needs to be disabled.

1. Copy the following codes

```
   <key>NSAppTransportSecurity</key>
   <dict>
   	<key>NSAllowsArbitraryLoads</key>
   	<true/>
   </dict>
```

2. 2. Paste it into info.plist, as shown below:

![step_7](https://dl.linkv.io/doc/en/ios/live/images/step_7.png)

### 

