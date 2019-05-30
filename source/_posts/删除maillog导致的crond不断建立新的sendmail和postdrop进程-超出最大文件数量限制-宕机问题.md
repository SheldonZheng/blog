---
title: 删除maillog导致的crond不断建立新的sendmail和postdrop进程 超出最大文件数量限制 宕机问题
tags:
  - Linux
date: 2017-05-15 11:56:51
---

近日把Linode服务器从新加坡机房迁移至日本机房，迁移前尝试清理一些磁盘空间  经过检查 发现/var/spool/postfix/maildrop/ 里面有非常多的小文件 合在一起占了1.6G的磁盘空间

随便搜了下 说可以删掉 就直接rm -rf掉 之后关闭服务器开始迁移了

&nbsp;

迁移之后的第一天  惯例去检查一下/var/log/secure 文件 发现有几万次暴力破解sshd密码的重试……把ssh的端口从默认的22换了另外一个 就没有这些请求了

当天晚上20：00左右开始出现CPU占用100% 一直持续到第二天早上SS不能用我才发现 此时无法ssh连接上去 只能通过Linode的控制台手动重启

&nbsp;

重启之后一切正常 查看是不是有可疑的程序 当时怀疑被种马了  检查了一圈都没啥问题 先放下了

&nbsp;

第二天晚上又出现一样的问题 再次重启 惯例检查系统日志 发现/var/log/maillog非常巨大 tail一下这个文件 一会就打印出来一条warn

&nbsp;

随后去查了一下sendmail和postdrop相关资料 观察了一会系统 发现crond每几分钟就会开启一个新的sendmail和postdrop进程 初步推断是由于最后开启的进程过多 导致fd被占满

因为Linux一切都是file fd被占满了导致没法创建新的连接 所以问题出现之时才会无法通过ssh连接

&nbsp;

搜索引擎搜了一下 发现/etc/cron.d/sysstat每隔十分钟会定时执行一次 里面的执行命令会报错 一旦报错 就会启动sendmail和postdrop进程;

&nbsp;

修复方法：

/etc/cron.d/sysstat 修改此文件 为里面的每一个命令加上 &amp;&gt;/dev/null   就不会启动sendmail和postdrop进程