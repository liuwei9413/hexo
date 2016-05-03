title: Linux安装及使用
date: 2016/01/18
categories: 操作系统
tags: [Linux]

---

# 一、安装

## 1、虚拟机软件（VMware安装Virtual Machine）

**VMware**是一个用来虚拟出PC的软件，相当于模拟出一台新的PC，这样就可以在一台电脑上同时运行两个独立的操作系统。
**VMware**的主要特点：
* 不需要重新开机就可同时使用两种操作系统；
* 本机系统可与虚拟机系统网络通信；
* 可以自定义并且可随时修改虚拟机硬件配置；

解压安装——自定义安装 参考[虚拟机VMware10安装](http://jingyan.baidu.com/article/93f9803fea85f4e0e46f55d6.html?qq-pf-to=pcqq.c2c '虚拟机VMware10安装')

## 2、centos安装（Linux发行版之一）

下载地址：http://mirror.bit.edu.cn/centos/7/isos/x86_64/ 选择CentOS-7-x86_64-DVD-1511.iso下载

安装步骤参考： http://www.cnblogs.com/smyhvae/p/3917532.html 注：我安装的时候没有没有遇到该文中的报错提示。

# 二、使用

## Xshell的安装和使用

直接Xshell官网下载：http://www.netsarang.com/xmanager_enterprise_download.html，安装教程官网有英文的，也可以参考：[xshell入门使用教程](http://jingyan.baidu.com/article/295430f13fb4db0c7f005065.html 'xshell入门使用教程')。

# 三、常见问题汇总

## 如何把windows下目录挂载到Linux下？

1. 右键需要挂载的目录——共享——特定用户（选择你想要挂载的用户，保证读取权限）
2. Linux下输入 `sudo mount -t cifs //192.168.100.109/test /test -o username=liuwei,password=123456,rw,uid=0,gid=0`
  - //192.168.100.109/test => 本机ip+共享文件夹名
  - username=liuwei,password=123456 => 用户名及密码
  - rw => 可读写
  - uid,gid => gid:GroupId即组Id，用来标识用户组的唯一标识符 uid:UserId即用户id，用来标识用户的唯一标识符。注：命令行输入id可查询相关id值
 
## 没有ifconfig命令

最小化安装centos，默认不安装ifconfig等命令，这时候终端运行ifconfig会报错![alt command not found](/uploads/images/linux-ifconfig-1.png)	。解决办法是用yum安装ifconfig命令包，终端输入：`yum search ifconfig`，ifconfig命令就在`net-tools.x86_64`这个包里，接下来安装这个包`yum install net-tools.x86_64`。终端输入ifconfig测试。可参考：[centos7没有安装ifconfig命令的解决方法](http://www.centoscn.com/CentosBug/osbug/2014/0916/3750.html 'centos7没有安装ifconfig命令的解决方法') 。

