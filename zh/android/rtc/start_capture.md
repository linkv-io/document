# 摄像头采集

## <a name='1'></a>1、概述

在开始推流之前，如果要推本地手机的音视频流，那么需要设置开启摄像头捕获，采集摄像头流。

## <a name='3'></a>3、步骤

### 代码示例

1. 首先需要调用 LVRTCEngine 单例的 startCapture 方法设置开启采集本地摄像头。

```java
// 获取 LVRTCEngine 单例对象
LVRTCEngine mRtcEngine = LVRTCEngine.getInstance(mContext.getApplication());

// 设置开启采集本地摄像头
mRtcEngine.startCapture();
```

2. 然后创建视频数据预览视图 LVDisplayView，并初始化一些属性。

```java
// LVDisplayView 为预览视图。
LVDisplayView mLocalDisplayView = new LVDisplayView()

// 设置预览视图绑定哪个用户ID
mLocalDisplayView.setUid(mUid);

// 预览的图像是否是本地用户数据
mLocalDisplayView.isLocalPreviewView(true);

// 设置显示视频数据的布局
mLocalDisplayView.setLayoutContainer(layout);

// 预览的试图是否显示在最高层级
mLocalDisplayView.isLocalPreviewView(true);
```

3. 为音视频设置添加预览视图，这样摄像头采集的数据就会渲染到此视图。

```java
// 为音视频设置预览视图 （SDK内部会自动将视图和接收到的音视频数据进行绑定操作，不设置音视频流会无法与视图绑定并进行渲染）
mRtcEngine.addDisplayView(mContext, mLocalDisplayView);
```

> 然后做完以上操作后，本地摄像头的数据就会 渲染到  LVDisplayView 上进行显示。

## <a name='4'></a>4、详细说明

>SDK 的视频流视图渲染显示严格与用户 ID 进行绑定，UID 决定将要渲染哪个视图 。
>
>如果想显示本地摄像头采集到的图像，则必须将 isLocalPreviewView 设置为true。

#### addDisplayView 方法 （为音视频设置预览视图方法）

* 开启采集本地摄像头之后， addDisplayView 添加视图后， SDK 内部才会自动将视图和音视频数据进行绑定渲染操作。

* 如果想要移除预览视图，那么可以调用 removeDisplayView 方法可以移除对应的预览视图，在调用之前可以 stopPlayingStream 停止播放对应的流。

```java
/**
 * 为音视频设置预览视图，请先加入房间后再进行设置，SDK 内部会自动将视图和接收到的音视频数据进行绑定操作
 * @param context       视图所在类的上下文引用
 * @param view          视图信息
 */
public void addDisplayView(Context context, LVDisplayView view);

/**
 * 移除预览视图
 * @param view          视图信息
 */
public void removeDisplayView(LVDisplayView view);
```

#### LVDisplayView 类（视频数据显示类）

* 该类用于视频数据的渲染显示，创建 LVDisplayView 视图后，需要调用 addDisplayView 把 LVDisplayView 视图添加进去。

```java
public class LVDisplayView {

    // 用户 ID
    protected String uid;
    
    // 是否是水平镜像渲染
    protected boolean isFlipHorizontal = false;
    
    // 是否是本地预览显示窗口
    protected boolean isLocalPreviewView;
    
    // 视图是否显示到高层级
    protected boolean isZOrderMediaOverlay = true;
    
    // 视图图像显示的布局
    protected ViewGroup layoutContainer;
    
}
```
