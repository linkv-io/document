# 架构介绍

## <a name='1'></a>1、SDK架构设计

LinkV IM 系统和业务方账户系统相互独立，可以无缝衔接。您在使用IM发消息只需提供用户ID和该ID对应的IM token，用户ID用以标识身份，IM token用以验证用户连接IM的权限。IM SDK的使用架构设计如下图：

![img](https://dl.linkv.io/doc/zh/android/im/images/structure_design.png)

登录后会开始循环验证IM token，验证失败会或者IM token过期都会触发设置token的回调。所以建议将获取token和设置token写在该回调方法中。IM token的获取流程如下图所示。

![img](https://dl.linkv.io/doc/zh/android/im/images/request_token_process.png)



## <a name='2'></a>2、集成流程图

集成SDK前需在后台注册开发者账号，并创建应用获取appId和appSign。集成步骤详见[集成流程](/zh/android/im/quick_start.md)

![img](https://dl.linkv.io/doc/zh/android/im/images/im_access_process.png)

