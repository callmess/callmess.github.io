---
title: gitserver
layout: post

description: "haha"
redirect_from: ["/2017/01/07/gitserver.html"]

---

 * 安装copssh,安装的过程会弹出一个提示让你选择service account 可以自定义也可以不用管.只是个虚拟账号
![](/res/0107/copssh.png)

 * 添加用于登录的用户,password authenticaction不要勾,因为我们是选择使用公钥来登录
![](/res/0107/copssh1.png)

 * 导入公钥: 将客户端生成的公钥导粘贴到下图这里
![](/res/0107/copssh.png)

 * 到了这一步,是可以用ssh命令登录Windows了, 但是登录后的的shell是找不到git的相关命令的
所以还要配置git的path

    D:\Git\cmd

    D:\Git\mingw64\bin

    到这一步成功了! 可以创建仓库测试了

    git init newrepo.git --bare

* 可能出现的问题

  * ssh能正常访问, git命令也能用.但是在git clone总是提示,仓库不存在(实际是存在的),

    ``解决:重启客户端电脑后再次操作就可以了``

  * 貌似git仓库所在的目录必须是在ssh的home目录才行, 试了在不同的盘符没有成功过,

    `解决:根据网上有说是只有相对路径才可以!!!!`

* 好了,可以洗洗睡了, 献上两张风景美图!!



![](/res/jun/17010501.jpg)


![](/res/jun/17010502.jpg)

 * email : [ilxj20@163.com](mailto:ilxj20@163.com?subject=发送邮件Moss&body=邮件内容)
