# Integration

Integrated IM SDK currently only supports importing aar files。

## <a name='1'></a>1、Development environment

* The minimum supported Android system version is 19, that is**minSdkVersion ≥ 19。**
* Android Studio **3.0 or above version**。

## <a name='2'></a>2、Integrated SDK

* [Download SDK](/?p=/en/android/im/download_demo.md&k=n2yBGW3V) 。Put the libimcore.aar file in the app/libs directory of the project。

* Configure the parameters in app/build.gradle, as shown below：

  ![img](https://dl.linkv.io/doc/en/android/im/images/import_aar_setting.png)

* Add the following content to the app's build.gradle file：

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

## <a name='3'></a>3、Prevent obfuscated code

Open the obfuscation configuration file (app/proguard-rules.pro) in the project and add the following line of code：

```java
-keep public class com.im.** { *; }
```

