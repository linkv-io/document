# common error code

###### This article lists common error codes for the initialization SDK, login room, push-pull flow, and mixed flow sections.

| error code | enumeration value | describes |
| --- | --- | --- |
|SDK business operation successful |
| paramError| 1000| parameter error |
| notInitError| 1001| does not initialize the error |
| notAuthError| 1002| SDK is not authorized, please authorize before using |
| initError| 1003| room instance initializes the error |
| unsupportFormat| 1004| unsupported audio video format |
| authError|2000 | SDK authorization error |
| disconnectSignaling|3000 | audio and video signaling service disconnect error |
| disconnectMedia| 3001| media service disconnected error |
| noEdgeError | 4000| can't get the effective audio and video signaling service |
| network workreqerror | 4001| network request error (including network unreachable, network request timeout, 40x series error) |
| networkRspError| 4002| network response error (illegal return data, 50x series error) |
| unknownError| 10000| unknown |

