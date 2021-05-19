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

```java
/**
 * 调用该方法进入私信列表页面
 * @param activity          上下文引用
 * @param requestCode       请求code
 * @param hostInfo          表示会话信息和用户信息
 * @param from              记录上一个页面的信息（从哪个页面来）
 */
LiveMeClient.getInstance().getLiveMeInterface().openLetterAct(activity, requestCode, hostInfo, from);
```

> 1. 该方法会检测登录状态，登录成功IM配置完成之后才能成功收发消息
> 2. 可通过开放平台应用程序控制面板进行打开关闭该功能
> 3. 可以通过SDK回调方法updateNum获取未读消息通知

## <a name='3'></a>3、金融

SDK内含支付提现功能，可以通过SDK代理转发充值订单实现客户端充值功能，充值流程如下：

<img src="https://dl.linkv.io/doc/zh/android/live/images/charge.png" alt="charge" style="width:50%;" />

#### 接口方法

```java
/**
* activity              调用此方法的所在activity
* source                订单类型
* requestCode           请求code
* orderId               订单ID
**/
public void onBuyGold(Activity activity,int source,int requestCode,String orderId);
```

- activity
  - 调用此方法的所在activity
- source 
  - 订单类型
- requestCode
  - 请求code
- orderId
  - 订单ID

> 1. 可通过开放平台应用程序控制面板进行打开关闭该功能
> 2. 金融开关内容包括充值提现入口，礼物功能，榜单功能。如果关闭该功能直播间不会展示礼物面板，个人页面不会展示钻石相关信息，屏蔽充值提前入口，屏蔽榜单入口



## <a name='4'></a>4、分享

支持多渠道分享，通过代理进行数据转发满足客户端分享功能，SDK只提供分享所需要的数据，分享操作需要在客户端进行，接入方需要申请相应的分享平台账号，进行相应的工程设置。


#### 分享数据model结构

```java
public class LiveMeShareInfo {

        // 媒体id
        private String videoId;
        
        // 主播名字
        private String userName;
        
        // 资源类型, 1: live room 2: h5
        private int source;

        // 标题
        private String title;
        
        // 内容
        private String content; 
        
        // 链接url
        private String url; 
        
        // 播主头像
        private String captureUrl;  
        
        // 类型，1：分享来自于其他人，2：分享来自于自己
        private int type;  //图片
}
```

#### 监听方法

* 接入方实现此监听方法，在此监听方法中实现分享功能。

```java
/**
 * 分享代理回调方法
 * @param activity                  上下文引用
 * @param liveMeShareInfo           分享数据实例
 * @param iShareCallback            分享状态回调
 **/
public void onShareClick(Activity activity, LiveMeShareInfo liveMeShareInfo, IShareCallback iShareCallback);
```

## <a name='5'></a>5、推送

SDK提供自定义推送功能，需要由我方服务端调用接入方服务端实现相关推送，可实现主播开播提示发送通知，点击通知栏进入直播间，私信消息通知等功能。

#### 推送流程图

<img src="https://dl.linkv.io/doc/zh/android/live/images/push.png" alt="push" style="width:50%;" />

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

```java
//透传数据模型
public class KEWLDataTrackModel {

    // 看播
    public static final int DataTrackActiveWatchLive = 1;
    
    // 送礼
    public static final int DataTrackActiveSendGift = 2;
    
    // 关注
    public static final int DataTrackActiveFollow = 3;
    
    // 首页tab点击
    public static final int DataTrackActiveTabClick = 4;
    
    // 排行榜点击
    public static final int DataTrackActiveRankClick = 5;
    
    // 使用滤镜
    public static final int DataTrackActiveUseFilter = 6;
    
    // 点击开播按钮
    public static final int DataTrackActiveLiveClick = 7;
    
    // 开播权限授权状态
    public static final int DataTrackActiveRequestPermission = 8;
    
    // 开始直播
    public static final int DataTrackActiveStartLive = 9;
    
    // 主播分享直播
    public static final int DataTrackActiveBroadCasterShare = 10;
    
    // 成功修改个人信息
    public static final int DataTrackActiveProfileModifySucc = 11;
    
    // 拉流成功
    public static final int DataTrackActivePullStreamSucc = 12;
    
    // 发送评论
    public static final int DataTrackActiveSendComment = 13;
    
    // 点击礼物面板
    public static final int DataTrackActiveGiftPanelClick = 14;
    
    // 送礼成功
    public static final int DataTrackActiveSendGiftSucc = 15;
    
    // 观众分享直播
    public static final int DataTrackActiveCustomerShare = 16;
    
    // 榜单页点击关注
    public static final int DataTrackActiveRankPageFollowClick=17;
}
```

#### 透传数据模型类

```java
public class KEWLDataTrackModel {

    // required
    // 上报类型
    public int type;
    
    // 用户id
    public String uid;
    
    // 用户区域
    public String user_area;

    // Watch Live
    // 直播id
    public String watch_live_video_vid;
    
    // 主播昵称
    public String watch_live_broadcaster_nick_name;
    
    // 主播性别
    public String watch_live_broadcaster_gender;
    
    // 主播年龄
    public String watch_live_broadcaster_age;

    // Send Gift
    // 礼物id
    public String send_gift_id;
    
    // 礼物价格
    public String send_gift_price;

    // Follow/UnFollow
    // follow状态，(关注还是取消关注)
    public boolean follow_is_follow;
    
    // 被关注性别
    public String follow_followers_gender;
    
    // 被关注年龄
    public String follow_followers_age;

    // 拉流的流id
    public String pull_stream_succ_vid;
    
    // 评论id
    public String send_comment_vid;
    
    // 礼物面板点击的礼物id
    public String panel_click_vid;
    
    // 成功送出的礼物id
    public String send_gift_succ_gift_id;
    
    // 成功送礼的直播id
    public String send_gift_succ_vid;
    
    // 被观众分享的直播id
    public String customer_share_vid;

    // Tab Click
    // 被点击的tab名字
    public String tab_click_tab_name;

    // User Filter
    // 滤镜名字
    public String use_filter_filter_name;

    // Request Permission
    // request_permission_per_type = 1 Camera
    // request_permission_per_type = 2 Micro
    // 权限类型（摄像头，麦克风）
    public String request_permission_per_type;

    // Rank Page Follow Click
    // 榜单页面点击关注还是取消关注
    public boolean rank_page_follow_click_follow_status;
    
    // 榜单中被关注的uid
    public String rank_page_follow_click_follow_uid;
}
```

#### 上报方法

```java
/**
 * 数据埋点理回调方法
 * @param kewlDataTrackModel     埋点数据model
 **/
public void onDataTrack(KEWLDataTrackModel kewlDataTrackModel);
```

> 上报的数据中需要根据上报的类型获取对应的上报数据字段，非此类型下的数据字段可能为空

## <a name='7'></a>7、互动玩法

SDK提供基础的直播功能和定制化服务外，也有丰富的交互功能如：多人连麦，PK,红包雨，抢宝箱等。

<img src="https://dl.linkv.io/doc/zh/android/live/images/live_config.jpg" alt="live_config" style="width:50%;" />

> 该功能为SDK内置功能，可通过开放平台应用程序控制面板进行打开关闭该功能。

## <a name='8'></a>8、主播工具

SDK提供美颜滤镜和贴纸功能

<img src="https://dl.linkv.io/doc/zh/android/live/images/live_tool.jpg" alt="live_tool" style="width:50%;" />

> 该功能为SDK内置功能，可通过开放平台应用程序控制面板进行打开关闭该功能。