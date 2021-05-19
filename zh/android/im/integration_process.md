# 集成

集成IM SDK目前只支持导入aar文件方式。

## <a name='1'></a>1、开发环境

* 最低支持安卓系统版本 为19，即**minSdkVersion ≥ 19。**
* Android Studio **3.0 或以上版本**。

## <a name='2'></a>2、集成SDK

* [下载 SDK](/?p=/zh/android/im/download_demo.md&k=n2yBGW3V) 。将libimcore.aar文件放到项目的app/libs目录下。

* 在app/build.gradle中配置参数，如下图：

  ![img](https://dl.linkv.io/doc/zh/android/im/images/import_aar_setting.png)

* 在app的build.gradle文件添加如下内容：

  ```xml
  apply plugin: 'com.android.application'
  
   android {
     xxxx
   }
  
   repositories {
     flatDir {
       dirs 'libs'
     }
   }
  
   dependencies {
     implementation fileTree(dir: 'libs', include: ['*.aar', '*.jar'])
   }
  ```

## <a name='3'></a>3、防止混淆代码

打开项目中的混淆配置文件（app/proguard-rules.pro），添加如下一行代码：

```java
-keep public class com.im.** { *; }
```

