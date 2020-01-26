---
title: linux 常用命令
date: 2019-11-23 16:13:27
categories: 
- [linux]
tags: 
- 持续更新
---

> 记录经常忘记的命令  
<!--more-->

## 网络
查看端口占用
netstat -tunlp |grep 端口号
## 防火墙
1、firewalld的基本使用
启动： systemctl start firewalld
查看状态： systemctl status firewalld
停止： systemctl disable firewalld
禁用： systemctl stop firewalld
 
2.systemctl是CentOS7的服务管理工具中主要的工具，它融合之前service和chkconfig的功能于一体。
启动一个服务：systemctl start firewalld.service
关闭一个服务：systemctl stop firewalld.service
重启一个服务：systemctl restart firewalld.service
显示一个服务的状态：systemctl status firewalld.service
在开机时启用一个服务：systemctl enable firewalld.service
在开机时禁用一个服务：systemctl disable firewalld.service
查看服务是否开机启动：systemctl is-enabled firewalld.service
查看已启动的服务列表：systemctl list-unit-files|grep enabled
查看启动失败的服务列表：systemctl --failed

3.配置firewalld-cmd

查看版本： firewall-cmd --version
查看帮助： firewall-cmd --help
显示状态： firewall-cmd --state
查看所有打开的端口： firewall-cmd --zone=public --list-ports
更新防火墙规则： firewall-cmd --reload
查看区域信息:  firewall-cmd --get-active-zones
查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0
拒绝所有包：firewall-cmd --panic-on
取消拒绝状态： firewall-cmd --panic-off
查看是否拒绝： firewall-cmd --query-panic
 
那怎么开启一个端口呢
添加（--permanent永久生效，没有此参数重启后失效）
firewall-cmd --zone=public --add-port=7001/tcp --permanent
重新载入
firewall-cmd --reload
查看
firewall-cmd --zone=public --query-port=8081/tcp
查看所有
firewall-cmd --list-all
firewall-cmd --list-ports

删除
firewall-cmd --zone=public --remove-port=8081/tcp --permanent

指定同网段的访问某个端口，其他网段不能访问
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="10.2.64.53" port protocol="tcp" port="7001" accept'
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="10.8.7.123" port protocol="tcp" port="8082" accept'
firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="10.2.158.87" port protocol="tcp" port="8085" accept'


查看rich配置
firewall-cmd --list-rich-rules
删除
firewall-cmd --permanent --zone=public --remove-rich-rule='rule family="ipv4" source address="10.2.64.53" port port="7001" protocol="tcp" accept'

keepalived开通防火墙vrrp
firewall-cmd --direct --permanent --add-rule ipv4 filter INPUT 0 --in-interface team0 --destination 224.0.0.18 --protocol vrrp -j ACCEPT

查
firewall-cmd --permanent --direct --get-all-rules

## 打开查看打开文件
[参考](https://www.cnblogs.com/chenjinxi/p/8268324.html)
查看进程打开文件
lsof -p 进程号
加 |wc l 可以统计

## 赋权


## 日志处理
过滤某一个时间段的日志：
sed -n '/2017-5-18 9:51:13/,/2017-5-18 9:55:13/p' test1.log
