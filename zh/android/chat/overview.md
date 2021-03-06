# 一对一视频通话
StrangerChat SDK不仅包含有类似声网和Zego的RTC音视频推拉流及IM通讯能力，除此之外还封装了陌生人交友、视频聊天、网络聊天室等场景需要用到的一些api。例如呼叫、接听、连麦、送礼、礼物动效等常用功能。本文介绍如何使用StrangerChat SDK快速实现音视频通话。 
* 商务合作与技术交流请加QQ群：**1160896626**

## 1、示例项目

StrangerChat SDK在GitHub上提供开源的实时视频通话示例项目[StrangerChatAndroid](https://github.com/linkvxiaohong/StrangerChatAndroid)。在实现相关功能前，你可以下载并查看源码。

<img src="https://github.com/linkv-io/StrangerChat/blob/master/Snapshot/StrangerChat.gif?raw=true", width="375">


### Demo下载体验

[点我安装Demo或扫描下方二维码下载](https://www.pgyer.com/zDgs)

<img src="![](https://www.pgyer.com/app/qrcode/zDgs)", width="200" />

### 前提条件

*  Android 5.1或以上版本的设备
* 有效的AppId和AppKey，[获取 AppID 和 AppSecret 指引](http://dev.linkv.io/)

## <a name='2'></a>2、集成SDK

* 在工程的build.gradle文件添加如下内容：

  ```xml
  maven {
    url 'http://maven.linkv.fun/repository/liveme-android/'
    credentials {
        username = 'LivemesdkPublicUser'
        password = 'public'
    }
  }
  ```


<img src="https://dl.linkv.io/doc/zh/android/chat/images/image-maven-config.png", width="375">

* 在项目中的android/app/build.gradle文件添加社交SDK依赖，请尽量使用api方式引入依赖，方便使用进阶功能接口：
```xml
    api 'com.linkv.live:strangerchat:1.0.1'
```

  

## 3、设置工程配置

### 添加权限

打开项目中的android/app/src/main/AndroidManifest.xml文件，添加如下代码。

```java
// 需要使用麦克风权限，否则无法发布音频直播，无法与主持人音频连麦.
<uses-permission android:name="android.permission.RECORD_AUDIO" />

// 需要使用摄像头权限，否则无法发布视频直播，无法与主持人视频连麦.
<uses-permission android:name="android.permission.CAMERA" />
```

### 允许使用http协议

> 由于Android 9.0以上版本默认禁止使用http域名，但sdk还需要使用到http域名，故需要做一些配置以支持Android 9.0以上的版本使用http域名

在项目路径android/app/src/main/res/xml文件夹中创建文件network_security_config.xml，并添加如下代码：

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```

<img src="https://dl.linkv.io/doc/zh/android/chat/images/image-http-xml.png", width="375">


打开项目中的android/app/src/main/AndroidManifest.xml文件，在application标签中添加如下属性：
```xml
    android:networkSecurityConfig="@xml/network_security_config"
```
