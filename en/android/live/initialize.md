# Initialization


**Update date：2020-08-19**

## <a name='1'></a>1、Overview

After the SDK integration is completed, it is necessary to apply for an account on the developer open platform, create an application, and obtain the APPID and secret required for SDK authentication before continuing to use.
## <a name='2'></a>2、Initialization


### 2.1、Create application

Please apply for the appid and signature required for SDK authentication in [LinkV Developer Background](http://dev.linkv.io/)，[Get AppID and AppSecret guidelines](/?p=%252Fzh%252Fopen%252Fquick_start.md&k=R5tULcvV)。

### 2.2、Implement LiveMeLiveInterface interface

Before using the SDK, you need to set the LiveMeLiveInterface callback, so you need to implement this interface.
<The onVideoClick method must be implemented when implementing the LiveMeLiveInterface interface，because the current privacy agreement authorization status will be verified in the live broadcast and start-up function，failure to obtain authorization will affect the use of the above functions，If you want to use all the functionality in the SDK properly, you need to return the correct privacy protocol authorization status in the onVideoClick method，need to have access to the implementation of the methods of other agents are discussed in [the callback function] (/ en/android/livemesdk/callback. The md) in detail。

```java
public class LiveMeImpl extends LiveMeLiveInterface {
    /**
     * Authorize the privacy protocol
     * @param activity              The Activity that calls this method
     * @param confirmCallback       Determine the authorized privacy callback
     */
    public void onVideoClick(Activity activity, OnTermConfirmCallback confirmCallback) {
        confirmCallback.onTermConfirm(true);
    }
}
```

### 2.3、Initialize SDK

Before using THE SDK, it is necessary to set the SDK to listen to the callback and call the initSdk method to initialize the SDK. It is recommended to do so in the Application:
```java
import com.app.livesdk.LiveMeClient;

// Set to test environment
CommonConflict.DEBUG_SERVER_ENV =  true;

// Set the SDK to listen for callbacks
LiveMeClient.getInstance().setLiveMeInterface(new LiveMeImpl());

/**
 * SDK Initialization method
 * @param context       Context reference
 * @param appId         appId for developer platform application
 * @param app_secret    The key requested by the developer platform
 * @param callback      Token state callback
 */
LiveMeClient.getInstance().initSdk(context, appId, app_secret, callback);
```

#### Parameter analysis

- context
  - Context reference, it is recommended to set to Application object。

- appId
  - Set to the appId applied from [Developer Platform](/?p=%252Fzh%252Fandroid%252Frtc%252Finit_sdk.md&k=qC1TAJfr) 

- app_secret
  - Set to the secret applied from [Developer Platform](/?p=%252Fzh%252Fandroid%252Frtc%252Finit_sdk.md&k=qC1TAJfr) 
   
- callback
  - This monitor is triggered when the token expires or the user is prohibited from logging in, and the corresponding method is called back.

