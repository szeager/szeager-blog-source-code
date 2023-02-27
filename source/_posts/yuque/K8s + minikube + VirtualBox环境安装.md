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

![1](/images/yuque/K8s+minikube+VirtualBox环境安装/1.png)

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

![2](/images/yuque/K8s+minikube+VirtualBox环境安装/2.png)

## 4、启动

```
启动VirtualBox

VirtualBox

启动minikube

minikube start

minikube dashboard
```

![3](/images/yuque/K8s+minikube+VirtualBox环境安装/3.png)

# 问题

## 1、minikube Unable to start VM: Error loading existing host

一开始使用 brew install minikube，去安装 minikube， 在 minikube start 时遇到了问题。

![4](/images/yuque/K8s+minikube+VirtualBox环境安装/4.png)
minikube delete 删除现有虚机，什么的都不生效，
然后直接卸载当前的 minikube，并且删除 ~/.minikube 目录缓存的文件

```
// 卸载
brew cask uninstall --force minikube

// 删除缓存目录
sudo rm -rf ~/.minikube
```
