## Classes

<dl>
<dt><a href="#OctopusRTC">OctopusRTC</a></dt>
<dd></dd>
</dl>

## Typedefs

<dl>
<dt><a href="#errMsg">errMsg</a> : <code>Object</code></dt>
<dd></dd>
<dt><a href="#sourceCamera">sourceCamera</a> : <code>Object</code></dt>
<dd></dd>
</dl>

<a name="OctopusRTC"></a>

## OctopusRTC
**Kind**: global class  

* [OctopusRTC](#OctopusRTC)
    * [new OctopusRTC(appId, userId, [env], [type], [logLevel], [userName])](#new_OctopusRTC_new)
    * [.init()](#OctopusRTC+init)
    * [.isSupported()](#OctopusRTC+isSupported) ⇒ <code>boolean</code>
    * [.login(roomId, role, auth, expire)](#OctopusRTC+login) ⇒ <code>Array</code> &#124; <code>[errMsg](#errMsg)</code>
    * [.logout()](#OctopusRTC+logout)
    * [.createStream([source])](#OctopusRTC+createStream) ⇒ <code>mediastream</code>
    * [.destroyStream(mediastream)](#OctopusRTC+destroyStream)
    * [.startPublishingStream(streamId, mediaElement)](#OctopusRTC+startPublishingStream) ⇒ <code>void</code>
    * [.stopPublishingStream(streamId)](#OctopusRTC+stopPublishingStream)
    * [.startPlayingStream(streamId)](#OctopusRTC+startPlayingStream) ⇒ <code>void</code>
    * [.stopPlayingStream(streamId)](#OctopusRTC+stopPlayingStream)
    * [.updateMixStream(mixStreamConfig)](#OctopusRTC+updateMixStream) ⇒ <code>\*</code>
    * [.replaceTrack(currentStream, track, [streamId])](#OctopusRTC+replaceTrack)
    * [.changeConstraints(currentStream, type, constrains, [streamId])](#OctopusRTC+changeConstraints) ⇒ <code>Promise</code>
    * [.muteSwitch(streamId, mute)](#OctopusRTC+muteSwitch)
    * [.cameraSwitch(streamId, state)](#OctopusRTC+cameraSwitch)
    * ["stream-update"](#OctopusRTC+event_stream-update) ⇒ <code>[ &#x27;Array&#x27; ].&lt;{streamId: string, userId: string, roomId: string}&gt;</code>
    * ["disconnect"](#OctopusRTC+event_disconnect) ⇒ <code>[errMsg](#errMsg)</code>

<a name="new_OctopusRTC_new"></a>

### new OctopusRTC(appId, userId, [env], [type], [logLevel], [userName])
创建OctopusRTC实例


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| appId | <code>string</code> |  | appId |
| userId | <code>string</code> |  | 用户的userId |
| [env] | <code>string</code> | <code>&quot;prod&quot;</code> | SDK环境选择 |
| [type] | <code>string</code> | <code>&quot;international&quot;</code> | 节点环境选择 |
| [logLevel] | <code>number</code> |  | 日志级别 |
| [userName] | <code>string</code> |  | 用户名称 |

<a name="OctopusRTC+init"></a>

### octopusRTC.init()
初始化SDK

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
<a name="OctopusRTC+isSupported"></a>

### octopusRTC.isSupported() ⇒ <code>boolean</code>
判断浏览器是否支持WebRTC

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
<a name="OctopusRTC+login"></a>

### octopusRTC.login(roomId, role, auth, expire) ⇒ <code>Array</code> &#124; <code>[errMsg](#errMsg)</code>
登录房间

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
**Returns**: <code>Array</code> &#124; <code>[errMsg](#errMsg)</code> - {(Promise<streamlist[] | errMsg>)}  

| Param | Type | Description |
| --- | --- | --- |
| roomId | <code>string</code> | 房间id |
| role | <code>1</code> &#124; <code>2</code> | 角色 |
| auth | <code>string</code> | 鉴权签名值 |
| expire | <code>string</code> | 过期时间戳 |

<a name="OctopusRTC+logout"></a>

### octopusRTC.logout()
登出房间

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
<a name="OctopusRTC+createStream"></a>

### octopusRTC.createStream([source]) ⇒ <code>mediastream</code>
创建流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
**Returns**: <code>mediastream</code> - {Promise<MediaStream>}  

| Param | Type | Description |
| --- | --- | --- |
| [source] | <code>object</code> | 视频源类型 |
| [source.camera] | <code>object</code> | 摄像头 |
| [source.screen] | <code>object</code> | 屏幕共享 |
| [source.custom] | <code>object</code> | 自定义流 |
| [source.camera.audio] | <code>boolean</code> | 是否开启音频 |
| [source.camera.video] | <code>boolean</code> | 是否开启视频 |
| [source.camera.audioInput] | <code>string</code> | 音频输入设备 |
| [source.camera.audioBitrate] | <code>number</code> | 音频码率 |
| [source.camera.videoInput] | <code>string</code> | 视频输入设备 |
| [source.camera.videoQuality] | <code>1</code> &#124; <code>2</code> &#124; <code>3</code> &#124; <code>4</code> | 视频质量 |
| [source.camera.facingMode] | <code>string</code> | 切换摄像头（移动端） |
| [source.camera.width] | <code>number</code> | 宽 |
| [source.camera.height] | <code>number</code> | 高 |
| [source.camera.frameRate] | <code>number</code> | 帧率 |
| [source.camera.bitrate] | <code>number</code> | 码率 |
| [source.camera.AGC] | <code>boolean</code> | 自动增益 |
| [source.camera.ANS] | <code>boolean</code> | 回声消除 |
| [source.camera.AEC] | <code>boolean</code> | 降噪 |
| [source.screen.audio] | <code>boolean</code> | (共享屏幕)是否开启音频 |
| [source.screen.videoQuality] | <code>1</code> &#124; <code>2</code> &#124; <code>3</code> &#124; <code>4</code> | 视频质量设置 |
| [source.screen.frameRate] | <code>number</code> | 帧率 |
| [source.screen.bitrate] | <code>number</code> | 码率 |
| source.custom.source | <code>MediaStream</code> | 视频流 |
| [source.custom.bitrate] | <code>number</code> | 码率 |

<a name="OctopusRTC+destroyStream"></a>

### octopusRTC.destroyStream(mediastream)
删除流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  

| Param | Type |
| --- | --- |
| mediastream | <code>MediaStream</code> | 

<a name="OctopusRTC+startPublishingStream"></a>

### octopusRTC.startPublishingStream(streamId, mediaElement) ⇒ <code>void</code>
开始推流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
**Returns**: <code>void</code> - {Promise<void>}  

| Param | Type | Description |
| --- | --- | --- |
| streamId | <code>string</code> | 流id |
| mediaElement | <code>MediaStream</code> | 流 |

<a name="OctopusRTC+stopPublishingStream"></a>

### octopusRTC.stopPublishingStream(streamId)
停止推流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  

| Param | Type | Description |
| --- | --- | --- |
| streamId | <code>string</code> | 流id |

<a name="OctopusRTC+startPlayingStream"></a>

### octopusRTC.startPlayingStream(streamId) ⇒ <code>void</code>
开始拉流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
**Returns**: <code>void</code> - {(Promise<MediaStream | void>)}  

| Param | Type | Description |
| --- | --- | --- |
| streamId | <code>string</code> | 流id |

<a name="OctopusRTC+stopPlayingStream"></a>

### octopusRTC.stopPlayingStream(streamId)
停止拉流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  

| Param | Type | Description |
| --- | --- | --- |
| streamId | <code>string</code> | 流id |

<a name="OctopusRTC+updateMixStream"></a>

### octopusRTC.updateMixStream(mixStreamConfig) ⇒ <code>\*</code>
混流

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
**Returns**: <code>\*</code> - {Promise<void>}  

| Param | Type |
| --- | --- |
| mixStreamConfig | <code>mixStreamConfig</code> | 

<a name="OctopusRTC+replaceTrack"></a>

### octopusRTC.replaceTrack(currentStream, track, [streamId])
更改流track

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  

| Param | Type |
| --- | --- |
| currentStream | <code>MediaStream</code> | 
| track | <code>MediaStreamTrack</code> | 
| [streamId] | <code>string</code> | 

<a name="OctopusRTC+changeConstraints"></a>

### octopusRTC.changeConstraints(currentStream, type, constrains, [streamId]) ⇒ <code>Promise</code>
更改约束、设备

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  
**Returns**: <code>Promise</code> - {(Promise<errMsg | void>)}  

| Param | Type |
| --- | --- |
| currentStream | <code>MediaStream</code> | 
| type | <code>&#x27;audio&#x27;</code> &#124; <code>&#x27;video&#x27;</code> | 
| constrains | <code>MediaTrackConstraints~sourceCamera</code> | 
| [streamId] | <code>string</code> | 

<a name="OctopusRTC+muteSwitch"></a>

### octopusRTC.muteSwitch(streamId, mute)
开启静音

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  

| Param | Type | Description |
| --- | --- | --- |
| streamId | <code>string</code> | 流id |
| mute | <code>boolean</code> | 是否静音 |

<a name="OctopusRTC+cameraSwitch"></a>

### octopusRTC.cameraSwitch(streamId, state)
切换摄像头

**Kind**: instance method of <code>[OctopusRTC](#OctopusRTC)</code>  

| Param | Type | Description |
| --- | --- | --- |
| streamId | <code>string</code> | 流id |
| state | <code>&#x27;close&#x27;</code> &#124; <code>&#x27;open&#x27;</code> | 摄像头状态 |

<a name="OctopusRTC+event_stream-update"></a>

### "stream-update" ⇒ <code>[ &#x27;Array&#x27; ].&lt;{streamId: string, userId: string, roomId: string}&gt;</code>
流变化通知 event.

**Kind**: event emitted by <code>[OctopusRTC](#OctopusRTC)</code>  
**Since**: 2.0  
<a name="OctopusRTC+event_disconnect"></a>

### "disconnect" ⇒ <code>[errMsg](#errMsg)</code>
websocket 断开通知 event.

**Kind**: event emitted by <code>[OctopusRTC](#OctopusRTC)</code>  
**Since**: 2.0  
<a name="errMsg"></a>

## errMsg : <code>Object</code>
**Kind**: global typedef  
**Properties**

| Name | Type |
| --- | --- |
| code | <code>number</code> | 
| msg | <code>string</code> | 

<a name="sourceCamera"></a>

## sourceCamera : <code>Object</code>
**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| audio | <code>boolean</code> | 是否开启音频 |
| video | <code>boolean</code> | 是否开启视频 |
| audioInput | <code>string</code> | 音频输入设备 |
| videoInput | <code>string</code> | 视频输入设备 |
| videoQuality | <code>number</code> | 视频质量 |
| facingMode | <code>string</code> | 摄像头朝向，"user"表示前置摄像头，"environment"表示后置摄像头 |
| width | <code>number</code> | 宽 |
| height | <code>number</code> | 高 |
| frameRate | <code>number</code> | 帧率 |
| bitrate | <code>number</code> | 码率 |
| AGC | <code>boolean</code> | 自动增益 |
| ANS | <code>boolean</code> | 回声消除 |
| AEC | <code>boolean</code> | 降噪 |

