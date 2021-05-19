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

For security reasons, the access of the client SDK requires the intervention of the server of the accessing party. When the client logs into the SDK, the corresponding live_open_id and live_token are first obtained from the server of the accessing party, and the login operation is performed after successful return.
####  For server-side development, please refer to the following sequence diagram

![img](https://dl.linkv.io/doc/en/android/live/images/live_install.png)

```sh
After the server has initialized the SDK，Call GetTokenByThirdUID method to get live_open_id and live_token

```

#### The client login process is as follows

![img](https://dl.linkv.io/doc/en/android/live/images/login.png)

If it is currently not logged in, the client needs to request the access server to interact with our server and obtain the OpenID and token successfully to call the login method.

```java
/**
 * Linkv login interface
 * @param userId        Access party user ID
 * @param openId        linkv only ID
 * @param token         Server-side authentication token
 */
LiveMeClient.getInstance().onLoginSuccess(userId, live_open_id, live_token);
```

We provide the fast binding of login interface in the demo source code, which is convenient for you to experience the functions of the SDK

```java
/**
 * Quickly bind the login interface
 * @param uid          Access party user ID
 * @param name          user nickname
 * @param onBindingTokenListener         Bind token state monitoring
 */
LiveMeClient.getInstance().bindingTokenWithUid(uid, name, new LoginGetTokenWrapper.OnBindingTokenListener() {
            @Override
            public void onRequestSuccess(String uid, String live_open_id, String live_token) {
                // Login interface
                LiveMeClient.getInstance().onLoginSuccess(uid, live_open_id, live_token);
            }

            @Override
            public void onRequestFail(String msg) {
            }
        });
```

> This function only works in Debug mode，In order to facilitate quick access to experience product functions。

### 2.2 logout

This method is called when the client logs out

```java
// Exit login status
LiveMeClient.getInstance().onLogout();
```

> 1. During the login process, the accessed uid will be bound with the unique linkv OpenID. The binding content includes the avatars and nicknames of the users, which will be shown in the Live broadcast for displaying and watching. The login and log-out of SDK need to be synchronized with the login and logout of clients to prevent the incorrect user information.
> 2. The SDK log-out will clear the currently cached user information such as uid, openid, token. After logging out, only the function of watching live broadcast is available.
> 3. If the token is invalid, the SDK delegate method of onTokenIsInvalid will be called, and Login again to implement the operation. 


### 2.3 Login status detection

In addition to watching the broadcast function to support the visitor mode，Other functions can only be used after successful login in the SDK, so the current login status needs to be detected after initialization，you need to log in if you are not logged in。

```java
//Login status detection
boolean isLogin = LiveMeClient.getInstance().isUserLogin();
```

> The SDK is single sign-on mode，the kick occurs when both clients log in to the SDK，Therefore, it is recommended to check the login status after the SDK initialization and before calling the function，log in if not logged in。

## <a name='3'></a>3、Get live listings

The createVideoListFragment method is used to quickly retrieve the Fragment of the standardized live list，This view contains three tabs: Popular, Follow, and All. Add the container to the page you want to display to complete the display of the list. The list has basic live broadcast information elements, which can be customized and developed by us, or through fetchVideoList Method to obtain the list data, customize the UI interface by the client of the access party
。

```java
/**
 * Get the live broadcast list view container

 * @param context               Context reference

 * @param container             Display the root layout of the list view、
 */
LiveMeClient.getInstance().createVideoListFragment(context, container);
```

> This function supports guest mode and does not detect the current login status
>

## <a name='4'></a>4、Start live broadcast


During the broadcast process, the SDK will detect and apply for the camera and microphone permissions of the current client. The user's consent and authorization is required to use the live broadcast function. The live broadcast preparation page can upload a custom live broadcast cover, fill in the live broadcast title, select the live broadcast label, and use the beauty filter. The mirror started broadcasting.

```java
/**
 * Call this method for fast live broadcast

 * @param context           Context reference
 */
LiveMeClient.getInstance().startBroadcast(context);
```

> 1. Live broadcast requires the permissions of the camera and microphone. you can complete the corresponding authorizations through Settings->General->App to use the live broadcast function normally
> 2. Live broadcast function only be activated after logging in successfully.
> 3. Before the live broadcast starts, the status of client's privacy agreement authentication will be detected, and the correct the authentication status by returning to the SDK delegate method agreePrivacyPolicyWithCompletion.
> 4. The SDK has built-in beauty filters and stickers. Linkv supports various live broadcast scenarios at the same time, and provides live broadcast functions such as vioce/video calls and Head-to-Head mode. The above functions are all the optional functions they can be enable/disable through the application control panel in the open platform.

## <a name='5'></a>5、Watch the live broadcast

The SDK handles the list of the live broadcasts internally, and the function of re-directing to the page of live broadcast from users' information page. This method will be called by the client when pushing the notification and redirecting to the live broadcast from the UI of the custom live broadcast list. This method used will be introduced in **advanced function** .

Call this method to enter the live page through the media id

```java
/**
 * Use the video ID to watch the live broadcast and jump to the live broadcast page

 * @param context           Context reference
 * @param videoId           Video ID
 */
LiveMeClient.getInstance().startWatchLive(context, videoId);
```

> This method will also detect the authentication status of the user's privacy agreement, and the correct status by returning to the SDK delegate method agreePrivacyPolicyWithCompletion.

