# 常用功能

**更新时间：2020-10-16**

## <a name='1'></a>1、概述

本文为您需要了解的SDK功能中的常用功能和注意事项，常用功能主要包含以下：

- 登录登出
- 获取直播列表
- 开始直播
- 观看直播

## <a name='2'></a>2、获取直播列表

通过调用createVideoListFragment方法可以快速获取标准化直播列表的Fragment，该视图包含热门、关注、全部三种选项卡，将该容器添加到你想要展示的页面上完成列表的展示，该列表具备基础的直播信息元素，可以由我方定制开发，也可以通过 fetchVideoList 方法获取列表数据由接入方客户端自定义开发UI界面。

```java
/**
 * 获取直播列表视图容器
 * @param context               上下文引用
 * @param container             显示列表视图的根布局
 */
LiveMeClient.getInstance().createVideoListFragment(context, container);
```

> **该功能免登录，不对当前登录状态进行检测。**
>


## <a name='3'></a>3、登录/登出。


### 3.1 登录

出于安全方面的考虑，客户端 SDK的接入需要接入方服务端介入，当客户端登录SDK时首先从接入方服务端获取相应的live_open_id和live_token，成功返回后进行登录操作。

####  服务端开发可以参考如下时序图

![img](https://dl.linkv.io/doc/zh/android/live/images/live_install.png)

```sh
服务端在SDK初始化完毕后，调用 GetTokenByThirdUID 方法获取live_open_id及live_token
```

#### 客户端登录流程如下图

![img](https://dl.linkv.io/doc/zh/android/live/images/login.png)

如果当前为未登录状态，需要客户端请求接入方服务端与我方服务端交互并成功获取openid和token后调用登录方法。

```java
/**
 * linkv登录接口
 * @param userId        接入方用户ID
 * @param openId        linkv唯一ID
 * @param token         服务端鉴权token
 */
LiveMeClient.getInstance().onLoginSuccess(userId, live_open_id, live_token);
```

我们会在演示源码中提供快速绑定登录的接口，方便您体验SDK的功能

```java
/**
 * 快速绑定登录接口
 * @param uid           接入方用户ID
 * @param name          用户昵称
 * @param onBindingTokenListener         绑定token状态监听
 */
LiveMeClient.getInstance().bindingTokenWithUid(uid, name, new LoginGetTokenWrapper.OnBindingTokenListener() {
            @Override
            public void onRequestSuccess(String uid, String live_open_id, String live_token) {
                // 登录接口
                LiveMeClient.getInstance().onLoginSuccess(uid, live_open_id, live_token);
            }

            @Override
            public void onRequestFail(String msg) {
            }
        });
```

> 该函数仅在debug模式下生效，为了方便快速接入体验产品功能。

### 3.2 登出

当客户端登出时调用该方法

```java
// 退出登陆状态
LiveMeClient.getInstance().onLogout();
```

> 1. 登录过程中会对接入方uid和linkv唯一openid进行绑定，绑定内容包括用户信息中的头像和昵称，用于在直播和观看直播中对外展示，未免出现用户信息错误的情况，需要在客户端登录登出时同步进行SDK的登录登出。
> 2. SDK登出会对当前缓存的用户信息和uid、openid、token做清除操作，登出之后只有看播功能可用。
> 3. token失效会调用SDK监听方法onTokenExpire，需要在该方法的实现中重新登录。

### 3.3 登录状态检测

除看播功能支持游客模式外，其他功能均需登录SDK成功后才能使用所以初始化完成后需要检测当前的登录状态，如果未登录需要进行登录。

```java
//登录状态检测
boolean isLogin = LiveMeClient.getInstance().isUserLogin();
```

> SDK为单点登录模式，当两个客户端登录SDK时会进行踢出，所以建议当SDK初始化完成后和调用功能函数前先检测登录状态，如未登录进行登录。


## <a name='4'></a>4、开始直播

开播过程中SDK会对当前客户端的摄像头和麦克风权限进行检测和申请，需要用户同意并授权才能使用直播功能，直播准备页面可以上传自定义直播封面、填写直播标题、选择直播标签、使用美颜滤镜开播。

```java
/**
 * 调用该方法进行快速直播
 * @param context           上下文引用
 */
LiveMeClient.getInstance().startBroadcast(context);
```

> 1. 直播需要摄像头和麦克风权限，如果没有允许相应的授权可以通过设置->通用->应用 打开相应的授权正常使用直播功能
> 2. 直播功能需要在登录状态下才能成功使用
> 3. 直播开始前会检测客户端的用户协议授权状态，需要在SDK代理方法onVideoClick中返回正确的授权状态
> 4. SDK内置美颜滤镜，贴纸。linkv同时支持多种直播场景，可以提供连麦、PK等直播功能，以上功能均为可选功能，可以通过开放平台中应用控制面板设置该功能的打开和关闭

## <a name='5'></a>5、观看直播

SDK内部会处理直播列表、用户信息页面的看播视图跳转功能，该方法会在推送通知和自定义直播列表UI界面跳转直播页面时由客户端发起调用。该方法的具体使用将在 **进阶功能** 中进行详细介绍

调用该方法通过媒体id进入到直播页面

```java
/**
 * 用视频ID观看直播，跳转到直播页面
 * @param context           上下文引用
 * @param videoId           视频ID
 */
LiveMeClient.getInstance().startWatchLive(context, videoId);
```

> 该方法同样会检测用户隐私协议的授权状态，需要在SDK代理方法onVideoClick中返回正确的授权状态。

