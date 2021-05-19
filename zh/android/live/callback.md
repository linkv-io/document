# 接口回调示例

**更新时间：2020-08-19**

## <a name='1'></a>1、概述

接口回调，包含充值，分享，隐私授权等相关回调，需要设置 LiveSDK 单例的 LiveMeLiveInterface 对象进行接收和处理代理回调事件。

## <a name='2'></a>2、设置监听

```java
//设置回调
LiveMeClient.getInstance().setLiveMeInterface(new LiveMeImpl());
```

## <a name='3'></a>3、监听事件

#### （1）充值

```java
/**
 * 充值接口
 * @param activity              调用此方法的所在activity
 * @param source                订单类型
 * @param requestCode           请求code
 * @param orderId               订单ID
 **/
public void onBuyGold(Activity activity,int source,int requestCode,String orderId);
```

#### （2）分享

```java
/**
 * 分享监听方法
 * @param activity                  调用此方法所在的activity
 * @param liveMeShareInfo           分享数据
 * @param iShareCallback            分享监听
 **/
public void onShareClick(Activity activity, LiveMeShareInfo liveMeShareInfo, IShareCallback iShareCallback);
```

#### （3）数据埋点

```java
/**
 * 数据埋点理回调方法
 * @param kewlDataTrackModel     埋点数据model
 **/
public void onDataTrack(KEWLDataTrackModel kewlDataTrackModel);
```

#### （4）隐私协议授权

```java
/**
 * 隐私协议授权回调
 * @param activity              调用隐私授权的activity
 * @param confirmCallback       授权回调
 **/
public void onVideoClick(Activity activity, OnTermConfirmCallback confirmCallback);
```

> 是否授权隐私条款协议，

#### （5）GDPR授权状态

```java
public interface OnTermConfirmCallback {
    void onTermConfirm(boolean confirm);
}
```

> 如果应用在欧盟地区发布，需要GDPR授权，如果授权失败直播和开播功能不可用

#### （6）Token失效

```java
public interface TokenCallback {

    // Token失效
    void onTokenExpire(String var1, int var2, String var3);

}
```

> 当客户端token失效时调用此函数通知客户端重新鉴权

#### （7）用户被拉黑

```java
public interface TokenCallback {

    // 用户被拉黑
    void onTokenExpire(String var1, int var2, String var3);

}
```

> 当前用户在直播间被拉黑时回调此函数

#### （8）私信消息红点更新

```java
/**
 * 监听未读消息数的接口
 * @param unReadNum         未读消息数
 **/
public interface UnReadListener {
    public void updateNum(int unReadNum);
}
```

> 私信未读消息提示，当有新的消息时回调此函数

#### （9）直播列表默认性别

> 直播列表默认筛选性别
>
> public static final String MALE = "1"; //男
>
> public static final String FAMALE = "0"; //女
>
> public static final String SECRET = "-1", //全部
