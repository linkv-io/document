<!--
 * @Date: 2020-06-17 11:21:08
 * @LastEditors: GWK
 * @LastEditTime: 2020-07-02 19:16:29
 * @FilePath: /linkv_doc/doc_new/zh/web/livemesdk/api.md
-->

# Web JS SDK API documentation

## <a name='1'></a> 1 Request interface

### <a name='1.1'></a> 1.1 Initial configuration

> let octopusRTC = new OctopusRTC(option) option Object parameters are as follows:

| Parameter     | Meaning                 | Type   | Required                |
| -------- | -------------------- | ------ | ------------------- |
| appId    | appId                | String | Yes                  |
| userId   | user id              | String | Yes                  |
| userName | user name              | String | No                  |
| env      | Environment test production | String | No(default production) |

### <a name='1.1'></a> 1.2 Initiation

> octopusRTC.init() No parameter

### <a name='1.2'></a> 1.3 login Room

> octopusRTC.login(roomId,role,token).then(success).catch(error) The parameters are as follows:

| Parameter     | Meaning                 | Type   | Required                |
| ------- | ---------------------- | ------------------------------- | ---- |
| roomId  | Room id                | String                          | Yes   |
| role    | Role type 1: anchor 2: audience | Number                          | Yes   |
| token   | Login authentication               | String                          | Yes   |
| success | Join successfully               | function(streamList)            | No   |
| error   | Failed to join               | function(error)) See the error code list for details | No   |

> streamList structure of stream objects in the array


| Parameter     | Meaning                 | Type   |
| -------- | --------------- | ------ |
| streamId | Stream id           | String |
| userId   | User corresponding to the stream id | String |
| roomId   | Room number           | String |

### <a name='1.4'></a> 1.4 logout Room

> octopusRTC.logout() No parameter
> After the call, it will send a logout signal to the OctopusRTC server


### <a name='1.5'></a> 1.5 Start preview

> octopusRTC.startPreview(localVideo, mediaStreamConstraints).then(success).catch(error). The parameters are as follows：

| Parameter     | Meaning                 | Type   | Required                |
| ---------------------- | --------------------- | --------------- | ------------------- |
| localVideo             | Local preview video object | Document object        | Yes                  |
| mediaStreamConstraints | Audio and video configuration items          | Object          | No (Default audio and video added) |
| success                | Preview succeed              | function()      | No                  |
| error                  | review failed              | function(error) | No                  |

> Object structure of mediaStreamConstraints

| Parameter     | Meaning                 | Type 
| ------------ | --------------------------- | ------- |
| audio        | YesNo requires audio                | Boolean |
| audioInput   | Microphone equipment Id               | String  |
| video        | YesNo need video                | Boolean |
| videoInput   | Camera equipment Id               | String  |
| videoQuality | Video quality level 1: low 2: medium 3: high | Number  |

-There is no need to specify audioInput and videoInput, that is, do not pass or fill in undefined. Use default device when not specified

> videoQuality Parameter value

| Value | Resolution     |
| ---- | ---------- |
| 1    | 240\*320   |
| 2    | 480\*640   |
| 3    | 720\* 1280 |

> The explanation for error is as follows [click here for details](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)

| name                 | Meaning             |
| -------------------- | ---------------- |
| AbortError           | Aborting error         |
| NotAllowedError      | Reject error         |
| NotFoundError        | Error not found       |
| NotReadableError     | Unable to read error     |
| OverConstrainedError | Unable to meet the requirement error |
| SecurityError        | Security Error         |
| TypeError            | Type Error          |

### <a name='1.6'></a> 1.6 Stop preview


> octopusRTC.stopPreview(localVideo)，The parameters are as follows：

| Parameter     | Meaning                 | Type   | Required                |
| ---------- | --------------------- | -------- | ---- |
| localVideo | Local preview video object | document object| Yes   |

- During the streaming process, stopping the preview will cause the streaming to be interrupted


### <a name='1.7'></a> 1.7 Start streaming


> octopusRTC.startPublishingStream(streamId,localVideo) The parameters are as follows：

| Parameter     | Meaning                 | Type   | Required                |
| ---------- | --------------------- | -------- | ---- |
| streamId   | Push steaming id               | Sting    | Yes   |
| localVideo | Local preview video object | document object | Yes   |

### <a name='1.8'></a> 1.8 Stop pushing stream

> octopusRTC.stopPublishingStream(streamId) The parameters are as follows：

| Parameter     | Meaning                 | Type   | Required                |
| -------- | ----- | ------ | ---- |
| streamId | Stream id | String | Yes   |

### <a name='1.6'></a> 1.9 Start streaming

> octopusRTC.startPlayingStream(streamId,remoteVideo) The parameters are as follows:

| Parameter     | Meaning                 | Type   | Required                |
| ----------- | --------------------- | -------- | ---- |
| streamId    | Pull stream id               | String   | Yes   |
| remoteVideo | The video object of the streaming interface | document object | Yes   |

### <a name='1.10'></a> 1.10 Stop streaming

> octopusRTC.stopPlayingStream(streamId) The parameters are as follows:

| Parameter     | Meaning                 | Type   | Required                |
| -------- | ----- | ------ | ---- |
| streamId | 流 id | String | Yes   |

### <a name='1.11'></a> 1.11 Pause sound

> octopusRTC.mute(userId) The parameters are as follows:

| Parameter     | Meaning                 | Type   | Required                |
| ------ | ------- | ------ | ---- |
| userId | User id | String | Yes   |

### <a name='1.12'></a> 1.12 Restore sound

> octopusRTC.unmute(userId) The parameters are as follows:

| Parameter     | Meaning                 | Type   | Required                |
| ------ | ------- | ------ | ---- |
| userId | User id | String | Yes   |

### <a name='1.13'></a> 1.13 Turn on the camera


> octopusRTC.openCamera() No parameter

### <a name='1.14'></a> 1.14 Turn off the camera
> octopusRTC.closeCamera() No parameter

## <a name='2'></a> 2 Callback interface

### <a name='2.1'></a> 2.1 Room disconnect notification

> octopusRTC.onDisconnect(err) The parameters are as follows

| Parameter     | Meaning                 | Type 
| -------- | -------- | ------ |
| err.code | Error code   | Number |
| err.msg  | Error information | String |

### <a name='2.2'></a> 2.2 Notice of being kicked off line

> octopusRTC.onKickOut(err) The parameters are as follows:

| Parameter     | Meaning                 | Type 
| -------- | -------- | ------ |
| err.code | Error code   | Number |
| err.msg  | Error information  | String |

### <a name='2.3'></a> 2.3 Stream update notification

> octopusRTC.onStreamUpdated(type, streamList,error) The parameters are as follows:

| Parameter     | Meaning                 | Type 
| ---------- | ----------------------- | ------ |
| type       | Change type 0:add，1:delete | Number |
| streamList | Change flow list              | Array  |

> 流信息对象结构:

| Parameter     | Meaning    | Type 
| -------- | --------------- | ------ |
| streamId | Stream id           | String |
| userId   | User corresponding to the stream id | String |
| roomId   | Room number     | String |

### <a name='2.4'></a> 2.4 Pull stream status change notification

> octopusRTC.onPlayStateUpdate(type, streamId)

| Parameter     | Meaning        | Type 
| -------- | ---------------------------------------------- | ------ |
| type     | Flow state type 0: Pull stream succeed 1 : Pull stream failed 2:Re-pull | Number | Number |
| streamId | steam id                                          | String |

### <a name='2.5'></a> 2.5 Push stream status change notification

> octopusRTC.onPublishStateUpdate(type, streamId);

| Parameter     | Meaning                 | Type 
| -------- | --------------------------------------------- | ------ |
| type     | Flow state type 0 :Push stream successfully 1:Push stream failed 2: Re-pull  | Number |
| streamId | stream id                                         | String |

## <a name='3'></a> 3 Tool method


### <a name='3.1'></a> 3.1 obtain roomId

> octopusRTC.roomId()

### <a name='3.2'></a> 3.2 obtain userId

> octopusRTC.userId()

### <a name='3.3'></a> 3.3 obtain userName

> octopusRTC.userName()

### <a name='3.4'></a> 3.4 Get local camera information

> octopusRTC.getCamerasList().then(success).catch(errr)

| Parameter     | Meaning                 | Type   | Required                |
| ------- | ---------------------- | ------------------------- | ---- |
| success | Successfully obtain local camera information | function(inputVideoArray) | Yes   |
| error   | Failed to obtain local camera information | function(error)           | Yes   |

> The meaning of each InputVideoInfo parameter in inputVideoArray is as follows

| Parameter     | Meaning                 | Type 
| -------- | ------------- | ------ |
| deviceId | Equipment id       | String |
| groupId  | Equipment group id | String |
| kind     | videoinput    | String |
| label    | Device name      | Stirng |

### <a name='3.5'></a> 3.5 Get local audio input device information

> octopusRTC.getMicrophonesList().then(success).catch(errr)

| Parameter     | Meaning                 | Type   | Required                |
| ------- | ---------------------------- | ------------------------- | ---- |
| success | Get local audio input device information successfully| function(inputAudioArray) | Yes   |
| error   | Failed to obtain local audiovisual input device information | function(error)           | Yes   |

> The meaning of each InputDeviceInfo parameter in inputAudioArray is as follows


| Parameter     | Meaning                 | Type 
| -------- | ------------- | ------ |
| deviceId | Equipment id       | String |
| groupId  | Equipment group id  | String |
| kind     | audioinput    | String |
| label    | Device name        | Stirng |

### <a name='3.6'></a> 3.6 Get local audio output device information

> octopusRTC.getSpeakersList().then(success).catch(errr)

| Parameter     | Meaning                 | Type   | Required                |
| ------- | ---------------------------- | ----------------------- | ---- |
| success | Get local audio output device information successfully | function(outAudioArray) | Yes   |
| error   | Failed to obtain local audiovisual output device information | function(error)         | Yes   |

> The meaning of each outAudioInfo parameter in outAudioArray is as follows

| Parameter     | Meaning                 | Type 
| -------- | ------------- | ------ |
| deviceId | Equipment id       | String |
| groupId  | Equipment group id | String |
| kind     | audiooutput   | String |
| label    | Device name      | Stirng |

### <a name='3.7'></a> 3.7 Get local device information

> octopusRTC.devicesList().then(success).catch(errr)

| Parameter     | Meaning                 | Type   | Required                |
| ------- | -------- | -------------------- | ---- |
| success | Obtain     | function(deviceList) | Yes   |
| error   | Failed to preview | function(error)      | Yes   |

## <a name='4'></a> 4 Error code list

| Error code            | description                    |
| ----------------- | ----------------------- |
| 400000            | edge is null            |
| 60002001          | kRoomInvalidSocketError |
| WS_JOINROOM_ERROR | Failed to join                |
