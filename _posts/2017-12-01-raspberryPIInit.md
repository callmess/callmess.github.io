---
title: 初次玩机体验
layout: post

description: "刚买到手的树莓派 很不出意外的遇到了各种问题 >>"
redirect_from: ["/2017/12/01/raspberryPIInit.html"]

---
第一次玩树莓派 ,买的是装好系统的版本. 碰到了几个问题,记录下:
* 么有显示器, 买来这个本来就没打算为它专门配置一个显示器,所以也就相当于瞎子了...  怎么办? ssh远程连接
* IP地址无法知道, 因为没有显示器无法查看IP ...  网线连接到路由器,到路由器查看IP (网上还介绍网段扫描IP的也行)  
* 无法ssh登录 , 默认是禁用了.启用方法是脸上显示器键鼠用命令启动  
 ```
service ssh start # 不是sshd是ssh
```
开机启动ssh:  
  sudo update-rc.d ssh enable (debian)

* 修改pi密码和启用root用户   
修改密码 直接 passwd pi 默认密码是raspberry ,现在我的密码是pi   
启用root直接 sudo passwd root 设置密码就好

* vnc远程连接桌面分辨率太小   
 在命令行执行 vncserver -geometry 1920x1080
(分辨率) 设置需要连接的桌面的分辨率大小   
最后会返回 New desktop is raspberrypi:1 (192.168.199.149:1)  
就可以用192.168.199.149:1这个地址登录了

* 更换软件源（apt-get sources）  
  官方有提供一个镜像列表：http://www.raspbian.org/RaspbianMirrors     
  编辑 /etc/apt/sources.list 文件 删掉旧的镜像地址换成新的地址
例如浙江大学的:  
deb http://mirrors.zju.edu.cn/raspbian/raspbian/ jessie main contrib non-free rpi  
deb-src http://mirrors.zju.edu.cn/raspbian/raspbian/ jessie main contrib non-free rpi  
(一般会有配置帮助说明)  
编辑此文件后，使用sudo apt-get update命令，更新软件列表

## Ps : sudo raspi-config 树莓派的配置命令
