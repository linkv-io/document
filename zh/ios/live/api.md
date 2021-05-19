# 客户端 API 汇总

**更新时间：2020-08-19**

此文档主要包括初始化和常用功能的方法函数以及SDK回调函数

## 成员变量

此分类下为SDK成员变量

| 方法名           | 说明             |
| ---------------- | ---------------- |
| delegate         | SDK代理回调      |
| showLoginView    | 是否显示登录窗口 |
| diamondAvailable | 是否屏蔽提现入口 |

## 基础功能

此分类下为SDK的基础功能函数

| 方法名                           | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| [sharedInstance](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/sharedInstance)              | 初始化函数，通过secret初始化SDK                              |
| [startWithAppid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/startWithAppid:secret:)              | 初始化函数，通过secret初始化SDK                              |
| [applicationWillTerminate](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/applicationWillTerminate:)     | UIApplication生命周期函数applicationWillTerminate被调用时调用此函数通知SDK |
| [didReceiveRemoteNotification](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/didReceiveRemoteNotification:) | 当收到推送通知时调用此函数                                   |
| [deviceId](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/deviceId)                     | 登录SDK成功后调用该函数会获取一个自定义的LiveMe设备id        |
| [onLoginSuccessWithOriginUid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/onLoginSuccessWithOriginUid:uid:token:)  | 通过服务端获取的openid和token登录SDK                         |
| [onLogout](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/onLogout)                     | 退出登录                                                     |
| [setReleaseEnv](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/setReleaseEnv:)                | 设置开发环境为release模式或者debug模式                       |
| [startBroadcast](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/startBroadcast)               | 开始直播                                                     |
| [startWatchLive](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/startWatchLive:)               | 开始观看直播                                                 |
| [openPersonalPage](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/openPersonalPage)             | 跳转到个人页面                                               |
| [openContributionRankPage](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/openContributionRankPage)     | 打开粉丝贡献榜单                                             |
| [openMessageList](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/openMessageList)              | 打开私信页面                                                 |
| [getChatUnReadNum](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/getChatUnReadNum)             | 获取未读消息数                                               |
| [showLiveListFilter](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/showLiveListFilter)           | 弹出直播列表性别选项卡                                       |
| [getOrderId](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/getOrderId:)                   | 获取当前订单id                                               |
| [featureListView](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/featureListView)               | 获取直播列表视图                                                 |
| [fetchVideoList](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/fetchVideoList:gender:page:complete:)               | 获取直播列表数据                                                 |
| [jumpToLiveRoomWithVid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/jumpToLiveRoomWithVid:)        | 跳转到直播间                                                 |
| [isUserLogin](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/isUserLogin)                  | 获取当前登录状态                                             |
| [bindingTokenWithUid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/bindingTokenWithUid:userName:compel)                  | 测试环境快速登录                                             |

## 回调函数

此分类下为SDK回调函数

| 方法名                               | 说明                         |
| ------------------------------------ | ---------------------------- |
| [onBuyCoinsWithOrderId](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onBuyCoinsWithOrderId:source:completion:)            | 充值完成回调                 |
| [agreePrivacyPolicyWithCompletion](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/agreePrivacyPolicyWithCompletion:) | 是否同意隐私协议回调         |
| [hasAgreeGDPR](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/hasAgreeGDPR)                     | 欧盟GDPR隐私条款授权状态回调 |
| [onTokenIsInvalid](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onTokenIsInvalid:)                 | 用户token失效回调            |
| [onUserBlock](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onUserBlock)                      | 当前用户被拉黑回调           |
| [updateChatUnReadNum](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/updateChatUnReadNum:)              | 未读消息更新通知回调         |
| [onDataTrack](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onDataTrack:)              | 埋点事件通知回调         |
| [filterGender](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/filterGender)                     | 获取直播列表默认筛选性别回调   |

