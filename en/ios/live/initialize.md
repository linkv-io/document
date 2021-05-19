# Initialize 

**Update date：2020-08-19**

## 1、Overview

After the SDK integration is completed, it is necessary to apply for an account on the developer open platform, create an application, and obtain the APPID and secret required for SDK authentication before continuing to use.
## 2、Initialize

### 2.1 Create application

Please apply for appID and signature required by SDK authentication in [LinkV Developer background](http://dev.linkv.sg/), [Get AppID and AppSecret Guidelines](http://dev.linkv.sg/).
### 2.2 Initialize SDK


#### （1）Initialization process

1. Import LiveMeSDK.h in Appdelegate.m
2. Call the SDK initialization function in the startup method to set the SDK proxy object
3. Implement the agreePrivacyPolicyWithCompletion method in the proxy object
4. The application is released in the EU and needs to implement the hasAgreeGDPR method in the proxy object

#### （2）Call example

```
#import <LiveMeSDK/LiveMeSDK.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString *appid = @"";
    NSString *secret = @"";
    
    [[LiveMeSDK sharedInstance] startWithAppid:appid secret:secret];
    [LiveMeSDK sharedInstance].delegate = self;
    return YES;
}
```

### 2.3 Set up the official/test environment of the SDK

```
// Default is true
[[LiveMeSDK sharedInstance] setReleaseEnv:false];
```

## 3、Implement the necessary delegate method

```
/**
* orderId Order id
* source Order type
* success Order status
* coinCount Number of top-up coins
**/
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock{
    
}

/*
   Because the current privacy agreement authorization status will be verified in the live broadcast and start-up function，failure to obtain authorization will affect the use of features
，If you want to use all the functions in the SDK normally, you need to return the correct privacy agreement authorization status in agreePrivacyPolicyWithCompletion

    1.Watch live
    2.Live broadcast
 */
- (BOOL)agreePrivacyPolicyWithCompletion:(void (^)(BOOL hasAgree))completionBlock{
    return YES;
}

/// The token invalidation will call the SDK proxy method onTokenIsInvalid, and you need to log in again in the implementation of this method.

/// @param error Error code
- (void)onTokenIsInvalid:(NSError *)error {
    
}

/// Tab Select callback

/// @param page Number of pages

- (void)onHomePageSelected:(int)page {
    
}

/// Call back this function when the current user is blocked in the live broadcast room。
- (void)onUserBlock{
    
}

/// If the application is released in the European Union, it needs GDPR authorization. If the authorization fails, the live broadcast and launch functions are not available.
- (BOOL)hasAgreeGDPR {
    return YES;
}

/// Default gender of live streaming list

- (LMRequestGender)filterGender {
    return LMRequestGenderAll;
}
```

## 4、Add live data list view

```
    // Get live data VC
    UIViewController *liveListController = [[LiveMeSDK sharedInstance] featureListVC];
       liveListController.view.frame = CGRectMake(0, kNavBarAndStatusBarHeight, [UIScreen mainScreen].bounds.size.width, [UIScreen mainScreen].bounds.size.height-kNavBarAndStatusBarHeight);
    
    // Add to controller
    [self addChildViewController:liveListController];
    [self.view addSubview:liveListController.view];
```

