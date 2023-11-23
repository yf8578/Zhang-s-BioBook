# 准备工作
## Linux环境
对于Linux环境，如果是MacOS或者Linux系统，可以直接使用系统自带的终端，如果是Windows系统，可以使用Windows的子系统，或者使用虚拟机安装Linux系统，下面分别介绍这三种方法。
像一些小的数据或者是自己用来练习的数据，可以直接在本地进行处理，但是如果是大数据，或者是需要长时间运行的程序，就需要在服务器上进行处理，这里推荐使用服务器，因为服务器的配置比较高，而且可以长时间运行，不会像本地电脑一样，运行一段时间就会出现卡顿的情况。
~~还有一个原因，毕竟是服务器嘛，公家的东西不用白不用。~~
1. 登陆服务器
2. 安装虚拟机
3. Windows安装子系统
### 登陆服务器
无论是Windows还是MAcOS，都可以使用ssh登陆服务器。
`ssh username@serverip -p 22`其中username是你的用户名，serverip是服务器的ip地址，-p 22是端口号，如果是默认的端口号，可以不用加这个参数。
如果是Windows系统，可以直接打开PowerShell，输入,就像下面这样：
```
Windows PowerShell
版权所有（C） Microsoft Corporation。保留所有权利。

安装最新的 PowerShell，了解新功能和改进！https://aka.ms/PSWindows

PS C:\Users\10696> ssh zhangyifan1@192.168.61.10 -p 22
(zhangyifan1@192.168.61.10) Password:
(zhangyifan1@192.168.61.10) Verification code:
Last login: Wed Nov 22 20:11:31 2023 from 172.18.160.229
Rocks 7.0 (Manzanita)
Profile built 15:01 19-Jul-2018

Kickstarted 15:19 19-Jul-2018
[zhangyifan1@cngb-login-0-10 13:44:28 (#╯°Д°)╯︵┻━┻ ~]$
```
这样就登陆成功了，如果是第一次登陆，会提示你是否要接受服务器的公钥，输入yes就可以了。
如果是Macos操作是一样的,~~**可惜我没Mac。**~~
除了电脑自带的终端，还有一些好用的第三方终端，如
1. [Tabby](https://tabby.sh/)
2. [Xshell](https://www.netsarang.com/en/xshell/)
3. [MobaXterm](https://mobaxterm.mobatek.net/)
......
### 安装虚拟机
可以参考这篇推文:[超详细的VMware虚拟机安装Linux图文教程保姆级](https://blog.csdn.net/weixin_61536532/article/details/129778310)
### Windows安装子系统
这里推荐使用Ubuntu子系统，因为Ubuntu子系统的安装比较简单，而且使用起来也比较方便。且推荐安装在D盘，因为D盘的读写速度比较快，而且不会占用C盘的空间。
我使用的方法是在微软商店中安装，之后再迁移到D盘中。
**安装子系统：**

1. 打开控制面板<br />
![Alt text](../_book/gitbook/images/%E6%8E%A7%E5%88%B6%E9%9D%A2%E6%9D%BF20231123141357.png)
2. 打开相关设置
![Alt text](../_book/gitbook/images/%E6%89%93%E5%BC%80wsl20231123141427.png)
3. 微软商店搜索wsl安装合适的版本
![微软商店](../_book/gitbook/images/msstore20231123140927.png)
4. 安装完成后，打开子系统，输入用户名和密码，就可以使用了。
![Alt text](../_book/gitbook/images/wsl20231123141828.png)
<br />
**迁移D盘：** https://juejin.cn/post/7024498662935904269
