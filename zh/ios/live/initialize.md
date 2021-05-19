# 初始化

**更新时间：2020-08-19**

## <a name='1'></a>1、概述

集成 SDK 完成后，需要在开发者开放平台申请账号、创建应用并获取SDK鉴权需要的appid 和 secret才能继续使用。

## <a name='2'></a>2、初始化

### <a name='2.1'></a>2.1 创建应用

请在 [LinkV 开发者后台](http://dev.linkv.io/) 申请 SDK 鉴权需要的 appid 和 签名，[获取 AppID 和 AppSecret 指引](http://dev.linkv.io/)。

### <a name='2.2'></a>2.2 初始化SDK

#### （1）初始化流程

1. 在Appdelegate.m导入LiveMeSDK.h
2. 在启动方法中调用SDK初始化函数，设置SDK代理对象
3. 在代理对象中实现agreePrivacyPolicyWithCompletion方法
4. 应用在欧盟发布同时需要在代理对象中实现hasAgreeGDPR方法

#### （2）调用示例

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

### <a name='2.3'></a>2.3 设置 SDK 的 正式/测试 环境

```
// 默认为 true
[[LiveMeSDK sharedInstance] setReleaseEnv:false];
```

## <a name='3'></a>3、实现 必备 delegate 方法

```
/**
* orderId 订单id
* source 订单类型
* success 充值状态
* coinCount 充值金币数量
**/
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock{
    
}

/*
   因为在观看直播和开播功能中会对当前的隐私协议授权状态做校验，没有得到授权会影响功能的使用，如果想要正常使用SDK中的全部功能需要在agreePrivacyPolicyWithCompletion返回正确的隐私协议授权状态
    1.觀看直播
    2.直播
 */
- (BOOL)agreePrivacyPolicyWithCompletion:(void (^)(BOOL hasAgree))completionBlock{
    return YES;
}

/// token失效会调用SDK代理方法onTokenIsInvalid，需要在该方法的实现中重新登录。
/// @param error 错误码
- (void)onTokenIsInvalid:(NSError *)error {
    
}

/// Tab 选择回调
/// @param page 页数
- (void)onHomePageSelected:(int)page {
    
}

/// 当前用户在直播间被拉黑时回调此函数。
- (void)onUserBlock{
    
}

/// 如果应用在欧盟地区发布，需要GDPR授权，如果授权失败，直播和开播功能不可用。
- (BOOL)hasAgreeGDPR {
    return YES;
}

/// 直播列表默认性别
- (LMRequestGender)filterGender {
    return LMRequestGenderAll;
}
```

## <a name='4'></a>4、添加直播数据列表视图

```
    // 获取直播数据 VC
    UIViewController *liveListController = [[LiveMeSDK sharedInstance] featureListVC];
       liveListController.view.frame = CGRectMake(0, kNavBarAndStatusBarHeight, [UIScreen mainScreen].bounds.size.width, [UIScreen mainScreen].bounds.size.height-kNavBarAndStatusBarHeight);
    
    // 添加到控制器中
    [self addChildViewController:liveListController];
    [self.view addSubview:liveListController.view];
```

