---
title: Window和Centos我都要。
urlname: rasq2b
date: '2020-04-05 07:04:00 -0700'
tags: []
categories: []
---

# 一、先安装 Windows 系统

1、制作启动盘
2、更改 bios 启动项、选择 U 盘启动
3、进入 PE 系统，划分好分区，安装自己下好的 window 系统。

# 二、安装 Centos

## 1、UltraISO 刻录镜像至 U 盘内

第一步，打开 CentOS-7-x86_64-DVD-1511.iso 镜像文件；
第二步，选择打开的镜像文件，点击菜单栏中的**启动-写入硬盘镜像**；
第三步，选择磁盘驱动器（U 盘所在位置），选中写入方式为**USB-HDD+**，点击写入。

## 2、准备磁盘空闲区域

第一步，打开磁盘管理器，**计算机-管理-磁盘管理**；
第二步，选择**压缩卷**或者**删除卷**，获取空闲区域。

## 3、重启电脑，选择 U 盘启动安装 CentOS 系统

### ①、重启电脑，进入 Bios，选择 U 盘启动；

### ②、进入安装界面，选择 Install CentOS7 项，进行安装； 

### ③、安装时出现问题【 Warning: dracut-initqueue timeout - starting timeout scripts】

#### 确认好 CentosU 盘的标签

![image.png](https://cdn.nlark.com/yuque/0/2020/png/290620/1586098411239-68e9d140-85ec-481d-97c0-208af95d4397.png#align=left&display=inline&height=466&name=image.png&originHeight=932&originWidth=1760&size=66439&status=done&style=none&width=880)

#### 在安装 CentOS7，【Install CentOS 7】时，按 Tab 键，进行编辑

![image.png](https://cdn.nlark.com/yuque/0/2020/png/290620/1586098735136-c95010b6-d32e-431d-8b09-a34b3777407f.png#align=left&display=inline&height=446&name=image.png&originHeight=892&originWidth=1204&size=1476971&status=done&style=none&width=602)

```
默认是：vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=CentOS\x207\x20x86_64 rd.live.check quiet

修改成U盘的标签
vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=CENTOS\x207\x20x8 quiet

```

### ④、选择语言（这里选择简体中文），默认最小安装，按自己需求安装，安装的时候可以设置账号和密码

## 4、没有网络，ifconfig command not found

```
1、查看网络
root# ip addr

2、修改网卡配置文件
root# $vim /etc/sysconfig/network-scripts/ifcfg-enxxx
打开文件后ONBOOT为yes

3、重启网卡
centos6的网卡重启方法：service network restart
centos7的网卡重启方法：systemctl restart network

4、ifconfig command not found
root# cd /sbin
root# ls | grep 'ifconfig'
// 没有则说明没有安装。
// 需要进行安装
root# sudo yum installnet-tools
```

参考文献：
[https://blog.csdn.net/yangsong4353/article/details/87876786](https://blog.csdn.net/yangsong4353/article/details/87876786)
[https://blog.csdn.net/weixin_34416649/article/details/93367249](https://blog.csdn.net/weixin_34416649/article/details/93367249)
[https://www.cnblogs.com/freeweb/p/5213877.html](https://www.cnblogs.com/freeweb/p/5213877.html)
[https://blog.csdn.net/mengxiangjia_linxi/article/details/78965103](https://blog.csdn.net/mengxiangjia_linxi/article/details/78965103)
