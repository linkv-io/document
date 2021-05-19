# 下载SDK

**更新时间：2020-08-27**

## <a name='1'></a>1、服务端 SDK 下载

LinkV 提供 以下语言的SDK，请下载**最新**版本的tag

| 语言 | 版本 |  |
| --- | --- | ---     |
|Golang | >= 1.8 | [下载](https://github.com/linkv-io/go-sdk) |
| Python2 | >=2.7.9 | [下载](https://github.com/linkv-io/python2-sdk) |
| Python3 | 3.5｜3.6｜3.7｜3.8 | [下载](https://github.com/linkv-io/python-sdk) |
| PHP | 5.* ｜ 7.* | [下载](https://github.com/linkv-io/php-sdk) |
| Node | >=10.15.3 | [下载](https://github.com/linkv-io/node-sdk) |
| Dart | >=2.5.0 ｜ <3.0.0 |[下载](https://github.com/linkv-io/dart-sdk) |

> 现有服务端SDK中并没有您所使用的服务端语言 请参照 [API文档]() 进行编写对接
>

## <a name='2'></a>2、客户端 Demo 下载

LinkV SDK提供示例项目，请前往  [LiveMeSDKSample](https://dl.linkv.io/static/Android/LiveMe/LinkVDemo.zip)  下载。在实现相关功能前，你可以下载并查看源代码，这对于您接入和使用本SDK有较大帮助。示例代码中包含，登录、获取直播列表、开播功能。

![demo_sample](https://dl.linkv.io/doc/zh/android/live/images/demo_sample.jpg)

## <a name='3'></a>3、应用下载

展示LiveMeSDK在社交场景的体验和能力

<img src="https://dl.linkv.io/doc/zh/ios/live/images/linkvapp_qrcode.png" width="iOS_Auth2" style="width:30%;" />

## <a name='4'></a>4、快速登录方法

为了方便快捷的体验SDK功能，和演示登录的流程，示例工程中提供了快速登录的 doLogin 方法，详细使用方法在示例工程的 DevelopmentLoginAct.java 文件中

```java
LiveMeClient.getInstance().bindingTokenWithUid(uid, name, new LoginGetTokenWrapper.OnBindingTokenListener() {
    @Override
    public void onRequestSuccess(String uid, String openId, String token) {
        //获取token登录
        LiveMeClient.getInstance().onLoginSuccess(uid, openId, token);
        //跳转页面
        LoginTransferUtil.process(DevelopmentLoginAct.this, mFrom);
    }

    @Override
    public void onRequestFail(String msg) {
        hideLoading();
        showToast("登录失败");
    }
});
```

> 示例代码中提供了SDK鉴权需要的测试appid和secret，不可以在正式环境中使用。示例代码中的所有功能需要在登录完成之后才能正常使用
>

