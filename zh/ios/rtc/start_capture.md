# 摄像头采集

## <a name='1'></a>1、概述

在开始推流之前，如果要推本地手机的音视频流，那么需要设置开启摄像头捕获，采集摄像头流。


## <a name='3'></a>3、步骤

### 代码示例

1. 首先需要调用 LVRTCEngine 单例的 startCapture 方法设置开启采集本地摄像头。

```objc
// 设置开启采集本地摄像头
[[LVRTCEngine sharedInstance] startCapture];
```

2. 然后创建 视频数据预览视图 LVRTCDisplayView，并指定其  frame 大小, 预览视图的填充模式。

```objc
// LVRTCDisplayView 为预览视图。
LVRTCDisplayView *mainPreview = [[LVRTCDisplayView alloc] initWithFrame:[UIScreen mainScreen].bounds];
// 设置预览视图填充模式
mainPreview.viewContentMode = LVViewContentModeScaleAspectFill;
```

3. 为音视频设置添加预览视图，并且不指定 uid（不指定 uid 默认使用登录房间的 uid）这样摄像头采集的数据就会渲染到此视图。

```objc
// 添加预览视图到当前视图
[self.view addSubview:mainPreview];

// 为音视频设置预览视图 （SDK内部会自动将视图和接收到的音视频数据进行绑定操作，不设置音视频流会无法与视图绑定并进行渲染）
[[LVRTCEngine sharedInstance] addDisplayView:mainPreview];
```

> 然后做完以上操作后，本地摄像头的数据就会 渲染到  LVRTCDisplayView 上进行显示。

## <a name='4'></a>4、详细说明

#### addDisplayView 方法 （为音视频设置预览视图方法）

* 开启采集本地摄像头之后， addDisplayView 添加视图后， SDK 内部才会自动将视图和音视频数据进行绑定渲染操作。

* 如果想要移除预览视图，那么可以调用 removeDisplayView 方法可以移除对应的预览视图，在调用之前可以 stopPlayingStream 停止播放对应的流。

```objc
// 为音视频设置预览视图，请先加入房间后再进行设置，SDK 内部会自动将视图和接收到的音视频数据进行绑定操作
// @param view 视图信息
// @discussion 如果不传 uid 则该视图默认为当前登录用户
- (void)addDisplayView:(LVRTCDisplayView *)view;

// 移除预览视图
// @param view 视图信息
-(void)removeDisplayView:(LVRTCDisplayView *)view;
```

#### LVRTCDisplayView  类（视频数据显示类）

* 该类用于视频数据的渲染显示，创建 LVRTCDisplayView 视图后，需要 调用 addDisplayView 把 LVRTCDisplayView 视图 添加进去。

```objc
@interface LVRTCDisplayView : UIView

/// 用户 ID，不传时默认为本地视图，（注：uid 和登录房间时传的 uid 相同时也默认为本地视图）
@property (nonatomic,copy)NSString *uid;

/// 设置视图填充模式
@property (nonatomic)LVViewContentMode viewContentMode;

/// 设置当前视图的旋转方向
/// @param orientation 旋转方向
- (void)setOrientation:(LVImageOrientation)orientation;
@end
```

>SDK 的视频流视图渲染显示 严格 与用户 ID 进行绑定，UID 决定将要渲染哪个视图 。
>
>如果不设置 uid，或者 uid 和登录房间时传的 uid 相同时，会自动默认渲染本地摄像头采集数据。

#### 设置本地预览视图模式

* 可以根据不同情况，调整本地预览视图的裁剪模式，设置显示。

```objc
/**
 本地预览视频视图的模式
 */
typedef NS_OPTIONS(NSUInteger, LVViewContentMode) {
    /**
     等比缩放，可能有黑边（或白边）
     */
    LVViewContentModeScaleAspectFit     = 0,
    /**
     等比缩放填充整View，可能有部分被裁减
     */
    LVViewContentModeScaleAspectFill    = 1,
    /**
     填充整个View
     */
    LVViewContentModeScaleToFill        = 2,
};
```
