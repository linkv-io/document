# The Common Functions

**Update date：2020-08-19**

## <a name='1'></a>1、Overview

This article is about the common functions and precautions in the SDK functions that you need to know. The common functions mainly include the followings:

* Log in/out
* Obtaining the live broadcasting list
* Starting the live broadcasting
* Watching the live broadcasting

## <a name='2'></a>2、Login/logout.

### <a name='2.1'></a>2.1 Login

For security reasons, access to the client SDK requires the intervention of the access side server. When the client logs in to the SDK, it first obtains the corresponding LIVE_open_ID and live_token from the access side server, and then carries out the login operation after successful return.
####  Server-side development can be referred to in the following sequence diagram

![img](https://dl.linkv.io/doc/en/ios/live/images/live_install.png)

```sh
After the SDK is initialized, the server calls the GetTokenByThirdUID method to get live_open_ID and live_token```

#### The client login process is as follows

![img](https://dl.linkv.io/doc/en/ios/live/images/login.png)

If it is currently not logged in, the client needs to request the access server to interact with our server and obtain the OpenID and token successfully to call the login method.

``` 
/**
* desc linkv Login interface
*@param originUid User id
*@param openid linkv Uniqueid
*@param token Server authentication token
**/
[[LiveMeSDK sharedInstance] onLoginSuccessWithOriginUid:originUid uid:openid token:token];
```

We provide the fast binding of login interface in the demo source code, which is convenient for you to experience the functions of the SDK

``` 
[[LiveMeSDK sharedInstance] bindingTokenWithUid:uid uname:uname complete:^(NSString *originId, NSString *uid, NSString *token) {
     [[LiveMeSDK sharedInstance] onLoginSuccessWithOriginUid:originId uid:uid token:token];
}];
```

> This function only takes effect in the debug mode to facilitate the quick access to experience product functions.

### <a name='2.2'></a>2.2 Logout

This method is called when the client logs out

``` 
[[LiveMeSDK sharedInstance] onLogout];
```

> 1. During the login process, the accessed uid will be bound with the unique linkv OpenID. The binding content includes the avatars and nicknames of the users, which will be shown in the Live broadcast for displaying and watching. The login and log-out of SDK need to be synchronized with the login and logout of clients to prevent the incorrect user information.
> 2. The SDK log-out will clear the currently cached user information such as uid, openid, token. After logging out, only the function of watching live broadcast is available.
> 3. If the token is invalid, the SDK delegate method of onTokenIsInvalid will be called, and Login again to implement the operation. 

### <a name='2.3'></a>2.3 Login status detection

Additionally, watching the broadcast function is supported as the guest mode, all other functions will be available after logging in to the SDK. So after the initialization is completed, you need to check the current login status. Please login to SDK if not.

``` 
// Login status detection
BOOL isLogin = [[LiveMeSDK sharedInstance] isUserLogin];
```

> The SDK is in single sign-on. It means when two clients log in to the SDK and they will be kicked out. Therefore, it is recommended to check the login status after the SDK is initialized and before calling the functions. If you are not logged in, please do so.

## <a name='3'></a>3、The List of live broadcasts

By calling the [featureListView](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/featureListView) , you can quickly obtain the view container of the standardized list of live broadcasts. The view contains three tabs: features, followed, and all. To complete the list display, please add this container to the page you would like to display on. The list contains basic live broadcast information. And the elements can be customized and developed by our side, or the list data can be obtained by the [fetchVideoList](https://dl.linkv.io/static/iOS/LiveMe/api/Classes/LiveMeSDK.html#//api/name/fetchVideoList:gender:page:complete:) and the UI can be customized by the access client.

``` 
//obtain the view container of live broadcast list
[[LiveMeSDK sharedInstance] featureListView];
```

> This function supports the guest mode and the current login status will not be detected.
>

## <a name='4'></a>4、Starting the live broadcast

During the live broadcast, the SDK will detect and apply for the camera and microphone permissions of the current client. The user needs to agree and authorize the permissions to use the live broadcast function. On the live broadcast preparation page users can upload a custom picture as the cover, and fill in the live broadcast title, select the live broadcast tags, and use the beauty filters to start the broadcasting.

``` 
//Call this method to start the live broadcast
[[LiveMeSDK sharedInstance] startBroadcast];
```

> 1. Live broadcast requires the permissions of the camera and microphone. you can complete the corresponding authorizations through Settings->General->App to use the live broadcast function normally
> 2. Live broadcast function only be activated after logging in successfully.
> 3. Before the live broadcast starts, the status of client's privacy agreement authentication will be detected, and the correct the authentication status by returning to the SDK delegate method agreePrivacyPolicyWithCompletion.
> 4. The SDK has built-in beauty filters and stickers. Linkv supports various live broadcast scenarios at the same time, and provides live broadcast functions such as vioce/video calls and Head-to-Head mode. The above functions are all the optional functions they can be enable/disable through the application control panel in the open platform.

## <a name='5'></a>5、Watch the live broadcast

The SDK handles the list of the live broadcasts internally, and the function of re-directing to the page of live broadcast from users' information page. This method will be called by the client when pushing the notification and redirecting to the live broadcast from the UI of the custom live broadcast list. This method used will be introduced in **advanced function** .

Call this method to enter the live page through the media id

``` 
/**
* vid media source id
**/
[[LiveMeSDK sharedInstance] jumpToLiveRoomWithVid:vid];
```

> This method will also detect the authentication status of the user's privacy agreement, and the correct status by returning to the SDK delegate method agreePrivacyPolicyWithCompletion.
>

## <a name='6'></a>6、Open personal page

```
// Call this method to jump to a personal page
[[LiveMeSDK sharedInstance] openPersonalPage];
```

## <a name='7'></a>7、Open the leaderboard page

```
// Call this method to open the leaderboard
[[LiveMeSDK sharedInstance] openContributionRankPage];
```

## <a name='8'></a>8、Filter the gender

```
// Call this method to filter gender list data
[[LiveMeSDK sharedInstance] showLiveListFilter];
```

