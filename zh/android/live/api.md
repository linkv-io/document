# 客户端 API 汇总

**更新时间：2020-08-19**

此文档主要包括初始化和常用功能的方法函数以及SDK回调函数

## 成员变量

此分类下为SDK成员变量

| 变量名               | 说明             |
| -------------------- | ---------------- |
| mLiveInterface         | SDK监听回调      |



## 基础功能

此分类下为SDK的基础功能函数

| 方法名                           | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| [getInstance](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#getInstance--)              | 获取到直播控制类的单例                              |
| [initSdk](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#initSdk-android.app.Application-java.lang.String-java.lang.String-com.app.livesdk.TokenCallback-)              | 初始化函数，通过secret初始化SDK                              |
| [getDeviceId](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#getDeviceId-android.content.Context-)                     | 登录SDK成功后调用该函数会获取一个自定义的LiveMe设备id        |
| [onLoginSuccess](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#onLoginSuccess-java.lang.String-java.lang.String-java.lang.String-)  | 通过服务端获取的openid和token登录SDK                         |
| [onLogout](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#onLogout--)                     | 退出登录                                                     |
| [startBroadcast](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#startBroadcast-android.content.Context-)               | 开始直播                                                     |
| [startWatchLive](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#startWatchLive-android.content.Context-java.lang.String-)               | 开始观看直播                                                 |
| [openPersonalPage](https://dl.linkv.io/static/Android/LiveMe/api/lenovoui/com/app/live/util/LinkVUIUtil.html#openPersonalPage-android.content.Context-)             | 跳转到个人页面                                               |
| [openLeaderBoardPage](https://dl.linkv.io/static/Android/LiveMe/api/lenovoui/com/app/live/util/LinkVUIUtil.html#openLeaderBoardPage-android.content.Context-)     | 打开粉丝贡献榜单                                             |
| [openMessageList](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#openMessageList-android.content.Context-)              | 打开私信页面                                                 |
| [getChatUnReadNum](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#getChatUnReadNum--)             | 获取未读消息数                                               |
| [showGenderSelectDialog](https://dl.linkv.io/static/Android/LiveMe/api/lenovoui/com/app/live/util/LinkVUIUtil.html#showGenderSelectDialog-androidx.fragment.app.Fragment-)           | 弹出直播列表性别选项卡                                       |
| [createVideoListFragment](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#createVideoListFragment-android.content.Context-)               | 获取直播列表视图                                                 |
| [fetchVideoList](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#fetchVideoList)               | 获取直播列表数据                                                 |
| [jumpToLiveRoomWithVid](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#jumpToLiveRoomWithVid-android.content.Context-java.lang.String-)        | 跳转到直播间                                                 |
| [isUserLogin](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#isUserLogin--)                  | 获取当前登录状态                                             |
| [bindingTokenWithUid](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#bindingTokenWithUid-java.lang.String-java.lang.String-com.app.user.login.development.LoginGetTokenWrapper.OnBindingTokenListener-)                  | 测试环境快速登录                                             |


## 回调函数

此分类下为SDK回调函数

| 方法名                               | 说明                         |
| ------------------------------------ | ---------------------------- |
| [onBuyGold](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#onBuyGold-android.app.Activity-int-int-java.lang.String-)            | 充值完成回调                 |
| [onVideoClick](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#onVideoClick-android.app.Activity-com.app.livesdk.OnTermConfirmCallback-) | 是否同意隐私协议回调         |
| [onTermConfirm](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/OnTermConfirmCallback.html#onTermConfirm-boolean-)                     | 欧盟GDPR隐私条款授权状态方法 |
| [onTokenExpire](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/TokenCallback.html#onTokenExpire-java.lang.String-int-java.lang.String-)                 | 用户token失效回调            |
| [onUserBlock](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/TokenCallback.html#onUserBlocked--)                      | 当前用户被拉黑回调           |
| [updateNum](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.UnReadListener.html#updateNum-int-)              | 未读消息更新通知回调         |
| [onDataTrack](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#onDataTrack-com.app.livesdk.KEWLDataTrackModel-)              | 埋点事件通知回调         |
| [filterGender](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#filterGender-int-)                     | 获取直播列表默认筛选性别回调   |
