---
title: 树莓派USB摄像头和motion实现网络监控
layout: post

description: "树莓派USB摄像头和motion实现网络监控"
redirect_from: ["/2017/12/03/usb-motion.html"]

---
raspbian 下很简单，直接安装 motion 即可：

sudo apt-get install motion
不过需要手工打开服务配置：

sudo nano /etc/default/motion
将 start_motion_daemon=no

修改为：
start_motion_daemon=yes
处理一个小的权限问题：

sudo chmod 777 /var/lib/motion
再 sudo service motion start

启动服务。
默认会使用 /dev/video0

这个设备，请确定 USB 摄像头插上去，能否 lsusb 列出，并且设备映射成功。
在路由器开放外网端口之前可以修改 /etc/motion/motion.conf

文件中以下配置：

width 640
height 480 # 视频大小
text_right Larry Li(Shenzhen)\n%Y-%m-%d %T-%q # 右下角文字
text_left CAMERA rpi1 # 左下角文字
target_dir /var/lib/motion # 文件存放位置，需要 chmod 777
picture_filename %Y%m%d/%H%M%S-%v-%q # 也可以按 %Y/%m/%d/%H%M%S-%v-%q 年月日一层一层建目录存放
movie_filename %Y%m%d/%H%M%S-%v # 其他几个 filename 配置也相同处理
stream_port 8081 # 指定实时 http 监控端口
stream_localhost off # 需要将 on 修改为 off 取消仅 localhost 访问限制
stream_limit 2 # 最好设置一个访问数限制
stream_auth_method 1 # 1 是标准的 basic auth
stream_authentication username:password # 用户名和密码
webcontrol_port 0 # 关闭控制端口，或者也设置 basic auth 的用户名和密码
然后使用 btsync 把 /var/lib/motion

共享给手机和远程电脑，我直接使用了 rw 读写模式，手工在远程删除旧文件。
