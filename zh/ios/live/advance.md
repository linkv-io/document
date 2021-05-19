# 进阶功能

**更新时间：2020-08-19**

## <a name='1'></a>1、概述

本章为进阶功能，部分功能属于定制化开发，可以通过官网的功能开关进行管理，包含主要功能如下：

- 私信
- 金融
- 分享
- 推送
- 数据埋点
- 互动玩法
- 主播工具

## <a name='2'></a>2、私信

提供两个聊天页面的入口，分别为私信列表和用户个人信息页面。可提供一对一聊天、群聊、陌生人消息、私信送礼等功能。

```
//调用该方法进入私信列表页面
[[LiveMeSDK sharedInstance] openMessageList];
```

> 1. 该方法会检测登录状态，登录成功IM配置完成之后才能成功收发消息
> 2. 可通过开放平台应用程序控制面板进行打开关闭该功能
> 3. 可以通过SDK代理方法updateChatUnReadNum获取未读消息通知

## <a name='3'></a>3、金融

SDK内含支付提现功能，可以通过SDK代理转发充值订单实现客户端充值功能，充值流程如下：

<img src="https://dl.linkv.io/doc/zh/ios/live/images/charge.png" alt="charge" style="width:50%;" />

#### 代理方法

```
/**
* orderId 订单id
* source 订单类型
* success 充值状态
* coinCount 充值金币数量
**/
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock;
```

#### 调用示例

```
- (void)onBuyCoinsWithOrderId:(NSString *)orderId source:(LMRechargeSource)source completion:(void (^)(BOOL success, NSInteger coinCount, NSString *orderId))completionBlock {
		//充值请求伪代码
		charge(BOOL success){
				completionBlock(success,coinCount,orderId)
		}
}
```

#### 参数解析

```
typedef NS_ENUM(NSInteger,LMRechargeSource) {
    LMRechargeSourcePersonalPage = 0,//个人信息页面充值
    LMRechargeSourceLiveRoom     = 1,//直播间礼物面板充值
};
```

* orderId
  * 订单id
* source 
  * 订单类型
* success
  * 充值状态
* coinCount
  * 充值金币数量

> 1. 可通过开放平台应用程序控制面板进行打开关闭该功能
> 2. 金融开关内容包括充值提现入口，礼物功能，榜单功能。如果关闭该功能直播间不会展示礼物面板，个人页面不会展示钻石相关信息，屏蔽充值提前入口，屏蔽榜单入口

## <a name='4'></a>4、分享

支持多渠道分享，通过代理进行数据转发满足客户端分享功能，SDK只提供分享所需要的数据，分享操作需要在客户端进行，接入方需要申请相应的分享平台账号，进行相应的工程设置。

#### 分享支持类型

```
// 分享支持文本、图片、视频三种媒体格式
typedef NS_ENUM(NSInteger, CMLShareContentType){
    
    CMLShareContentTypeNormal,
    CMLShareContentTypeImage,
    CMLShareContentTypeVideo,
};
```

#### 分享数据model结构

```
@interface LMVideoShareContent : CMLShareContent
@property (nonatomic, strong) NSString *vid;//媒体id
@property (nonatomic, strong) NSString *streamerName;//主播名字
@property (nonatomic, assign) NSInteger sourceType;//资源类型
@end

@interface CMLShareContent : NSObject
@property (nonatomic, copy) NSString *subject; //标题
@property (nonatomic, copy) NSString *content; //内容
@property (nonatomic, copy) NSString *contentURL; //链接url
@property (nonatomic, copy) NSString *imageURL;  //图片链接
@property (nonatomic, strong) UIImage *image;  //图片
@property (nonatomic, strong) NSURL  *videoUrl;  //视频url
@property (nonatomic, assign) CMLShareContentType type; //分享媒体类型
@property (nonatomic, assign) BOOL cancelInsWaterMark; //取消水印
@property (nonatomic, assign) BOOL cancelInsTipFrame; //取消ins弹框
@end
```

#### 代理方法

* 接入方实现此代理方法，在此代理方法中实现分享功能。

```
/**
* @desc 分享代理回调方法
* @param shareContent 分享数据实例
* @param superView 分享面板展示容器视图
**/
- (void)shareWithContent:(LMVideoShareContent *)shareContent superView:(UIView *)superView;
```

## <a name='5'></a>5、推送

SDK提供自定义推送功能，需要由我方服务端调用接入方服务端实现相关推送，可实现主播开播提示发送通知，点击通知栏进入直播间，私信消息通知等功能。

#### 推送流程图

<img src="https://dl.linkv.io/doc/zh/ios/live/images/push.png" alt="push" style="width:50%;" />

#### 消息体示例

| 消息字段 | 描述                                           |
| -------- | ---------------------------------------------- |
| type     | 消息类型 1，普通消息。2，控制类消息。3系统消息 |
| msg_type | 1文本。2图片。3音频。4视频                     |
| content  | 消息内容                                       |
| msg_id   | 消息id                                         |
| time     | 消息生成时间                                   |

> 1. 此消息体为示例，具体消息结构可自定义
> 2. 接入方服务端需要开发相应的推送接口供我方调用

## <a name='6'></a>6、数据埋点

SDK目前已经通过代理方法对一些关键的数据点位进行了数据转发，接入方客户端可以酌情进行上报，如果需要特殊的数据统计需要SDK进行相应的定制开发。

#### 透传数据埋点类型

```
//透传数据模型
typedef NS_ENUM(NSInteger, DataTrackType) {
    DataTrackActiveWatchLive = 1,//看播
    DataTrackActiveSendGift = 2,//送礼
    DataTrackActiveFollow = 3,//关注
    DataTrackActiveTabClick = 4,//首页tab点击
    DataTrackActiveRankClick = 5,//排行榜点击
    DataTrackActiveUseFilter = 6,//使用滤镜
    DataTrackActiveLiveClick = 7,//点击开播按钮
    DataTrackActiveRequestPermission = 8,//开播权限授权状态
    DataTrackActiveStartLive = 9,//开始直播
    DataTrackActiveBroadCasterShare = 10,//主播分享直播
    DataTrackActiveProfileModifySucc = 11,//成功修改个人信息
    DataTrackActivePullStreamSucc = 12,//拉流成功
    DataTrackActiveSendComment = 13,//发送评论
    DataTrackActiveGiftPanelClick = 14,//点击礼物面板
    DataTrackActiveSendGiftSucc = 15,//送礼成功
    DataTrackActvieCustomerShare = 16,//观众分享直播
    DataTrackActiveRankPageFollowClick = 17,//榜单页点击关注
};
```

#### 透传数据模型类

```

@interface KEWLDataTrackModel : NSObject

// required
@property (nonatomic, assign) DataTrackType type;//上报类型
@property (nonatomic, copy) NSString *uid;//用户id
@property (nonatomic, copy) NSString *user_area;//用户区域

// Watch Live
@property (nonatomic, copy) NSString *watch_live_video_vid;//直播id
@property (nonatomic, copy) NSString *watch_live_broadcaster_nick_name;//主播昵称
@property (nonatomic, copy) NSString *watch_live_broadcaster_gender;//主播性别
@property (nonatomic, copy) NSString *watch_live_broadcaster_age;//主播年龄

// Send Gift
@property (nonatomic, copy) NSString *send_gift_id;//礼物id
@property (nonatomic, copy) NSString *send_gift_price;//礼物价格

// Follow/UnFollow
@property (nonatomic, assign) BOOL follow_is_follow;//follow状态，(关注还是取消关注)
@property (nonatomic, copy) NSString *follow_followers_gender;//被关注性别
@property (nonatomic, copy) NSString *follow_followers_age;//被关注年龄

@property (nonatomic, copy) NSString *pull_stream_succ_vid;//拉流的流id
@property (nonatomic, copy) NSString *send_comment_vid;//评论id
@property (nonatomic, copy) NSString *panel_click_vid;//礼物面板点击的礼物id
@property (nonatomic, copy) NSString *send_gift_succ_gift_id;//成功送出的礼物id
@property (nonatomic, copy) NSString *send_gift_succ_vid;//成功送礼的直播id
@property (nonatomic, copy) NSString *customer_share_vid;//被观众分享的直播id

// Tab Click
@property (nonatomic, copy) NSString *tab_click_tab_name;//被点击的tab名字

// User Filter
@property (nonatomic, copy) NSString *use_filter_filter_name;//滤镜名字

// Request Permission
// request_permission_per_type = 1 Camera
// request_permission_per_type = 2 Micro
@property (nonatomic, copy) NSString *request_permission_per_type;//权限类型（摄像头，麦克风）

// Rank Page Follow Click
@property (nonatomic, assign) BOOL rank_page_follow_click_follow_status;//榜单页面点击关注还是取消关注
@property (nonatomic, copy) NSString *rank_page_follow_click_follow_uid;//榜单中被关注的uid
@end
```

#### 上报方法

```
//此方法中进行数据上报
- (void)onDataTrack:(KEWLDataTrackModel *)dataTrackModel {
    //上报 dataTrackModel内容
}
```

> 上报的数据中需要根据上报的类型获取对应的上报数据字段，非此类型下的数据字段可能为空。

## <a name='7'></a>7、互动玩法

SDK提供基础的直播功能和定制化服务外，也有丰富的交互功能如：多人连麦，PK,红包雨，抢宝箱等。

<img src="https://dl.linkv.io/doc/zh/ios/live/images/live_config.jpg" alt="live_config" style="width:50%;" />

> 该功能为SDK内置功能，可通过开放平台应用程序控制面板进行打开关闭该功能。

## <a name='8'></a>8、主播工具

SDK提供美颜滤镜和贴纸功能

<img src="https://dl.linkv.io/doc/zh/ios/live/images/live_tool.jpg" alt="live_tool" style="width:50%;" />

> 该功能为SDK内置功能，可通过开放平台应用程序控制面板进行打开关闭该功能。

