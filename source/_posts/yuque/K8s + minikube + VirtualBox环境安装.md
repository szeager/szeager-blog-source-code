---
title: K8s + minikube + VirtualBox环境安装
urlname: seoatt
date: '2019-04-17 00:43:56 -0700'
tags: []
categories: []
---

# 安装

## 1、安装 brew

> brew  全称 Homebrew，是 Mac OSX 上的软件包管理工具，能在 Mac 中方便的安装软件或者卸载软件。

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## 2、安装 kubectl

```
brew install kubectl
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555487062618-7bccde11-a75a-4ce0-872d-83bb5e59040f.png#align=left&display=inline&height=241&name=image.png&originHeight=241&originWidth=453&size=39218&status=done&width=453)

## 3、安装 VirtualBox

```
brew cask install virtualbox
```

## 3、安装 minikube

```
brew cask install minikube
或者 阿里云minikube源:
curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v1.0.0/minikube-darwin-amd64 && sudo chmod +x minikube && sudo mv minikube /usr/local/bin/

阿里云minikube源:  https://github.com/AliyunContainerService/minikube
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555487071495-1f9f2702-5b0f-42cc-a7b6-b6c02c2d5d3a.png#align=left&display=inline&height=122&name=image.png&originHeight=122&originWidth=472&size=23992&status=done&width=472)

## 4、启动

```
启动VirtualBox

VirtualBox

启动minikube

minikube start

minikube dashboard
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555487526698-6dd62268-502a-4220-8256-24d95378f285.png#align=left&display=inline&height=956&name=image.png&originHeight=956&originWidth=1909&size=131424&status=done&width=1909)

# 问题

## 1、minikube Unable to start VM: Error loading existing host

一开始使用 brew install minikube，去安装 minikube， 在 minikube start 时遇到了问题。
![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555493610722-5ff301b1-9b0c-46e1-a8a4-5009b1a71415.png#align=left&display=inline&height=405&name=image.png&originHeight=405&originWidth=438&size=58630&status=done&width=438)
minikube delete 删除现有虚机，什么的都不生效，
然后直接卸载当前的 minikube，并且删除 ~/.minikube 目录缓存的文件

```
// 卸载
brew cask uninstall --force minikube

// 删除缓存目录
sudo rm -rf ~/.minikube
```
