# Overview

> LinkV Instant Messaging (IM) SDK provides a low-latency, high-concurrency, and stable and reliable global instant messaging service to help you quickly implement real-time scene applications such as live chat rooms and peer-to-peer messaging.


## <a name='1'></a>1、Architecture introduction


The following is an example of LiveMe user access application, using IM service link flow chart. Among them, as shown in the figure below, the left side is the user, and the right side is the origin site service.

![img](https://dl.linkv.io/doc/en/android/im/images/im_chain_diagram.png)

## <a name='2'></a>2、Overall service architecture


The IM service system adopts a service-oriented architecture, which can include but is not limited to single chat, group chat, and live room services, and the messages in the service can be customized. For LiveMe, there are currently more than 200 types of live room messages alone. .

![img](https://dl.linkv.io/doc/en/android/im/images/server_architecture.png)

## <a name='3'></a>3、Global acceleration node


In order to facilitate the nearby access of global users and a better product experience, this system deploys a globalization acceleration point, so that the problem of global users accessing this service is reduced to the problem of accessing local services nearby. The global acceleration diagram is as follows:

![img](https://dl.linkv.io/doc/en/android/im/images/world_node.png)

