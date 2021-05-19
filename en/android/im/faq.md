
# Common Questions

## <a name='1'></a>1、libsqlite.soLibrary duplication problem。

* Problem description: If the project introduces libsqlite.so library, it will prompt a repeated conflict error for this library when packaging the resource file.
* Solution: Add packagingOptions to android nodes where the build.Gradle file for the module that introduces libsqlite. So：

```xml
android{
		// ....

    // IM SDK included libsqlite.so，So packaging doesn't include.
    packagingOptions {
        exclude "lib/arm64-v8a/libsqlite.so"
        exclude "lib/armeabi-v7a/libsqlite.so"
    }
}
```

