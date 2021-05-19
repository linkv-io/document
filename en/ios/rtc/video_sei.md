# Media Supplemental Enhancement Information (SEI)

## <a name='1'></a>1、Introduction

When LinkV SDK publish streaming, it can send additional messages with the video frames. Then the remote side will receive the OnDrawFrame callback function with the additional messages when they playing the stream. If you want to add text information when you publish the streams and receive it on the side of playing the stream, The SEI is needed to synchronize the text data and the video data.

Generally, it can be used in the situations of lyrics synchronization, livestreaming quiz , etc., in the scenarios need to send synchronized text with video data.

## <a name='2'></a>2、Procedures

* Implement the delegate method of loginRoom, and then feedback the corresponding SEI information by the delegate method when publishing stream.

* The corresponding SEI data information is received by the callback method from video data when playing stream.

### 2.2. Add SEI in Publishing Stream

* The SDK will trigger the following callback when sending the video, and the developer can insert the information that needs to be attached to the video.

* This method will trigger the callback in every frame, it will be called plenty of times, and needs to be handle well.

``` objc
// Whether to add other media information to the Video frames
// @param timestamp The timestamp of the frame that needs to send the data.
// @return Please return the additional data to be sent with the current video frame (the maximum string is 24 characters)

* (NSString *)onMediaSideInfoInPublishVideoFrame:(NSUInteger)timestamp{

    return @"extra data";
}
```

### 2.3. Get SEI in Playing Stream

* The remote users will receive a notification of the customized data when they have received it.

``` objc
// After receiving the video data, if the rendering view is been set for the SDK, the SDK will render the video frame automatically
// @param pixelBuffer decoded video data
// @param uid User ID
// @param sei THe additional attached information 
// @return It is recommended to return the timestamp of the current rendering completion to count the delays of the rendering process.
// @discussion Note：If the user implements this interface, the remote video rendering inside the SDK will be activated, and the rendering will be completed externally

* (int64_t)OnDrawFrame:(CVPixelBufferRef)pixelBuffer

                   uid:(NSString *)uid
                   sei:(NSString *)sei{
	NSLog(@"%@", sei);                 
}
```
