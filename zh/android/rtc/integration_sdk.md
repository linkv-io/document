# 快速开始

###### LinkV RTCEngine SDK 支持 Android 4.4 或以上版本系统，AndroidStudio 建议使用 3.6 或以上版本，目前暂不支持模拟器运行。

## <a name='1'></a>1、准备环境

##### 请确保开发环境满足以下技术要求：

- Android Studio 3.0 或以上版本。
- Android 版本不低于 4.4 且支持音视频的 Android 真机。
- Android 设备已经连接到 Internet。

## <a name='1'></a>2、导入工程
目前 RTCEngine SDK 仅支持通过拷贝.jar和.so的方式集成，目前支持的平台架构包括：armeabi-v7、arm64-v8a，集成步骤如下。

### 2.1、手动集成

- 下载 SDK 
    - 请从  [LinkV RTCEngine](http://www.liveme.com/download.sdk)  下载 SDK。
历史版本更新，请查看：LinkV RTCEngineLib Android 历史更新日志。

- 导入配置SDK

    * 下载完最新SDK后进行解压。
    * 将linkV.jar文件放入到项目的libs文件夹中，armeabi-v7a和arm64-v8a文件夹放入到jniLibs文件夹中。
    
    <img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_input_jar.png" width="100%"/>
    * 添加jar包引用，打开项目中的app/build.gradle文件,添加如下代码：
    ```java
    ...
    dependencies {
        ...
        implementation files('libs/linkv.jar')
    }
    ```
    <img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_import_jar.png" width="100%" />
    * 指定ndk支持的平台类型，打开项目中的app/build.gradle文件,添加如下代码：
    ```java
    ...
    ndk {
        abiFilters 'armeabi-v7a', 'arm64-v8a'
    }
    ```
    <img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_set_ndk.png" width="100%" />

## <a name='3'></a>3、添加权限

打开项目中的app/src/main/AndroidManifest.xml文件，添加如下代码。
```xml
    <!--    访问网络连接，可能产生GPRS流量-->
    <uses-permission android:name="android.permission.INTERNET" />
    <!--    获取网络信息状态，如当前的网络连接是否有效-->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!--    获取当前WiFi接入的状态以及WLAN热点的信息-->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <!-- 允许访问摄像头进行拍照-->
    <uses-permission android:name="android.permission.CAMERA" />
    <!--    允许使用相机-->
    <uses-feature android:name="android.hardware.camera" />
    <!--    允许使用相机的自动对焦功能-->
    <uses-feature android:name="android.hardware.camera.autofocus" />
    <!--    录制声音通过手机或耳机的麦克-->
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <!--    修改声音设置信息-->
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```
<img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_add_permission.png" width="100%" />

> 请注意：因为 Android 6.0 在一些比较重要的权限上要求必须动态申请权限，不能只通过 AndroidMainfest.xml 文件声明权限。因此还需要参考执行如下代码（requestPermissions 是 Activity 的方法）

```java
String[] permissionNeeded = {
        "android.permission.CAMERA",
        "android.permission.RECORD_AUDIO"};

if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
    if (ContextCompat.checkSelfPermission(this, "android.permission.CAMERA") != PackageManager.PERMISSION_GRANTED ||
        ContextCompat.checkSelfPermission(this, "android.permission.RECORD_AUDIO") != PackageManager.PERMISSION_GRANTED) {
        requestPermissions(permissionNeeded, 101);
    }
}
```

## <a name='4'></a>4、支持http域名
由于Android 9.0以上版本默认禁止使用http域名，但sdk还需要使用到http域名，故需要做一些配置以支持Android 9.0以上的版本使用http域名。

### 4.1、创建网络配置xml文件
在项目路径app/src/main/res/xml文件夹中创建文件network_security_config.xml，并添加如下代码：
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```
<img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_create_network_config.png" width="100%" />

### 4.2、在AndroidManifest.xml中设置网络配置文件
打开项目中的app/src/main/AndroidManifest.xml文件，在application标签中添加如下属性：
```java
...
android:networkSecurityConfig="@xml/network_security_config"
...
```
<img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_set_network_config.png" width="100%" />

## <a name='5'></a>5、防止混淆代码

打开项目中的app/proguard-rules.pro文件，添加如下代码：
```java
...
-keep class com.linkv.rtc.* { *; }
```
<img src="https://dl.linkv.io/doc/zh/android/rtc/images/android_add_confuse.png" width="100%" />

## <a name='6'></a>6、测试集成
导入包，然后执行initSdk，看是否有问题：
```java
private void initSDK() {
    LVRTCEngine rtcEngine = LVRTCEngine.getInstance(MyApplication.instance);
    // 初始化sdk
    rtcEngine.initSDK();
}
```

