# Advanced features

**Update date：2020-08-19**

## <a name='1'></a>1、Overview

Some advanced features are customized developments, it can be disabled or enabled through the official website, including the main functions are as follows:

* Private messaging
* Finance
* Sharing
* Push notification
* Event tracking
* Interactive gameplay
* Broadcaster tools

## <a name='2'></a>2、Private messaging

It provides the access to two chat pages, which are the private message list and the user's personal information page. It can provide the users with the functions of one-to-one chat, group chat, receiving the stranger's messages, private message and others.

``` 
//call this method to access to the list of private message
[[LiveMeSDK sharedInstance] openMessageList];
```

> 1. This method will detect the login status, and the message can only be sent and received after the IM configuration is completed.
> 2. The function can be enabled or disabled through the application control panel of the console.
> 3. You can receive the notification of the unread messages through the SDK delegate method of updateChatUnReadNum.

## <a name='3'></a>3、Finance

The SDK provides the withdrawal function, which can be used to forward the recharge orders through the SDK delegate to implement the client recharge function. The recharge process is as follows:

<img src="https://dl.linkv.io/doc/en/ios/live/images/charge.png" alt="charge" style="width:50%; " />

#### Delegate

``` 
/**
* orderId
* source order type
* success recharge status
* coinCount the recharge amount of coins
**/
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock;
```

#### Example

``` 
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock {

		//pseudocode of the recharge request
		charge(BOOL success){
				completionBlock(success,coinCount,orderId)
		}
}
```

#### Parameter parsing

``` 
typedef NS_ENUM(NSInteger,LMRechargeSource) {
    LMRechargeSourcePersonalPage = 0,//personal recharge information page
    LMRechargeSourceLiveRoom     = 1,//the recharge information page in the Live broadcast room
};
```

* orderId
  * Order id
* source 
  * Order Type
* success
  * Recharge status
* coinCount
  * Recharge amount of coins

> 1. The function can be disabled/enabled through the application control panel of the console.
> 2. The financial contents include the access of the withdrawal function, the functions of gifting and leaderboard. If this function is disabled, the live broadcasts room will not display the gifts panel, and the diamond-related information will not be shown on the profile pages. Additionally, the access to leaderboard functions, the recharge and withdrawal functions will be hidden. 

## <a name='4'></a>4、Sharing

Supporting multi-channel sharing and data forwarding through the delegates to meet the client's demands on sharing function, SDK only provides the data required for sharing, the sharing operation needs to be performed by the clients, and the developers need to apply for the account of corresponding sharing platforms to process the corresponding project settings.

#### Sharing support type

``` 
// support the texts,images and video sharing.
typedef NS_ENUM(NSInteger, CMLShareContentType){
    
    CMLShareContentTypeNormal,
    CMLShareContentTypeImage,
    CMLShareContentTypeVideo,
};
```

#### Shared data model structure

``` 
@interface LMVideoShareContent : CMLShareContent
@property (nonatomic, strong) NSString *vid;//media id
@property (nonatomic, strong) NSString *streamerName;//broadcaster's name
@property (nonatomic, assign) NSInteger sourceType;//source type
@end

@interface CMLShareContent : NSObject
@property (nonatomic, copy) NSString *subject; //title
@property (nonatomic, copy) NSString *content; //content
@property (nonatomic, copy) NSString *contentURL; //
@property (nonatomic, copy) NSString *imageURL;  //
@property (nonatomic, strong) UIImage *image;  //
@property (nonatomic, strong) NSURL  *videoUrl;  //
@property (nonatomic, assign) CMLShareContentType type; //content type
@property (nonatomic, assign) BOOL cancelInsWaterMark; //cancel the ins watermark
@property (nonatomic, assign) BOOL cancelInsTipFrame; //cancel the ins tip frame.
@end
```

#### Delegate

* The developers implement the sharing function in this method.

``` 
/**
* @desc the sharing delegate callback
* @param shareContent 
* @param superView the container view for the sharing panel display
**/
- (void)shareWithContent:(LMVideoShareContent *)shareContent superView:(UIView *)superView;
```

## <a name='5'></a>5、Push Notification

The SDK provides the custom push-notification function. Our server needs to call the access server to implement the push-notification function, including the functions of notifying private messages, sending a notification when the specific broadcasters have started a live broadcast, and the users can be directed to the live broadcast room by clicking the notification ect.

#### Publishing flowchart

<img src="https://dl.linkv.io/doc/en/ios/live/images/push.png" alt="push" style="width:50%; " />

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

``` 
//
typedef NS_ENUM(NSInteger, DataTrackType) {
    DataTrackActiveWatchLive = 1,//watching
    DataTrackActiveSendGift = 2,//gifting
    DataTrackActiveFollow = 3,//following
    DataTrackActiveTabClick = 4,//the home page tab click
    DataTrackActiveRankClick = 5,//the leaderboard click
    DataTrackActiveUseFilter = 6,//use the filters
    DataTrackActiveLiveClick = 7,//click to start the broadcast
    DataTrackActiveRequestPermission = 8,//permission status of starting the broadcast
    DataTrackActiveStartLive = 9,//start the broadcast
    DataTrackActiveBroadCasterShare = 10,//sharing the broadcast by the host
    DataTrackActiveProfileModifySucc = 11,//sucessfully to modify the profile information
    DataTrackActivePullStreamSucc = 12,//succesfully to play the streams
    DataTrackActiveSendComment = 13,//send the comments
    DataTrackActiveGiftPanelClick = 14,//Click the gifts panel
    DataTrackActiveSendGiftSucc = 15,//gifted successfully
    DataTrackActvieCustomerShare = 16,//sharing the broadcast by the audience
    DataTrackActiveRankPageFollowClick = 17,//Click to follow the users on the leaderboard
};
```

#### Data track models in transparent transmission

``` 

@interface KEWLDataTrackModel : NSObject

// required
@property (nonatomic, assign) DataTrackType type;// the report type
@property (nonatomic, copy) NSString *uid;//User ID
@property (nonatomic, copy) NSString *user_area;//Users area/location

// Watch Live
@property (nonatomic, copy) NSString *watch_live_video_vid;//Romm ID
@property (nonatomic, copy) NSString *watch_live_broadcaster_nick_name;//the broadcaster's mick name
@property (nonatomic, copy) NSString *watch_live_broadcaster_gender;//broadcaster's gender
@property (nonatomic, copy) NSString *watch_live_broadcaster_age;//age

// Send Gift
@property (nonatomic, copy) NSString *send_gift_id;//gift ID
@property (nonatomic, copy) NSString *send_gift_price;//Gift price

// Follow/UnFollow
@property (nonatomic, assign) BOOL follow_is_follow;//follow/unfollow
@property (nonatomic, copy) NSString *follow_followers_gender;//the gender of the person being followed
@property (nonatomic, copy) NSString *follow_followers_age;//the age of the person being followed

@property (nonatomic, copy) NSString *pull_stream_succ_vid;//Play-streams ID
@property (nonatomic, copy) NSString *send_comment_vid;//Comment ID
@property (nonatomic, copy) NSString *panel_click_vid;//the clicked gift Id on the gift panel
@property (nonatomic, copy) NSString *send_gift_succ_gift_id;//the sent gift ID
@property (nonatomic, copy) NSString *send_gift_succ_vid;//the live broadcast id that the gift has been sent successfully
@property (nonatomic, copy) NSString *customer_share_vid;//the shared Live broadcast id by the audience

// Tab Click
@property (nonatomic, copy) NSString *tab_click_tab_name;//the clicked tab name

// User Filter
@property (nonatomic, copy) NSString *use_filter_filter_name;//filter name

// Request Permission
// request_permission_per_type = 1 Camera
// request_permission_per_type = 2 Micro
@property (nonatomic, copy) NSString *request_permission_per_type;//peimisssion type(camera/microphone)

// Rank Page Follow Click
@property (nonatomic, assign) BOOL rank_page_follow_click_follow_status;//click to follow/unfollow from the rank page
@property (nonatomic, copy) NSString *rank_page_follow_click_follow_uid;//the followed IUD onon the rank page
@end
```

#### The Report method

``` 
//use this method to process the data report.
- (void)onDataTrack:(KEWLDataTrackModel *)dataTrackModel {
    //上报 dataTrackModel内容
}
```

> In the reported data, the corresponding reported data field needs to be obtained according to the reported types, and the data field can be empty if there is an unrecognized type.

## <a name='7'></a>7、Interactive gameplay

The SDK provides basic live broadcast functions and customized services. There are also various interactive functions such as: group chatting, cross-room Head-to-Head mode, red pocket rain, treasure chest, etc.

<img src="https://dl.linkv.io/doc/en/ios/live/images/live_config.jpg" alt="live_config" style="width:50%; " />

> These functions are the SDK buit-in functions, they can be enbled/disabled through the application control panel of the console.

## <a name='8'></a>8、The tools for the broadcasters

SDK provides the Beauty functions with various filters and stickers.

<img src="https://dl.linkv.io/doc/en/ios/live/images/live_tool.jpg" alt="live_tool" style="width:50%; " />

> These functions are the SDK buit-in functions, they can be enbled/disabled through the application control panel of the console.

