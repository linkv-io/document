# 常见问题

## <a name='1'></a>1、libsqlite.so库重复问题。

* 问题描述：如果项目中已经引入libsqlite.so库，则会在打包资源文件时提示此库重复的冲突错误。
* 解决办法：在引入了libsqlite.so的module的build.gradle文件的android节点添加packagingOptions：

```xml
android{
		// ....

    // IM SDK含有libsqlite.so，所以打包不包含。
    packagingOptions {
        exclude "lib/arm64-v8a/libsqlite.so"
        exclude "lib/armeabi-v7a/libsqlite.so"
    }
}
```

