# Custom Audio Capture

## <a name='1'></a>1、Introduction

During the live streaming process, the audio data will be captured by microphone default. If the application has its own audio input source, you want it to be able to input the audio data source separately without being involved in the accompaniment mixing, then the custom audio capture can be used.

## <a name='2'></a>2、Description

With the custom audio capture, the side of pull stream will hear the custom audio streams from the side of push stream.

<img src="https://dl.linkv.io/doc/en/ios/rtc/images/diy_audio_extra2.png" width="iOS_Auth2" style="width:50%; " />

## <a name='3'></a>3、The operation procedures

（1）Turn on the function of external audio capture

（2）Log in to the room and push the streams

（3）Decode the audio

（4）Called and send the external audio data

## <a name='4'></a>4、4. API

#### Turn on and off the external audio capture function (set before joining the room)

``` objc
// Turn on and off the external audio capture function. If this parameter is true, the SDK's built-in microphone function will be automatically disabled, and the user will input audio PCM data to the SDK.
// @param enable true: On，false: Off
[[LVRTCEngine sharedInstance] enableExternalAudioInput:true]; 
```

#### Send the external audio data

``` objc
// Send the external audio data，（It can only be activated by turning on the external audio interface with enableExternalAudioInput ）
// @param audioFrameBuffer audio date
// @param length （int16_t array data length）
// @return whether it is succeeded or not
[[LVRTCEngine sharedInstance] sendAudioFrame:buffer length:(int)length];
```

#### Set up the external audio data parameters

``` objc
/// Set up the external audio data parameters
/// @param audioConfig audio parameters
-(void)setExternalAudioConfig:(LVAudioRecordConfig *)audioConfig;
```

#### The external audio parameters of LVAudioRecordConfig

* The external audio sample rate, channel, etc. can be customized after the external audio is turned on. If not, the default value will be used.

``` objc
/// The external audio parameters
@interface LVAudioRecordConfig : NSObject

/// input the sample rate（default as 48000）
@property (nonatomic,assign)int sampleRate;

/// input the channel（default as 1）
@property (nonatomic,assign)int channels;

/// The data length of each buffer inputted（the parameter must be the same length as the inputted data of sendAudioBuffer ）
@property (nonatomic,assign)int framesPerBuffer;

@end
```

## <a name='5'></a>5、Demo

For the specific reference, please open the [foundation SDK demo](/?p=/en/ios/rtc/download_sdk.md&k=LKdNguJq) for the example project.

