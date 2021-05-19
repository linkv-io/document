# Media Supplemental Enhancement Information (SEI)

## <a name='1'></a>1、Introduction

In LinkV SDK, when pushing the stream, the remote end will receive the callback of the onDrawFrame method after pulling the stream, that is, this method will be called back when the remote video data is received. If you want to add text information when you push the stream, and then receive it at the stream end, use sei to synchronize the text data and the audio and video content data.
Generally used for lyrics synchronization，Live answer and other scenes that need to send synchronized text with video data。

## <a name='2'></a>2、Procedures

* Call the setLiveRoomCallback method of LVRTCEngine to set the implementation interface LVRTCCallback, and then feedback the corresponding sei information in the proxy method of the pusher.
* The corresponding sei data information is received in the proxy method of the remote video data callback of the streaming party。

### 2.2. Push side

When the SDK sends a video, the following method will be called back, and the developer can return the information that needs to be carried with the video.
This method calls back each frame, is called multiple times, and requires control processing.
```java
/**
 *  Whether additional media information needs to be attached to the video frame
 *  @return     Please return additional data to be sent with the current video frame（The maximum string length is 24 characters）
 */
 String onMediaSideInfoInPublishVideoFrame() {
    return data;
}
```

### 2.3. Pull stream side

* Remote users receive notifications of custom data when they receive this custom data

```java
/**
 *  Receive remote video data back，If you set up a render view for the SDK, the SDK will automatically render the video frame internally
 *  @param i420Buffer       ByteBufferType，i420 byte array
 *  @param width        int type，Video frame wide
 *  @param height       int type，Video frame width
 *  @param stride       int type，the frame data stride
 *  @param userId       String Type，user id corresponding to the frame data
 *  @param ext          String Type，additional data information carried with the video data
 *  @return     long type，It is recommended to return the timestamp of the current rendering completion，used to count the rendering delay
 */
long onDrawFrame(ByteBuffer i420Buffer, final int width, final int height, int strideY, final String userId, String ext)
```