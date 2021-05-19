# 架构

**更新时间：2020-08-19**

## 1、架构设计
LinkV **社交娱乐**解决方案(属SAAS服务) 采用SAAS集成方案，接入需要客户端与服务端同步进行。

## 2、集成时序图
客户端SDK的使用依赖从服务端获取的**live_open_id**与**live_token**，因此需要优先接入服务端。

![img](https://dl.linkv.io/doc/zh/ios/live/images/live_install.png)

## 3、支付时序图
支付中需要使用客户端先通过SDK获取的**order_id**才能完成支付完成

![img](https://dl.linkv.io/doc/zh/ios/live/images/live_pay_install.png)

> 该order_id被LinkV当作唯一订单，后续对账的唯一凭证，接入方需维护该订单号(order_id)与对应支付记录的绑定关系
> 