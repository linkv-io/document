# 客户端集成

**更新时间：2020-08-27**

LiveMe 社交娱乐SDK目前支持Maven集成方式，SDK支持 Android 4.4 或以上版本系统，AndroidStudio建议使用3.6或以上版本，目前暂不支持模拟器运行。

## <a name='1'></a>1、 环境准备

##### 请确保满足以下开发环境：

- AndroidStudio 3.0 或以上版本。
- Android 版本不低于 4.4 且支持音视频的 Android 真机。
- Android 设备已经连接到 Internet。

## <a name='2'></a>2、 导入工程

### 2.1、gradle集成方式

#### 2.1.1 添加Maven库

打开项目根目录下的build.gradle文件，在 buildscript 与 allprojects 的 repositories 节点中添加如下代码：

```java
maven {
    url 'http://maven.linkv.fun/repository/liveme-android/'
    credentials {
        username = 'LivemesdkPublicUser'
        password = 'public'
    }
}
```
![](https://dl.linkv.io/doc/zh/android/live/images/gradle_introduce_live1.png)

#### 2.1.2 gradle引入livemeuisdk依赖

在项目主模块的build.gradle文件中，dependencies节点下添加如下库依赖：

```java
dependencies {
    ...
    // 建议使用最新版本,x.x.x 为版本号.
    implementation 'com.app.live:linkvui:x.x.x'
}
```
![](https://dl.linkv.io/doc/zh/android/live/images/gradle_introduce_live2.png)

#### 2.1.3 添加Java8语言支持

在项目主模块的build.gradle文件中，android节点下添加如下库依赖：

```java
android {
    ...
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
```
![](https://dl.linkv.io/doc/zh/android/live/images/gradle_introduce_live3.png)

## <a name='3'></a>3、添加权限

打开项目中的app/src/main/AndroidManifest.xml文件，添加如下代码。
```java
<!--访问网络连接，可能产生GPRS流量-->
<uses-permission android:name="android.permission.INTERNET" />
<!--改变WiFi状态-->
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<!--访问电话状态-->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```
![](https://dl.linkv.io/doc/zh/android/live/images/add_permission.png)

## <a name='4'></a>4、 FileProvider冲突
当项目中使用了FileProvider需要注意此问题，如果没有使用FileProvider则忽略。
如果有类似提示：
```java
java.lang.IllegalArgumentException: Couldn't find meta-data for provider with authority xxx.xxx.provider
```
则说明项目中使用的FileProvider与sdk中使用的FileProvider的authorities冲突了，需要如下处理：

### 4.1、打开主应用中的AndroidManifest.xml文件，在application节点下添加代码:
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
![](https://dl.linkv.io/doc/zh/android/live/images/include_problem6.png)

### 4.2、 自定义FileProvider的resource路径冲突,SDK中的FileProvider的resource路径为:paths。
当项目中使用了自定义FileProvider需要注意此问题，如果没有使用自定义FileProvider则忽略。
如果有类似提示:
```
Attribute meta-data#android. support. FILE_ PROVIDER_ PATHS@resource value=(@xml/file_ paths)from AndroidManifest.xml:101:17-51
is also present at [com. app. live: linkvui:0.0. 60.57] AndroidManifest.xml:95:17-46 value=(@xml/paths) ,
Suggestion: add ' tools: replace="android: resourcel"' to <meta-data> element at AndroidManifest . xml:99:13-101:54 to override.
```
说明FileProvider的resource路径的路径有冲突,请修改主应用中的自定义FileProvider的resource路径。
例如:resource路径修改为：file_paths,示例代码如下:
```java
<provider
    android:name=".XXXProvider"
    tools:replace="android:authorities"
    android:authorities="${applicationId}.provider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/file_paths"
        tools:replace="android:resource"/>
</provider>	

```


## <a name='5'></a>5、 常见问题

### 5.1、AndroidManifest文件中allowBackup属性冲突问题
如果有类似提示：
```java
Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml:7:9-35
        is also present at [com.app.live:livemesdk:0.0.24-outerLenovoRelease] AndroidManifest.xml:34:9-36 value=(false).
        Suggestion: add 'tools:replace="android:allowBackup"' to <application> element at AndroidManifest.xml:6:5-21:19 to override.
```
则说明AndroidManifest文件中的allowBackup属性有冲突，需要如下处理：

#### 5.1.1、打开主应用中的AndroidManifest.xml文件，在manifest节点下添加属性:
```java
xmlns:tools="http://schemas.android.com/tools"
```
![](https://dl.linkv.io/doc/zh/android/live/images/include_problem1.png)

#### 5.1.2、打开主应用中的AndroidManifest.xml文件，在application节点下添加属性:
```java
tools:replace="android:allowBackup"
```
![](https://dl.linkv.io/doc/zh/android/live/images/include_problem2.png)

### 5.2、apk方法数量大于65536
如果有类似提示：
```java
Error: Cannot fit requested classes in a single dex file (# methods: 67667 > 65536)
```
则说明apk中的方法数量超出65536的限制了，需要进行如下配置：

#### 5.2.1、打开主项目中的app/build.gradle文件，在dependencies节点下添加如下代码：
```java
dependencies {
    ...
    implementation 'com.android.support:multidex:1.0.3'
}
```
![](https://dl.linkv.io/doc/zh/android/live/images/include_problem3.png)

#### 5.2.2、打开主项目中的app/build.gradle文件，在defaultConfig节点下添加如下代码：
```java
multiDexEnabled true
```
![](https://dl.linkv.io/doc/zh/android/live/images/include_problem4.png)

#### 5.2.3、打开主项目中的自定义Application子类，在onCreate方法中添加如下代码：
```java
MultiDex.install(this);
```
![](https://dl.linkv.io/doc/zh/android/live/images/include_problem5.png)
