---
title: 记录安装vim失败和解决过程
layout: post

description: "sudo apt-get install -y vim 安装vim 但是很遗憾并不顺利... >>"
redirect_from: ["/2017/12/01/installvimraspbian.html"]

---
###### 系统 : raspbian
###### 安装方法 : sudo apt-get install -y vim
**报错信息**:
```Err:1 http://mirrordirector.raspbian.org/raspbian stretch/main armhf vim-runtime all 2:8.0.0197-4
  404  Not Found [IP: 93.93.128.193 80]
Err:2 http://mirrordirector.raspbian.org/raspbian stretch/main armhf vim armhf 2:8.0.0197-4
  404  Not Found [IP: 93.93.128.193 80]
E: Failed to fetch http://mirrordirector.raspbian.org/raspbian/pool/main/v/vim/vim-runtime_8.0.0197-4_all.deb  404  Not Found [IP: 93.93.128.193 80]
E: Failed to fetch http://mirrordirector.raspbian.org/raspbian/pool/main/v/vim/vim_8.0.0197-4_armhf.deb  404  Not Found [IP: 93.93.128.193 80]
E: Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?

```

初步判断是到软件源的网络通信问题  

**解决办法** : 换软件源 (见初次玩机体验)

- 执行 sudo apt-get install -y vim
还是报错!  
**错误信息**:

``` python 
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 vim : Depends: vim-common (= 2:7.4.488-7+deb8u3) but 2:8.0.0197-4 is to be installed
E: Unable to correct problems, you have held broken packages.
```


- 百度说要update 软件源和系统,分析应该是不同的软件源的软件版本不容的原因,已经安装了高版本的包但是当前软件源的版本比这个版本低

**办法**: 删除掉原来的包 sudo apt-get remove vim-common

- 再执行安装命令 :sudo apt-get install -y vim

**成功安装** :

``` python
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
 vim-common vim-tiny
0 upgraded, 0 newly installed, 2 to remove and 60 not upgraded.
After this operation, 1,132 kB disk space will be freed.
Do you want to continue? [Y/n] Y
(Reading database ... 122662 files and directories currently installed.)
Removing vim-tiny (2:8.0.0197-4) ...
Removing vim-common (2:8.0.0197-4) ...
Processing triggers for mime-support (3.60) ...
Processing triggers for desktop-file-utils (0.23-1) ...
Processing triggers for man-db (2.7.6.1-2) ...
Processing triggers for gnome-menus (3.13.3-9) ...
Processing triggers for hicolor-icon-theme (0.15-1) ...
pi@raspberrypi:/etc/apt $ sudo apt-get install -y vim
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
 vim-common vim-runtime
Suggested packages:
 ctags vim-doc vim-scripts
The following packages will be REMOVED:
 xxd
The following NEW packages will be installed:
 vim vim-common vim-runtime
0 upgraded, 3 newly installed, 1 to remove and 60 not upgraded.
Need to get 6,042 kB of archives.
After this operation, 28.2 MB of additional disk space will be used.
Get:1 http://mirrors.ustc.edu.cn/raspbian/raspbian jessie/main armhf vim-common armhf 2:7.4.488-7+deb8u3 [185 kB]
Get:2 http://mirrors.ustc.edu.cn/raspbian/raspbian jessie/main armhf vim-runtime all 2:7.4.488-7+deb8u3 [5,048 kB]
Get:3 http://mirrors.ustc.edu.cn/raspbian/raspbian jessie/main armhf vim armhf 2:7.4.488-7+deb8u3 [810 kB]                                                     
Fetched 6,042 kB in 10s (602 kB/s)                                                                                                                             
(Reading database ... 122602 files and directories currently installed.)
Removing xxd (2:8.0.0197-4) ...
Selecting previously unselected package vim-common.
(Reading database ... 122591 files and directories currently installed.)
Preparing to unpack .../vim-common_2%3a7.4.488-7+deb8u3_armhf.deb ...
Unpacking vim-common (2:7.4.488-7+deb8u3) ...
Selecting previously unselected package vim-runtime.
Preparing to unpack .../vim-runtime_2%3a7.4.488-7+deb8u3_all.deb ...
Adding 'diversion of /usr/share/vim/vim74/doc/help.txt to /usr/share/vim/vim74/doc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim74/doc/tags to /usr/share/vim/vim74/doc/tags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:7.4.488-7+deb8u3) ...
Selecting previously unselected package vim.
Preparing to unpack .../vim_2%3a7.4.488-7+deb8u3_armhf.deb ...
Unpacking vim (2:7.4.488-7+deb8u3) ...
Processing triggers for mime-support (3.60) ...
Processing triggers for desktop-file-utils (0.23-1) ...
Setting up vim-common (2:7.4.488-7+deb8u3) ...
Installing new version of config file /etc/vim/vimrc ...
Processing triggers for man-db (2.7.6.1-2) ...
Setting up vim-runtime (2:7.4.488-7+deb8u3) ...
Processing /usr/share/vim/addons/doc
Processing triggers for gnome-menus (3.13.3-9) ...
Processing triggers for hicolor-icon-theme (0.15-1) ...
Setting up vim (2:7.4.488-7+deb8u3) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdiff) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in auto mode
```
