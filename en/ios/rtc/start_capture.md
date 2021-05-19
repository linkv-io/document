# Camera Capture

## <a name='1'></a>1、Overview

Before starting to publish the stream, you need to enable the camera of the mobile device to capture the camera's video stream.

## <a name='2'></a>2、Process

![](https://dl.linkv.io/doc/en/ios/rtc/images/bind_capture.png)

## <a name='3'></a>3、Procedures

### Code example

1. First, you need to call the startCapture method of the LVRTCEngine singleton to start the local camera capture.

``` objc
// Start the Capture
[[LVRTCEngine sharedInstance] startCapture];
```

2. Then create a video data preview of LVRTCDisplayView, and specify its frame size, Set the view content mode as ScaleAspectFill

``` objc
// LVRTCDisplayView as the Main Preview。
LVRTCDisplayView *mainPreview = [[LVRTCDisplayView alloc] initWithFrame:[UIScreen mainScreen].bounds];
// Set the view content mode as ScaleAspectFill
mainPreview.viewContentMode = LVViewContentModeScaleAspectFill;
```

3. Add the main preview settings, and do not specify uid (default to using uid of the login room) so that the data captured by the camera will be rendered.

``` objc
// Add the mainPreview to the current view
[self.view addSubview:mainPreview];

// add mainPreview to dispaly（SDK will bind the received video and the view)
[[LVRTCEngine sharedInstance] addDisplayView:mainPreview];
```

> After finishing the operation above, the data of the local camera will be rendered and displayed on the LVRTCDisplayView.

## <a name='4'></a>4、Detailed Description

#### addDisplayView

* After the local camera is enabled and added the addDisplayView, the SDK will bind the view and the received video data for rendering.

* If you want to remove the displayview, you can call the removeDisplayView to remove the corresponding displayview. Before calling this method, you can call stopPlayingStream to stop playing the corresponding stream.

``` objc
//Please entered the room first and then configure the displayview, SDK will bind the received video and the view
// @param view data of the displayview
// @discussion Default as the current user if dont pass an UID. 

* (void)addDisplayView:(LVRTCDisplayView *)view;

// Remove the displayview
// @param view displayview's information
-(void)removeDisplayView:(LVRTCDisplayView *)view;
```

#### LVRTCDisplayView

* This class is used to render and display the video data. After creating the LVRTCDisplayView, you need to call the addDisplayView to add the LVRTCDisplayView onto it.

``` objc
@interface LVRTCDisplayView : UIView

/// UID，if not passed,default as the local dispayview（Reminder：If the UID is the same as the UID passed the room login, also default as the local displayview）
@property (nonatomic,copy)NSString *uid;

/// Configuration of the viewcontent mode
@property (nonatomic)LVViewContentMode viewContentMode;

/// Configure the orientation of the current displayview
/// @param orientation 

* (void)setOrientation:(LVImageOrientation)orientation;

@end
```

> The SDK's video stream view rendering display is bound to the user ID, and the UID determines which view will be rendered.
>
> If uid is not set, or the uid is the same as the uid of logging into the room, the local camera will be captured to render.

#### Configure the ViewContentMode

* You can adjust the crop mode of the local preview view and set the display according to different situations.

``` objc
/**
  The ViewContentMode
 */
typedef NS_OPTIONS(NSUInteger, LVViewContentMode) {
    /**
     Proportional scaling，Could be Black/white edges
     */
    LVViewContentModeScaleAspectFit     = 0,
    /**
     Some of the parts could be cropped when sacaling to fill the whole view.
     */
    LVViewContentModeScaleAspectFill    = 1,
    /**
     scale to fill the View
     */
    LVViewContentModeScaleToFill        = 2,
};
```
