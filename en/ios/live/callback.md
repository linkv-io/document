# Callback Sample

**Update date：2020-08-19**

## <a name='1'></a>1、Overview

The callback functions includes the functions of recharging, sharing, privacy authorization and other related callbacks, you need to set the singleton delegate object of the LiveMeSDK to receive and process delegate callback.

## <a name='2'></a>2、Set up the delegate

``` 
 [LiveMeSDK sharedInstance].delegate = delegateObject;
```

## <a name='3'></a>3、Event

#### （1）Recharging

``` 
/**
* orderId Orderid
* source Order type
* success payment status
* coinCount the amount of coins recharged
**/
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock;
```

#### （2）Sharing

``` 
/**
* @desc the sharing delegation callback
* @param shareContent the sharing content
* @param superView THe container view of sharing pannel display
**/
- (void)shareWithContent:(LMVideoShareContent *)shareContent superView:(UIView *)superView;
```

#### （3）Event tracking

``` 
/**
* @desc Event tracking delegation callback
* @param dataTrackModel Event tracking instance
**/
- (void)onDataTrack:(KEWLDataTrackModel *)dataTrackModel；
```

#### （4）Privacy agreement authorization

``` 
/**
* hasAgree Whether to agree to the privacy policy
**/
- (BOOL)agreePrivacyPolicyWithCompletion:(void (^)(BOOL hasAgree))completionBlock;
```

> Whether to authorize the privacy policy.

#### （5）GDPR authorization status

``` 
- (BOOL)hasAgreeGDPR;
```

> If the application is published in the EU, GDPR authorization is required. If the authorization fails, the functions of live broadcast and starting the broadcast will be unavailable.

#### （6）Invalid Token

``` 
- (void)onTokenIsInvalid:(NSError *)error;
```

> This function is called when the client token is invalid and notifying the client to re-authenticate.

#### （7）The user is blocked

``` 
- (void)onUserBlock;
```

> This function is called when the current user is blocked out of the live broadcast room.

#### （8）Red-dot update for the private messages

``` 
/**
* number Unread messages
**/
- (void)updateChatUnReadNum:(NSInteger)number;
```

> The prompt for unread private messages. Call this function when there is a new message.

#### （9）The default gender of the live broadcast list

``` 
/**
* return gender
**/
- (LMRequestGender)filterGender;
```

> The live broadcast list is filtered by gender and set as default.
>
> LMRequestGenderFemale = 3, //female
>
> LMRequestGenderMale  = 2, //male
>
> LMRequestGenderAll  = 1, //all

