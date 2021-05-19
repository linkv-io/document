# SDK Update log


## <a name='1'></a> xxxx-xx-xx (v x.x.x.x)

### <a name='1.1'></a> new features
- ##### Retweet supports RTMPS protocol
###### &emsp;&emsp;&emsp;This function can repost the live stream to Facebook to help customers' ecological flow. Currently only deployed to overseas clusters。

- ##### End-to-end encryption and decryption of streaming media data
###### &emsp;&emsp;&emsp;By pushing and pulling the symmetric key set before the stream, the security of the media data is further strengthened. The key setting is completed by an external module, such as client App。Only Native SDK push-pull is supported, and CDN, WebRTC, mixed stream client and recording client are not supported。

- ##### MediaRecorder Increase quality callback

###### &emsp;&emsp;&emsp;Media local recording agent ZegoMediaRecordDelegate Add -onRecordStatusUpdateFromChannel:storagePath:duration:fileSize:quality: callback。
###### &emsp;&emsp;&emsp;When offline recording, you can use this callback to obtain quality information such as resolution and frame rate, and perform fault-tolerant processing in time。

> Upgrade note:
> 

## <a name='2'></a> xxxx-xx-xx (v x.x.x.x)

