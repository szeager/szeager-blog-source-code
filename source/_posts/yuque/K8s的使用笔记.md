---
title: K8s的使用笔记
urlname: sciomr
date: '2019-04-17 19:34:15 -0700'
tags: []
categories: []
---

# 1、创建一个集群

## 查看版本

$> minikube version
minikube version: v0.15.0-katacoda

## 启动集群

$> minikube start
![1](/images/yuque/K8s的使用笔记/1.png)

## 查看版本

$> kubectl version
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e09955
4f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z",
GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e09955
4f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"1970-01-01T00:00:00Z",
GoVersion:"go1.7.1", Compiler:"gc", Platform:"linux/amd64"}

## 查看集群状态

$> kubectl cluster-info
![2](/images/yuque/K8s的使用笔记/2.png)

## 获取可用的 node

$> kubectl get nodes
![3](/images/yuque/K8s的使用笔记/3.png)

# 2、部署应用

kubectl run kubernetes-bootcamp --image=docker.io/jocatalin/kubernetes-bootcamp:v1 --port=8080
![4](/images/yuque/K8s的使用笔记/4.png)

查看当前 pods
![5](/images/yuque/K8s的使用笔记/5.png)
