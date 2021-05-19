# Integrate the SDK

###### LinkV RTCEngine SDK support Android 4.4 or above version system, AndroidStudio recommends to use 3.6 or above version, currently does not support emulator operation.

## <a name='1'></a>1、Prepare environment

## Integration method

- Android Studio 3.0 or above.
-A real Android device with an Android version of at least 4.4 and supporting audio and video.
-The Android device is connected to the Internet.

## <a name='1'></a>2、Import project

Currently RTCEngine SDK only supports integration by copying .jar and .so. The currently supported platform architectures include armeabi-v7, arm64-v8a, and the integration steps are as follows.

### 2.1、Manual integration

- Download SDK 
    - Please download SDK from [LinkV RTCEngine](http://www.liveme.com/download.sdk)  。
For historical version updates, please check: LinkV RTCEngineLib Android historical update log.

- Import configuration SDK

    * After downloading the latest SDK, unzip it.
    * Put the linkV.jar file into the libs folder of the project, and put the armeabi-v7a and arm64-v8a folders into the jniLibs folder.
    
    <img src="https://dl.linkv.io/doc/en/android/rtc/images/android_input_jar.png" width="100%"/>
* Add the jar package reference, open the app/build.gradle file in the project, and add the following code:
    ```java
    ...
    dependencies {
        ...
        implementation files('libs/linkv.jar')
    }
    ```
    <img src="https://dl.linkv.io/doc/en/android/rtc/images/android_import_jar.png" width="100%" />
    * Specify the platform type supported by ndk, open the app/build.gradle file in the project, and add the following code:：
    ```java
    ...
    ndk {
        abiFilters 'armeabi-v7a', 'arm64-v8a'
    }
    ```
    <img src="https://dl.linkv.io/doc/en/android/rtc/images/android_set_ndk.png" width="100%" />

## <a name='3'></a>3、Add permissions


Open the app/src/main/AndroidManifest.xml file in the project and add the following code.```xml
    <!--    Access to network connection may generate GPRS traffic-->
    <uses-permission android:name="android.permission.INTERNET" />
    <!--    Get network information status, such as whether the current network connection is valid-->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <!--    Get the current WiFi access status and WLAN hotspot information-->
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <!-- Allow access to the camera to take pictures-->
    <uses-permission android:name="android.permission.CAMERA" />
    <!--    Allow camera-->
    <uses-feature android:name="android.hardware.camera" />
    <!--    Allow use of the camera's auto focus function-->
    <uses-feature android:name="android.hardware.camera.autofocus" />
    <!--    Record sound via mobile phone or headset microphone-->
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <!--    Modify sound setting information-->
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```
<img src="https://dl.linkv.io/doc/en/android/rtc/images/android_add_permission.png" width="100%" />

> Please note: Because Android 6.0 requires dynamic application of permissions on some of the more important permissions, you cannot just declare permissions through the AndroidMainfest.xml file. Therefore, you need to refer to and execute the following code (requestPermissions is the method of Activity)

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

## <a name='4'></a>4、Support http domain name
Since Android 9.0 and above versions prohibit the use of http domain names by default, but SDK also needs to use http domain names, some configuration needs to be done to support Android 9.0 and above versions to use http domain names.

### 4.1、Create network configuration xml file

Create the file network_security_config.xml in the app/src/main/res/xml folder of the project path and add the following code:
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```
<img src="https://dl.linkv.io/doc/en/android/rtc/images/android_create_network_config.png" width="100%" />

### 4.2. Set the network configuration file in AndroidManifest.xml
Open the app/src/main/AndroidManifest.xml file in the project and add the following attributes to the application tag:
```java
...
android:networkSecurityConfig="@xml/network_security_config"
...
```
<img src="https://dl.linkv.io/doc/en/android/rtc/images/android_set_network_config.png" width="100%" />

## <a name='5'></a>5、Prevent obfuscated code


Open the app/proguard-rules.pro file in the project and add the following code:
```java
...
-keep class com.linkv.rtc.* { *; }
```
<img src="https://dl.linkv.io/doc/en/android/rtc/images/android_add_confuse.png" width="100%" />

## <a name='6'></a>6、Test integration

Import the package, and then execute initSdk to see if there is a problem:
```java
private void initSDK() {
    LVRTCEngine rtcEngine = LVRTCEngine.getInstance(MyApplication.instance);
    // initiation sdk
    rtcEngine.initSDK();
}
```

