---
title: CentOS7 最小安装遇到的问题
layout: post

description: "ContOS最小安装,很多工具命令都是没有的,包括ifconfig命令"
redirect_from: ["/2017/01/08/twogithubuser.html"]

---
* #### 问题一: ifconfig: command not found ##
![失败信息](/res/0210/1.png)

能百度到的都是相互转载的,并不能解决我的问题  
此时是上不了网的  
还要万能的Google还是可以找到决绝方法的

执行命令 ip addr  查看网卡(一般是eth0,我的是enp7s0f5)是没有获取到IP的
到/etc/sysconfig/network-scripts 找网卡对应的文件
![](/res/0210/2.png)

用vi打开编辑,确保配置了开机启动dhcp  bootproto=dhcp, onboot=yes
![](/res/0210/3.png)

重启 reboot , 即可获取到IP,用 ip addr查看IP已正确获取,ping baidu.com可ping通
![](/res/0210/4.png)

此时 ifconfig命令依旧不能用,
yum -y install net-tools 安装后ifconfig命令即可正常使用
![](/res/0210/5.png)
参考
[http://www.cnblogs.com/dunitian/p/4974761.html](http://www.cnblogs.com/dunitian/p/4974761.html)  
[http://centoshowtos.org/blog/ifconfig-on-centos-7/](http://centoshowtos.org/blog/ifconfig-on-centos-7/)

* #### 问题二 :每隔几秒弹出 [  132.5XXXXX] jme 0000:07:00.5 enp7s0f5: UDP Checlsum error ###
执行命令 ethtool  --offload enp7s0f5 rx off  解决问题
![](/res/0210/6.png)

参考:[http://superuser.com/questions/559236/how-to-get-rid-of-udp-checksum-error-messages-in-virtual-console](http://superuser.com/questions/559236/how-to-get-rid-of-udp-checksum-error-messages-in-virtual-console)


其他问题: Mac无法远程到新安装的该系统,因为host key变了
![](/res/0210/7.png)

找到 know_host文件,用vi编辑删掉对应IP的记录
![](/res/0210/8.png)

重新登录,OK
![成功](/res/0210/9.png)


### 联系我
 * email : [ilxj20@163.com](mailto:ilxj20@163.com?subject=sen to Moss&body=邮件内容)
 <!-- subject后面不能跟中文,否则后果很杯具-->
