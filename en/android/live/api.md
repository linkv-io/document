# API summary

**Update Date：2020-08-19**

This summary includes the method functions for initialization, common functions and SDK callback functions

## The Member variables

SDK member variables under this category

| variable name               | Description             |
| -------------------- | ---------------- |
| mLiveInterface         | SDK listening callback      |



## Basic functions

This category is the basic functions of SDK

| Method name           | Descriptions             |
| -------------------------------- | ------------------------------------------------------------ |
| [getInstance](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#getInstance--)              | Get the singleton of the live control class                              |
| [initSdk](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#initSdk-android.app.Application-java.lang.String-java.lang.String-com.app.livesdk.TokenCallback-)              | Initialization function, initialize SDK through secret                             |
| [getDeviceId](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#getDeviceId-android.content.Context-)                     | Calling this function after successfully logging in to the SDK will get a custom LiveMe device id        |
| [onLoginSuccess](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#onLoginSuccess-java.lang.String-java.lang.String-java.lang.String-)  | Log in to the SDK through the openid and token obtained from the server                         |
| [onLogout](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#onLogout--)                     | log out                                                     |
| [startBroadcast](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#startBroadcast-android.content.Context-)               | Start the live streaming                                                     |
| [startWatchLive](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#startWatchLive-android.content.Context-java.lang.String-)               | Start watching live broadcast                                                 |
| [openPersonalPage](https://dl.linkv.io/static/Android/LiveMe/api/lenovoui/com/app/live/util/LinkVUIUtil.html#openPersonalPage-android.content.Context-)             | Direct to personal page                                               |
| [openLeaderBoardPage](https://dl.linkv.io/static/Android/LiveMe/api/lenovoui/com/app/live/util/LinkVUIUtil.html#openLeaderBoardPage-android.content.Context-)     | Open gifter leaderboard                                             |
| [openMessageList](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#openMessageList-android.content.Context-)              | Open private message page                                                 |
| [getChatUnReadNum](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#getChatUnReadNum--)             | Get the number of unread messages                                               |
| [showGenderSelectDialog](https://dl.linkv.io/static/Android/LiveMe/api/lenovoui/com/app/live/util/LinkVUIUtil.html#showGenderSelectDialog-androidx.fragment.app.Fragment-)           | Pop up the gender tab of the live broadcast list                                       |
| [createVideoListFragment](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#createVideoListFragment-android.content.Context-)               | Get live streaming list view                                                 |
| [fetchVideoList](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#fetchVideoList)               | Get the data of the live broadcast list                                                 |
| [jumpToLiveRoomWithVid](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#jumpToLiveRoomWithVid-android.content.Context-java.lang.String-)        | Direct to live broadcast room                                                 |
| [isUserLogin](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#isUserLogin--)                  | Get the current login status                                             |
| [bindingTokenWithUid](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.html#bindingTokenWithUid-java.lang.String-java.lang.String-com.app.user.login.development.LoginGetTokenWrapper.OnBindingTokenListener-)                  | Test environment, fast login                                             |

## The Callback functions

this category is about the SDK callback functions

| Method name           | Descriptions             |
| ------------------------------------ | ---------------------------- |
| [onBuyGold](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#onBuyGold-android.app.Activity-int-int-java.lang.String-)            | Callback when recharge is complete                 |
| [onVideoClick](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#onVideoClick-android.app.Activity-com.app.livesdk.OnTermConfirmCallback-) | Whether to agree to the privacy agreement callback         |
| [onTermConfirm](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/OnTermConfirmCallback.html#onTermConfirm-boolean-)                     | EU GDPR privacy clause authorization status method |
| [onTokenExpire](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/TokenCallback.html#onTokenExpire-java.lang.String-int-java.lang.String-)                 | User token invalidation callback            |
| [onUserBlock](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/TokenCallback.html#onUserBlocked--)                      | the callback when user is blocked out           |
| [updateNum](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeClient.UnReadListener.html#updateNum-int-)              | Unread message update notification callback         |
| [onDataTrack](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#onDataTrack-com.app.livesdk.KEWLDataTrackModel-)              | Event tracking notification callback         |
| [filterGender](https://dl.linkv.io/static/Android/LiveMe/api/livemesdk/com/app/livesdk/LiveMeLiveInterface.html#filterGender-int-)                     | callback for filtering the live broadcast list by gender   |
