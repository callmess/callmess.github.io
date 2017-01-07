---
title: 一台电脑使用两个github账号
layout: post

description: "我们有两个github账号要用,但是我们只有一个Git环境怎么办呢? learn more >>"
redirect_from: ["/2017/01/08/twogithubuser.html"]

---
* 两个账号想要相互没有影响的工作,需要配置连个不同的 id_rsa 并且区分命名
 **ssh-keygen -t rsa -C "ilxj586@gmail.com" 
保存文件时注意区分命名(不要覆盖原有的id_rsa)
添加密钥 : ssh-add ~/.ssh/id_rsa_gmail
创建配置文件 config
添加如下内容:
 Default github user(ilxj20@163.com)
Host github.com
HostName github.com
User git
IdentityFile /Users/ss/.ssh/id_rsa

# second user(ilxj586@gmail.com)
Host gm.github.com
HostName github.com
User git
IdentityFile /Users/ss/.ssh/id_rsa_gmail

### 联系我
 * email : [ilxj20@163.com](mailto:ilxj20@163.com?subject=sen to Moss&body=邮件内容)
 <!-- subject后面不能跟中文,否则后果很杯具-->
