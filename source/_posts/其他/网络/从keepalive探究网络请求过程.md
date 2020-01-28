---
title: 从keepalive探究网络请求过程
date: 2019-12-27 16:13:27
tags:
- 待续
categories:
- 网络
---

>最近搭建rabbitmq的集群，搭建完成后需要用代理把请求转发到对应节点，  
但是代理如nginx也是单点的，不符合集群高可用特点，故想到了vip，发现自己对网络请求过程不是很熟悉。  
故进行一番研究。

<!--more-->
## keepalive
**keepalived是什么？**

Keepalived软件起初是专为LVS负载均衡软件设计的，用来管理并监控LVS集群系统中各个服务节点的状态，后来又加入了可以实现高可用的VRRP (Virtual Router Redundancy Protocol ,虚拟路由器冗余协议）功能。因此，Keepalived除了能够管理LVS软件外，还可以作为其他服务（例如：Nginx、Haproxy、MySQL等）的高可用解决方案软件

keepalived的高可用解决方案：  
通过VRRP功能虚拟一个ip出来（vip）,所有访问都通过vip访问,而通过vip访问的请求通过VRRP转移到对应的ip

## 参考资料
[生产环境之Nginx高可用方案](https://www.cnblogs.com/SimpleWu/p/11004902.html)