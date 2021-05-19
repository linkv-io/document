# Custom Audio Capture

## <a name='1'></a>1、Introduction

During the live streaming process, the audio data will be captured by microphone default. If the application has its own audio input source, you want it to be able to input the audio data source separately without being involved in the accompaniment mixing, then the custom audio capture can be used.

## <a name='2'></a>2、Description

With the custom audio capture, the side of pull stream will hear the custom audio streams from the side of push stream.

<img src="https://dl.linkv.io/doc/en/android/rtc/images/diy_audio_extra2.png" width="iOS_Auth2" style="width:50%;" />

## <a name='3'></a>3、The operation procedures

（1）Turn on the function of external audio capture

（2）Log in to the room and push the streams

（3）Decode the audio

（4）Called and send the external audio data

## <a name='4'></a>4、4. API

#### Turn on and off the external audio capture function (set before joining the room)

```java
/**
 * Turn on and off the external audio capture function，This parameter will automatically disable the built-in microphone function of the SDK if the card is clocked in, and the user will input audio PCM data to the SDK.
 * @param enable        Boolean type，true: Clock in，false: Close
 */
mRtcEngine.enableExternalAudioInput(true);
```

#### Send the external audio data

```java
/**
 *  Send external audio data，Note：It will only take effect after calling enableExternalAudioInput to open the external audio input interface
 * @param     databyte array type, audio data
 * @return      int type，0 means failure; !0 means success.
 */
mRtcEngine.sendAudioFrame(audioData);
```

#### Set up the external audio data parameters

```java
/**
 * Set external audio data parameters
 * @param audioConfig       Audio parameters
 */
mRtcEngine.setExternalAudioConfig(audioConfig);
```

#### The external audio parameters of LVAudioRecordConfig

* The external audio sample rate, channel, etc. can be customized after the external audio is turned on. If not, the default value will be used.

```java
// External audio capture parameter configuration
public class LVExternalAudioConfig {

    // External audio capture input sampling rate（Default 4800000）
    private int sampleRate = 4800000;
    
    // Number of external audio capture input channels （Default 1）
    private int channels = 1;

}
```

## <a name='5'></a>5、Demo

For the specific reference, please open the [foundation SDK demo](/?p=/en/android/rtc/download_sdk.md&k=LKdNguJq)  for the example project.

