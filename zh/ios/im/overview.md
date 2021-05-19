# 概述

> LinkV 即时通讯（IM ） SDK 提供了低延时、高并发且稳定可靠的全球即时消息服务，帮助您快速实现直播间聊天室，点对点消息等实时场景应用。

## <a name='1'></a>1、架构介绍

以下为LiveMe用户接入应用为例，使用IM业务的链路流程图。其中，如下图所示，左侧为用户，右侧为源站服务。

![img](https://dl.linkv.io/doc/zh/ios/im/images/im_chain_diagram.png)

## <a name='2'></a>2、整体服务架构

IM服务系统采用服务化架构，可以包含但不限于单聊、群聊、直播间服务，且服务中的消息可以做到自定义，拿LiveMe来说，仅直播间消息目前已达近200余种。

![img](https://dl.linkv.io/doc/zh/ios/im/images/server_architecture.png)

## <a name='3'></a>3、全球加速节点

为了便于全球用户就近接入，及更好的产品体验，本系统部署了全球化加速点，使全球化用户，访问本服务的问题，减化为了就近访问本地服务的问题。全球加速示意图如下：

![img](https://dl.linkv.io/doc/zh/ios/im/images/world_node.png)

