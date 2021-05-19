# Camera Capture

## <a name='1'></a>1、Overview

Before starting to publish the stream, you need to enable the camera of the mobile device to capture the camera's video stream.

## <a name='2'></a>2、Process

![](https://dl.linkv.io/doc/en/android/rtc/images/bind_capture.png)

## <a name='3'></a>3、Procedures

### Code example

1. First, you need to call the startCapture method of the LVRTCEngine singleton to start the local camera capture.

```java
// Get the LVRTCEngine singleton object

LVRTCEngine mRtcEngine = LVRTCEngine.getInstance(mContext.getApplication());

// Set to enable local camera

mRtcEngine.startCapture();
```

2. Then create a video data preview of LVRTCDisplayView, and specify its frame size, Set the view content mode as ScaleAspectFill

```java
// LVDisplayView Preview view
。
LVDisplayView mLocalDisplayView = new LVDisplayView()

// Set which user ID the preview view is bound to

mLocalDisplayView.setUid(mUid);

// Whether the previewed image is local user data

mLocalDisplayView.isLocalPreviewView(true);

// Set the layout of the display video data
mLocalDisplayView.setLayoutContainer(layout);

// Whether the preview is displayed at the highest level
mLocalDisplayView.isLocalPreviewView(true);
```

3. Add preview view for audio and video settings，In this way, the data collected by the camera will be rendered into this view。

```java
// Set the preview view for audio and video (SDK will automatically bind the view and the received audio and video data. If the audio and video stream is not set, the view cannot be bound and rendered)

mRtcEngine.addDisplayView(mContext, mLocalDisplayView);
```

> Then after finishing the above operations, the data of the local camera will be rendered to LVDisplayView for display
。

## <a name='4'></a>4、Detailed description


>SDK's video stream view rendering display is strictly bound to the user ID, and the UID determines which view will be rendered.

>
>If you want to display the image captured by the local camera, you must set isLocalPreviewView to tru
e。

#### addDisplayView method (set preview view method for audio and video)


* After the local camera is turned on and addDisplayView adds a view, the SDK will automatically bind the view and audio and video data for rendering.


* If you want to remove the preview view, you can call the removeDisplayView method to remove the corresponding preview view, and you can stop playing the corresponding stream before calling stopPlayingStream.

```java
/**
 * Set preview view for audio and video，Please join the room before setting, the SDK will automatically bind the view and the received audio and video data
 * @param context       Context reference of the class of the view

 * @param view          View information

 */
public void addDisplayView(Context context, LVDisplayView view);

/**
 * Remove preview view
 * @param view          View information

 */
public void removeDisplayView(LVDisplayView view);
```

#### LVDisplayView Class (video data display class）

* This class is used for the rendering and display of video data. After creating the LVDisplayView view, you need to call addDisplayView to add the LVDisplayView view.
```java
public class LVDisplayView {

    // User ID
    protected String uid;
    
    // Whether it is a horizontal mirror rendering

    protected boolean isFlipHorizontal = false;
    
    // Whether it is a local preview display window

    protected boolean isLocalPreviewView;
    
    // Whether the view is displayed to a higher level

    protected boolean isZOrderMediaOverlay = true;
    
    // View image display layout

    protected ViewGroup layoutContainer;
    
}
```
