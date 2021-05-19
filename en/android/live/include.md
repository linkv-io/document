# User end integration

**Update date：2020-08-27**

LiveMe the social entertainment SDK currently supports Maven integration. The SDK supports Android 4.4 or above. Android Studio recommends using 3.6 or above. Currently, it does not support emulator operation.。

## <a name='1'></a>1、 Development Environment Preparation

##### Please make sure to meet the following development environment：

- AndroidStudio 3.0 or above version。
- Android version is not less than 4.4 and supports audio and video Android real machine。
- Android device is connected Internet。

## <a name='2'></a>2、 Import the SDK

### 2.1、gradle integration mode

#### 2.1.1 Add Maven library


Open the build.gradle file in the project root directory，Add the following code to the repositories node of buildscript and allprojects：

```java
maven {
    url 'http://maven.linkv.fun/repository/liveme-android/'
    credentials {
        username = 'LivemesdkPublicUser'
        password = 'public'
    }
}
```
![](https://dl.linkv.io/doc/en/android/live/images/gradle_introduce_live1.png)

#### 2.1.2 Gradle introduces livemeuisdk dependency

In the build.gradle file of the main module of the project, add the following library dependencies under the dependencies node：

```java
dependencies {
    ...
    // Recommend to use the latest version
    implementation 'com.app.live:livemeuisdk:latest'
}
```
![](https://dl.linkv.io/doc/en/android/live/images/gradle_introduce_live2.png)

#### 2.1.3 Add Java8 language support

In the build.gradle file of the main module of the project，Add the following library dependencies under the android node：

```java
android {
    ...
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```
![](https://dl.linkv.io/doc/en/android/live/images/gradle_introduce_live3.png)

## <a name='3'></a>3、Add permissions


Open the project in the app/SRC/main/AndroidManifest. The XML file, add the following code.
```java
<!--Access network connection，GPRS traffic may be generated-->
<uses-permission android:name="android.permission.INTERNET" />
<!--Change WiFi status-->
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<!--Access phone status-->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```
![](https://dl.linkv.io/doc/zh/android/live/images/add_permission.png)

## <a name='4'></a>4、 FileProvider conflict
Be aware of this when FileProvider is used in your project, and ignore if FileProvider is not used。
If there is a similar prompt:
```java
java.lang.IllegalArgumentException: Couldn't find meta-data for provider with authority xxx.xxx.provider
```
There is a conflict between FileProvider used in the project and the authorities used in the SDK, which needs to be handled as follows:
### 4.1、Open the AndroidManifest.XML file in the main application and add code under the Application node:
```java
<provider
    android:name="androidx.core.content.FileProvider"
    tools:replace="android:authorities"
    android:authorities="${applicationId}.provider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/paths" />
</provider>
```
![](https://dl.linkv.io/doc/en/android/live/images/include_problem6.png)

## <a name='5'></a>5、 common problem

### 5.1、Conflict of allowBackup attribute in AndroidManifest file

If there is a hint like this：
```java
Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml:7:9-35
        is also present at [com.app.live:livemesdk:0.0.24-outerLenovoRelease] AndroidManifest.xml:34:9-36 value=(false).
        Suggestion: add 'tools:replace="android:allowBackup"' to <application> element at AndroidManifest.xml:6:5-21:19 to override.
```
Then it indicates that the allowBackup attribute in the AndroidManifest file has a conflict, which needs to be handled as follows:
#### 5.1.1、Open the Androidmanifest.XML file in the main application and add attributes under the manifest node:
```java
xmlns:tools="http://schemas.android.com/tools"
```
![](https://dl.linkv.io/doc/en/android/live/images/include_problem1.png)

#### 5.1.2、Open the AndroidManifest.XML file in the main application and add attributes under the Application node:
```java
tools:replace="android:allowBackup"
```
![](https://dl.linkv.io/doc/en/android/live/images/include_problem2.png)

### 5.2、The number of apk methods is greater than 65536

If there is a hint like this：：
```java
Error: Cannot fit requested classes in a single dex file (# methods: 67667 > 65536)
```
It indicates that the number of methods in APK exceeds the limit of 65536, and the following configuration is required:
#### 5.2.1、Open the App/build.Gradle file in the main project, and add the following code under the Dependencies node：
```java
dependencies {
    ...
    implementation 'com.android.support:multidex:1.0.3'
}
```
![](https://dl.linkv.io/doc/en/android/live/images/include_problem3.png)

#### 5.2.2、Open the app/ build.Gradle file in the main project and add the following code under the defaultConfig node：
```java
multiDexEnabled true
```
![](https://dl.linkv.io/doc/en/android/live/images/include_problem4.png)

#### 5.2.3、Open the custom Application subclass in the main project and add the following code in the onCreate method:
```java
MultiDex.install(this);
```
![](https://dl.linkv.io/doc/en/android/live/images/include_problem5.png)
