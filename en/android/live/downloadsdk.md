# Download SDK

**Update Date：2020-08-19**

## <a name='1'></a>1、Server SDK download

LinkV provides SDKs in the following languages, please download the **latest** version of the tag

| Language | Version |  |
| --- | --- | ---     |
|Golang | >= 1.8 | [Download](https://github.com/linkv-io/go-sdk) |
| Python2 | >=2.7.9 | [Download](https://github.com/linkv-io/python2-sdk) |
| Python3 | 3.5｜3.6｜3.7｜3.8 | [Download](https://github.com/linkv-io/python-sdk) |
| PHP | 5.* ｜ 7.* | [Download](https://github.com/linkv-io/php-sdk) |
| Node | >=10.15.3 | [Download](https://github.com/linkv-io/node-sdk) |
| Dart | >=2.5.0 ｜ <3.0.0 |[Download](https://github.com/linkv-io/dart-sdk) |

> The server language you are using is not available in the existing server SDK. Please refer to [API document]() for writing and docking
>

## <a name='2'></a>2、User end Demo Download

LinkV SDK provides sample project, please go to  [LiveMeSDKSample](https://dl.linkv.io/static/Android/LiveMe/LinkVDemo.zip)  to download.Before implementing the relevant functions, you can download and view the source code, which is of great help for you to access and use this SDK. The sample code contains the functions of logging in, getting the live broadcast list, and starting the broadcast.

![demo_sample](https://dl.linkv.io/doc/en/android/live/images/demo_sample.jpg)

## <a name='3'></a>3、Quick login method

In order to experience the SDK functions conveniently and quickly, and demonstrate the login process, the doLogin method for quick login is provided in the sample project. The detailed usage method is in the DevelopmentLoginAct.java file.

```java
LiveMeClient.getInstance().bindingTokenWithUid(uid, name, new LoginGetTokenWrapper.OnBindingTokenListener() {
    @Override
    public void onRequestSuccess(String uid, String openId, String token) {
        //Obtain token to login
        LiveMeClient.getInstance().onLoginSuccess(uid, openId, token);
        //redirection page
        LoginTransferUtil.process(DevelopmentLoginAct.this, mFrom);
    }

    @Override
    public void onRequestFail(String msg) {
        hideLoading();
        showToast("login error");
    }
});
```

> The test AppID and secret required by SDK authentication are provided in the sample code and cannot be used in the formal environment.All functions in the sample code can be used normally after logging in。
>

