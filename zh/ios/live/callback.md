# 接口回调示例

**更新时间：2020-08-19**

## <a name='1'></a>1、概述

接口回调，包含充值，分享，隐私授权等相关回调，需要设置 LiveMeSDK 单例的 delegate 对象进行接收和处理代理回调事件。

## <a name='2'></a>2、设置代理

```
 [LiveMeSDK sharedInstance].delegate = delegateObject;
```

## <a name='3'></a>3、代理事件

#### （1）充值

```
/**
* orderId 订单id
* source 订单类型
* success 充值状态
* coinCount 充值金币数量
**/
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock;
```

#### （2）分享

```
/**
* @desc 分享代理回调方法
* @param shareContent 分享数据实例
* @param superView 分享面板展示容器视图
**/
- (void)shareWithContent:(LMVideoShareContent *)shareContent superView:(UIView *)superView;
```

#### （3）数据埋点

```
/**
* @desc 数据埋点代理回调方法
* @param dataTrackModel 埋点数据实例
**/
- (void)onDataTrack:(KEWLDataTrackModel *)dataTrackModel；
```

#### （4）隐私协议授权

```
/**
* hasAgree 是否同意隐私条款
**/
- (BOOL)agreePrivacyPolicyWithCompletion:(void (^)(BOOL hasAgree))completionBlock;
```

> 是否授权隐私条款协议。

#### （5）GDPR授权状态

```
- (BOOL)hasAgreeGDPR;
```

> 如果应用在欧盟地区发布，需要GDPR授权，如果授权失败，直播和开播功能不可用。

#### （6）Token失效

```
- (void)onTokenIsInvalid:(NSError *)error;
```

> 当客户端token失效时调用此函数通知客户端重新鉴权。

#### （7）用户被拉黑

```
- (void)onUserBlock;
```

> 当前用户在直播间被拉黑时回调此函数。

#### （8）私信消息红点更新

```
/**
* number 未读消息数
**/
- (void)updateChatUnReadNum:(NSInteger)number;
```

> 私信未读消息提示，当有新的消息时回调此函数。

#### （9）直播列表默认性别

```
/**
* return 性别
**/
- (LMRequestGender)filterGender;
```

> 直播列表默认筛选性别
>
> LMRequestGenderFemale = 3, //女
>
> LMRequestGenderMale  = 2, //男
>
> LMRequestGenderAll  = 1, //全部

