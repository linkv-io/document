# Architecture

**Update date：2020-08-19**

## 1、Architecture design
LinkV **Social Entertainment**Solutions (SAAS services) adopt SAAS integration solutions，and need user end and server end access at the same time。

## 2、Integrated Sequence diagram
The use of the client SDK depends on the server**live_open_id**and**live_token**，therefore,priority access to the server is required。

![img](https://dl.linkv.io/doc/en/ios/live/images/live_install.png)

## 3、Payment sequence diagram
During the payment,need to use the **order_id** obtained by the client through SDK to complete the payment.

![img](https://dl.linkv.io/doc/en/ios/live/images/live_pay_install.png)

> This order_id is treated as the only order by LinkV，and the only proof of subsequent reconciliation，The access party needs to maintain the binding relationship between thsi(order_id) and the corresponding payment record
> 