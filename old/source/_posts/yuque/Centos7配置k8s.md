---
title: Centos7配置k8s
urlname: ceumd3
date: '2020-04-07 06:04:35 -0700'
tags: []
categories: []
---

环境
系统 ：Centos 7 
cluster: 一台 master 一台 node

1、先把 wget 安装上

> [root@master01 ~]# yum -y install wget

2、把/etc/yum.repos.d/目录下所有的 repo 文件移动到其他目录，例如 bak/，
然后下载 Centos-7.repo。【因为添加 K8s 仓库的时候会报错，这步解决了这个问题，把步骤提前】

```
[root@master01 ~]# mkdir bak
[root@master01 ~]# mv *.repo bak/
[root@master01 ~]# wget http://mirrors.aliyun.com/repo/Centos-7.repo

参考：https://blog.csdn.net/kelvin_yin/article/details/86674703
```

3、K8s 镜像仓库

```
1 新增kubernetes源

[root@master01 ~]# cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF

k8仓库部署方法请参考 https://developer.aliyun.com/mirror/kubernetes?spm=a2c6h.13651102.0.0.3e221b11SW3mYV
```

### 更新 yum 缓存

```
[root@master01 ~]# yum clean all
[root@master01 ~]# yum makecache
[root@master01 ~]# yum update

刚才安装docker时遇到问题yum [Errno 256] No more mirrors to try 解决方法：

1.yum clean all
2.yum makecache
3.yum update
```

### 安装 docker、kubelet、kubeadm、kubecli。

```
[root@master01 ~]# yum install kubectl kubeadm kubecli -y --nogpgcheck
[root@master01 ~]# yum install docker -y
```

### 安装 docker 底层工具

```
[root@master01 ~]# yum install -y yum-utils device-mapper-persistent-data lvm2
```

### 设置 Docker 源

```
[root@master01 ~]# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

[root@master01 ~]# yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo //阿里云yum源
```

### docker 安装版本查看

```
[root@master01 ~]# yum list docker-ce --showduplicates | sort -r
```

### 安装 docker

```
[root@master01 ~]# yum install docker-ce-18.09.9 docker-ce-cli-18.09.9 containerd.io -y
// 指定安装的docker版本为18.09.9
```

##

### 启动 Docker

```
[root@master01 ~]# systemctl start docker
[root@master01 ~]# systemctl enable docker
```

### linux 命令自动补全

### 安装 bash-completion

```
[root@master01 ~]# yum -y install bash-completion
```

### 加载 bash-completion

```
[root@master01 ~]# source /etc/profile.d/bash_completion.sh
```

_registry.cn-qingdao.aliyuncs.com/kubernetes-image_
\_
[https://www.kubernetes.org.cn/6632.html](https://www.kubernetes.org.cn/6632.html)

https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/ errno
