# Architecture introduction

## <a name='1'></a>1、SDK Architecture design


LinkV IM System and business side account system are independent of each other，Can be seamless。When you use IM to send messages, you only need to provide the user ID and the IM token corresponding to the ID. The user ID is used to identify the identity, and the IM token is used to verify the user's permission to connect to IM. The architecture design of IM SDK is as follows:
![img](https://dl.linkv.io/doc/en/ios/im/images/structure_design.png)

After login, it will start to verify the IM token in a loop. If the verification fails or the IM token expires, the callback to set the token will be triggered. Therefore, it is recommended to write the get token and set token in the callback method. The process of obtaining IM token is shown in the figure below.

![img](https://dl.linkv.io/doc/en/ios/im/images/request_token_process.png)



## <a name='2'></a>2、Integration flow chart

You need to register a developer account in the background before integrating the SDK，and create an application to get appId and appSign
。See the integration steps[Integration process](/en/android/im/quick_start.md)

![img](https://dl.linkv.io/doc/en/ios/im/images/im_access_process.png)
