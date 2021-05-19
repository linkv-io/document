# Advanced features

**Update Date：2020-08-19**

## <a name='1'></a>1、Overview

Some advanced features are customized developments, it can be disabled or enabled through the official website, including the main functions are as follows:

* Private messaging
* Finance
* Sharing
* Push notification
* Event tracking
* Interactive gameplay
* Broadcaster tools

<img src="https://dl.linkv.io/doc/en/android/live/images/advance.jpg" alt="advance" style="width:90%;" />

## <a name='2'></a>2、Private messaging

It provides the access to two chat pages, which are the private message list and the user's personal information page. It can provide the users with the functions of one-to-one chat, group chat, receiving the stranger's messages, private message and others.

```java
/**
 * Call this method to enter the message list page
 * @param activity          Context reference
 * @param requestCode       Request code
 * @param hostInfo          Represents session information and user information
 * @param from              Record the information of the previous page（From which page）
 */
LiveMeClient.getInstance().getLiveMeInterface().openLetterAct(activity, requestCode, hostInfo, from);
```

> 1. This method will detect the login status, and the message can only be sent and received after the IM configuration is completed.
> 2. The function can be enabled or disabled through the application control panel of the console.
> 3. You can receive the notification of the unread messages through the SDK delegate method of updateChatUnReadNum.

## <a name='3'></a>3、Finance

The SDK provides the withdrawal function, which can be used to forward the recharge orders through the SDK delegate to implement the client recharge function. The recharge process is as follows:

<img src="https://dl.linkv.io/doc/en/android/live/images/charge.png" alt="charge" style="width:50%;" />

#### Delegate

```java
/**
* activity              The activity that called this method
* source                Order Type
* requestCode           Request code
* orderId               Order ID
**/
public void onBuyGold(Activity activity,int source,int requestCode,String orderId);
```

- activity
  - The activity that called this method
- source 
  - Order Type
- requestCode
  - Request code
- orderId
  - Order ID

> 1. This function can be turned on and off through the open platform application control panel
> 2. The content of financial switch includes recharge and withdrawal entrance, gift function, and list function. If you turn off this feature, the gift panel will not be displayed in the live broadcast room, and the personal page will not display the diamond-related information. The advance entry for recharge is blocked, and the list entry is blocked.


## <a name='4'></a>4、Share

Multi-channel sharing is supported. Data forwarding through an agent meets the client sharing function. The SDK only provides the data required for sharing. The sharing operation needs to be performed on the client. The access party needs to apply for the corresponding sharing platform account and make the corresponding project settings.

#### Sharing data model structure

```java
public class LiveMeShareInfo {

        // Video id
        private String videoId;
        
        // Broadcaster Name
        private String userName;
        
        // Source Type 1: live room 2: h5
        private int source;

        // Totle
        private String title;
        
        // Content
        private String content; 
        
        // Link url
        private String url; 
        
        // Broadcaster Avatar
        private String captureUrl;  
        
        // Type，1：Sharing from others，2：Sharing from myself
        private int type;  //Pictures
}
```

#### Delegate

* The developers implement the sharing function in this method.

```java
/**
 * Sharing proxy callback method
 * @param activity                  Content reference
 * @param liveMeShareInfo           Sharing data examples
 * @param iShareCallback            Sharing status callback
 **/
public void onShareClick(Activity activity, LiveMeShareInfo liveMeShareInfo, IShareCallback iShareCallback);
```

## <a name='5'></a>5、Push Notification

The SDK provides the custom push-notification function. Our server needs to call the access server to implement the push-notification function, including the functions of notifying private messages, sending a notification when the specific broadcasters have started a live broadcast, and the users can be directed to the live broadcast room by clicking the notification ect.

#### Publishing flowchart

<img src="https://dl.linkv.io/doc/en/android/live/images/push.png" alt="push" style="width:50%;" />

#### Message bodies

| Message field | description                                           |
| -------- | ---------------------------------------------- |
| type     | Message type 1, ordinary message. 2. Control messages. 3 System messages |
| msg_type | 1 text. 2 images 3 audio. 4 videos               |
| content  | Message content                                       |
| msg_id   | Message id                                         |
| time     | Message generated time                                   |

> 1. These message bodies are the examples, the specific message structure can be customized
> 2. The access server needs to develop a corresponding API for us to call

## <a name='6'></a>6、Event tracking

The SDK has already forwarded some key data points through delegate methods. The application developers can use it to report events if they need. If special data statistics are required, the SDK needs to be customized and developed accordingly.

#### Event tracking data types in transparent transmission

```java
//Transparent data model
public class KEWLDataTrackModel {

    // Watch broadcast
    public static final int DataTrackActiveWatchLive = 1;
    
    // Give gifts
    public static final int DataTrackActiveSendGift = 2;
    
    // Follow
    public static final int DataTrackActiveFollow = 3;
    
    // Home tab click
    public static final int DataTrackActiveTabClick = 4;
    
    // Leaderboard click
    public static final int DataTrackActiveRankClick = 5;
    
    // Use filter
    public static final int DataTrackActiveUseFilter = 6;
    
    // Hit the start button
    public static final int DataTrackActiveLiveClick = 7;
    
    // State of broadcast authorization
    public static final int DataTrackActiveRequestPermission = 8;
    
    // Start Live
    public static final int DataTrackActiveStartLive = 9;
    
    // Host sharing live broadcast
    public static final int DataTrackActiveBroadCasterShare = 10;
    
    // Modified personal information successfully
    public static final int DataTrackActiveProfileModifySucc = 11;
    
    // Pull stream success
    public static final int DataTrackActivePullStreamSucc = 12;
    
    // Send Comments
    public static final int DataTrackActiveSendComment = 13;
    
    // Click gifts panel
    public static final int DataTrackActiveGiftPanelClick = 14;
    
    // Send gifts successfully
    public static final int DataTrackActiveSendGiftSucc = 15;
    
    // Audience sharing live broadcast
    public static final int DataTrackActiveCustomerShare = 16;
    
    // Click follow on the list page
    public static final int DataTrackActiveRankPageFollowClick=17;
}
```

#### Data track models in transparent transmission

```java
public class KEWLDataTrackModel {

    // required
    // Report type
    public int type;
    
    // User id
    public String uid;
    
    // User Area
    public String user_area;

    // Watch Live
    // Live id
    public String watch_live_video_vid;
    
    // Broadcaster nickname
    public String watch_live_broadcaster_nick_name;
    
    // Broadcaster gender
    public String watch_live_broadcaster_gender;
    
    // Broadcaster age
    public String watch_live_broadcaster_age;

    // Send Gift
    // Gift id
    public String send_gift_id;
    
    // Gift price
    public String send_gift_price;

    // Follow/UnFollow
    // follow status，(Follow or unfollow)
    public boolean follow_is_follow;
    
    // Gender of interest
    public String follow_followers_gender;
    
    // Follower age
    public String follow_followers_age;

    // Pull stream id
    public String pull_stream_succ_vid;
    
    // Comment id
    public String send_comment_vid;
    
    // The id of the gift clicked on the gift panel
    public String panel_click_vid;
    
    // Gift id sent successfully
    public String send_gift_succ_gift_id;
    
    // Live stream id of successful gift
    public String send_gift_succ_vid;
    
    // Live stream id shared by viewers
    public String customer_share_vid;

    // Tab Click
    // Name of the tab that was clicked
    public String tab_click_tab_name;

    // User Filter
    // Filter name
    public String use_filter_filter_name;

    // Request Permission
    // request_permission_per_type = 1 Camera
    // request_permission_per_type = 2 Micro
    // Permission type（camera，microphone）
    public String request_permission_per_type;

    // Rank Page Follow Click
    // Click to follow or unfollow on the list page
    public boolean rank_page_follow_click_follow_status;
    
    // UID being followed in the list
    public String rank_page_follow_click_follow_uid;
}
```

#### The Report method

```java
/**
 * Data burying point management callback method
 * @param kewlDataTrackModel     Buried point data model
 **/
public void onDataTrack(KEWLDataTrackModel kewlDataTrackModel);
```

> In the reported data, the corresponding reported data field needs to be obtained according to the reported types, and the data field can be empty if there is an unrecognized type.

## <a name='7'></a>7、Interactive gameplay

The SDK provides basic live broadcast functions and customized services. There are also various interactive functions such as: group chatting, cross-room Head-to-Head mode, red pocket rain, treasure chest, etc.

<img src="https://dl.linkv.io/doc/en/android/live/images/live_config.jpg" alt="live_config" style="width:50%;" />

> These functions are the SDK buit-in functions, they can be enbled/disabled through the application control panel of the console.

## <a name='8'></a>8、The tools for the broadcasters

SDK provides the Beauty functions with various filters and stickers.

<img src="https://dl.linkv.io/doc/en/android/live/images/live_tool.jpg" alt="live_tool" style="width:50%;" />

> These functions are the SDK buit-in functions, they can be enbled/disabled through the application control panel of the console.

