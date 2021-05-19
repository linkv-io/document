# API summary

**Update date：2020-08-19**

This summary includes the method functions for initialization, common functions and SDK callback functions

## The Member variables

SDK member variables under this category

| Method name           | Descriptions             |
| ---------------- | ---------------- |
| delegate         | SDK delegate callback      |
| showLoginView    | Whether to display the login window |
| diamondAvailable | Whether to hide the withdrawal entrance |

## Basic functions

This category is the basic functions of SDK

| Method name           | Descriptions             |
| -------------------------------- | ------------------------------------------------------------ |
| [sharedInstance](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/sharedInstance)              | Initialization function, initialize SDK via secret|
| [startWithAppid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/startWithAppid:secret:)              | Initialization function, initialize SDK via secret|
| [applicationWillTerminate](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/applicationWillTerminate:)     | UIApplication lifecylcle function, when the applicationWillTerminate is called will trigger the call to notify the SDK|
| [didReceiveRemoteNotification](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/didReceiveRemoteNotification:) | This function is called when the push notification is received|
| [deviceId](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/deviceId)                     | After successfully logging in to the SDK, calling this function will obtain a custom LiveMe device id|
| [onLoginSuccessWithOriginUid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/onLoginSuccessWithOriginUid:uid:token:)  | Log in to the SDK through the openid and token that obtained from the server|
| [onLogout](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/onLogout)                     | log out                                                     |
| [setReleaseEnv](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/setReleaseEnv:)                | Set the development environment to release mode or debug mode|
| [startBroadcast](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/startBroadcast)               | Start the live streaming                                                     |
| [startWatchLive](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/startWatchLive:)               | Start watching live broadcast                                                 |
| [openPersonalPage](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/openPersonalPage)             | Direct to personal page                                               |
| [openContributionRankPage](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/openContributionRankPage)     | Open fans contribution list                                             |
| [openMessageList](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/openMessageList)              | Open private message page                                                 |
| [getChatUnReadNum](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/getChatUnReadNum)             | Get the number of unread messages                                               |
| [showLiveListFilter](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/showLiveListFilter)           | Popup gender tab on the live broadcast list                                        |
| [getOrderId](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/getOrderId:)                   | Get the current order id                                               |
| [featureListView](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/featureListView)               | Get the views of the live broadcast list                                                  |
| [fetchVideoList](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/fetchVideoList:gender:page:complete:)               | Get the data of the live broadcast list                                                 |
| [jumpToLiveRoomWithVid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/jumpToLiveRoomWithVid:)        | Direct to live broadcast room                                                 |
| [isUserLogin](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/isUserLogin)                  | Get the current login status                                             |
| [bindingTokenWithUid](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/bindingTokenWithUid:userName:compel)                  | Test environment, fast login                                             |

## The Callback functions

this category is about the SDK callback functions

| Method name           | Descriptions             |
| ------------------------------------ | ---------------------------- |
| [onBuyCoinsWithOrderId](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onBuyCoinsWithOrderId:source:completion:)            | Recharge completion callback                 |
| [agreePrivacyPolicyWithCompletion](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/agreePrivacyPolicyWithCompletion:) | the callback for whether is agreed to the privacy policy         |
| [hasAgreeGDPR](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/hasAgreeGDPR)                     | EU GDPR privacy policy authorization status callback |
| [onTokenIsInvalid](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onTokenIsInvalid:)                 | the callback for invalid user Token            |
| [onUserBlock](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onUserBlock)                      | the callback when user is blocked out            |
| [updateChatUnReadNum](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/updateChatUnReadNum:)              | the unread messages update notification callback         |
| [onDataTrack](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/onDataTrack:)              | Event tracking notification callback         |
| [filterGender](https://dl.linkv.io/static/iOS/LiveMe/api/Protocols/LiveMeSDKDelegate.html#//api/name/filterGender)                     | callback for filtering the live broadcast list by gender   |

