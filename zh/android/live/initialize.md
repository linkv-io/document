# 初始化

**更新时间：2020-08-19**

## <a name='1'></a>1、概述

集成 SDK 完成后，需要在开发者开放平台申请账号、创建应用并获取SDK鉴权需要的appid 和 secret才能继续使用.

## <a name='2'></a>2、初始化

### 2.1、创建应用

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV)。

### 2.2、实现 LiveMeLiveInterface 接口

在使用 SDK 之前需要设置 LiveMeLiveInterface 回调，故需要实现这个接口。

< 实现 LiveMeLiveInterface 接口时必须实现 onVideoClick 方法，因为在观看直播和开播功能中会对当前的隐私协议授权状态做校验，没有得到授权会影响以上功能的使用，如果想要正常使用 SDK 中的全部功能需要在 onVideoClick 方法返回正确的隐私协议授权状态，需要有接入方实现的其他代理方法将在 [回调函数](/zh/android/livemesdk/callback.md) 中做详细介绍。

```java
public class LiveMeImpl extends LiveMeLiveInterface {
    /**
     * 对隐私协议进行授权操作
     * @param activity              调用此方法的Activity
     * @param confirmCallback       确定授权隐私回调
     */
    public void onVideoClick(Activity activity, OnTermConfirmCallback confirmCallback) {
        confirmCallback.onTermConfirm(true);
    }
}
```

### 2.3、初始化SDK

在使用 SDK 之前需要设置SDK监听回调，并调用 initSdk 方法对 SDK 进行初始化操作，建议在 Application 中进行：

```java
import com.app.livesdk.LiveMeClient;

// 设置为测试环境
CommonConflict.DEBUG_SERVER_ENV =  true;

// 设置 SDK 监听回调
LiveMeClient.getInstance().setLiveMeInterface(new LiveMeImpl());

/**
 * SDK 初始化方法
 * @param context       上下文引用
 * @param appId         开发者平台申请的appId
 * @param app_secret    开发者平台申请的密钥
 * @param callback      token状态回调
 */
LiveMeClient.getInstance().initSdk(context, appId, app_secret, callback);
```

#### 参数解析

- context
  - 上下文引用，建议设置为 Application 对象。

- appId
  - 设置为从 [开发者平台](/?p=%252Fzh%252Fandroid%252Frtc%252Finit_sdk.md&k=qC1TAJfr) 申请的 appId

- app_secret
  - 设置为从 [开发者平台](/?p=%252Fzh%252Fandroid%252Frtc%252Finit_sdk.md&k=qC1TAJfr) 申请的 secret
   
- callback
  - 当token过期或者用户被禁止登录时触发此监听，回调相应的方法。

