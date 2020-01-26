---
title: Macbook air安装win10系统（单系统）并安装ubuntu子系统
date: 2019-09-04 16:13:27
tags:
categories:
- 随笔
---

>开发需要ubuntu系统，就想把air安装ubuntu。结果发现win10 的wsl2十分厉害，可以安装ubuntu子系统并且兼容性非常好，决定安装win10
<!--more-->
# 安装win10
## 下载win10镜像并制作安装盘
下载地址 建议下载官方原版，官方肯定是最放心的。  
网上教程一大把 https://zhuanlan.zhihu.com/p/51737001 十分简单  
macbook是开机时按option键进入安装  
淘宝可以买正版激活码 10元左右，没有必要用破解工具
# 安装专属驱动
安装完系统后无驱动会出现各种问题，下载 boortcamp 安装专属驱动  
下载链接 要下载对应型号 https://www.applex.net/pages/bootcamp/  
下载完后解压 到u盘，然后接到新系统运行setup即可。  
安装完重启  
到此，系统就安装完毕，可正常使用
# 提升触控板体验
苹果自带的驱动体验十分不好，建议安装**trackpad** 提升体验  
参考 https://www.zhihu.com/question/40320651  
下载地址 http://trackpad.forbootcamp.org/#download
各种参数自行调节  
飞一般的感觉  
# 安装ubuntu子系统
>wsl2见
https://docs.microsoft.com/en-us/windows/wsl/wsl2-index
总的来说比1提升了好几个档次，兼容性很强，可能window版本原因没有wsl2，先用wsl，兼容性也可以。

ubuntu安装见 https://blog.csdn.net/zhouzme/article/details/78780479

