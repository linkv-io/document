# Callback Sample

**Update date：2020-08-19**

## <a name='1'></a>1、Overview

Interface callbacks, including recharge, sharing, privacy authorization and other related callbacks, you need to set the LiveMeLiveInterface object of the LiveSDK singleton to receive and process proxy callback events。

## <a name='2'></a>2、Set up the delegate

```java
//Set callback
LiveMeClient.getInstance().setLiveMeInterface(new LiveMeImpl());
```

## <a name='3'></a>3、Event

#### （1）Recharge

```java
/**
 * Recharge interface
 * @param activity              The activity in which this method is called
 * @param source                Order type
 * @param requestCode           request code
 * @param orderId               order ID
 **/
public void onBuyGold(Activity activity,int source,int requestCode,String orderId);
```

#### （2）Sharing

```java
/**
 * Sharing monitoring methods
 * @param activity                  The activity in which this method is called
 * @param liveMeShareInfo           Share data
 * @param iShareCallback            share callback
 **/
public void onShareClick(Activity activity, LiveMeShareInfo liveMeShareInfo, IShareCallback iShareCallback);
```

#### （3）Event tracking

```java
/**
 * Data burying point management callback method
 * @param kewlDataTrackModel     Buried point data model

 **/
public void onDataTrack(KEWLDataTrackModel kewlDataTrackModel);
```

#### （4）Privacy agreement authorization

```java
/**
 * Privacy agreement authorization callback

 * @param activity              Call privacy authorized activity
 * @param confirmCallback       Authorize callback

 **/
public void onVideoClick(Activity activity, OnTermConfirmCallback confirmCallback);
```

> Whether to authorize the privacy clause agreement，

#### （5）GDPR authorization status

```java
public interface OnTermConfirmCallback {
    void onTermConfirm(boolean confirm);
}
```

> If the application is published in the EU, GDPR authorization is required. If the authorization fails, the functions of live broadcast and starting the broadcast will be unavailable.

#### （6）Invalid Token

```java
public interface TokenCallback {

    // Token expired
    void onTokenExpire(String var1, int var2, String var3);

}
```

> This function is called when the client token is invalid to notify the client to re-authenticate

#### （7）The user is blocked

```java
public interface TokenCallback {

    // Users blocked
    void onTokenExpire(String var1, int var2, String var3);

}
```

> This function is called when the current user is blocked in the broadcast room

#### （8）Red-dot update for the private messages
```java
/**
 * Interface to monitor the number of unread messages

 * @param unReadNum         Number of unread messages
 **/
public interface UnReadListener {
    public void updateNum(int unReadNum);
}
```

> The prompt for unread private messages. Call this function when there is a new message.

#### （9）The default gender of the live broadcast list

> The live broadcast list is filtered by gender and set as default.
>
> public static final String MALE = "1"; //female
>
> public static final String FAMALE = "0"; //male
>
> public static final String SECRET = "-1", //all
