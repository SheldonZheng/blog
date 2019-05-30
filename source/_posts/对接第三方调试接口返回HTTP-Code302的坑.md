---
title: 对接第三方调试接口返回HTTP Code302的坑
tags:
  - Uncategorized
date: 2017-05-08 12:54:20
---

近日对接一个新的第三方平台，调试他们提供的接口的时候，使用Apache Client总是收不到返回结果,而使用Postman等第三方工具发送同样的headers和body就可以返回结果;

一开始想的很复杂,直接拿出来Wireshark抓包,一抓包发现返回的竟然是302;

![](http://baiye.website/wp-content/uploads/2017/05/WX20170508-125028.png)

图片已经打码处理过了;

然后用curl -v验证了一下,返回的状态码确实是302,这样会导致不支持重定向的代码没法正常收到结果,而Postman等工具支持重定向,就可以发送请求成功;

一般而言,API提供方不会返回302,我遇到的这个问题已经让对方修改解决;

![](http://baiye.website/wp-content/uploads/2017/05/WX20170508-125236.png)