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
![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555554972516-d66f3af1-cf86-4526-8ce5-1c14038fce18.png#align=left&display=inline&height=276&name=image.png&originHeight=276&originWidth=528&size=66687&status=done&width=528)

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
![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555555012422-e5fd9cfe-9145-44f2-85eb-bac190515354.png#align=left&display=inline&height=118&name=image.png&originHeight=118&originWidth=534&size=21951&status=done&width=534)

## 获取可用的 node

$> kubectl get nodes
![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555555039243-61295b89-5c96-4eab-94b7-209e1e650c6a.png#align=left&display=inline&height=52&name=image.png&originHeight=52&originWidth=330&size=8505&status=done&width=330)

# 2、部署应用

kubectl run kubernetes-bootcamp --image=docker.io/jocatalin/kubernetes-bootcamp:v1 --port=8080
![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555555187839-a4d3df16-9859-4f86-8417-58db6f379699.png#align=left&display=inline&height=102&name=image.png&originHeight=102&originWidth=542&size=22409&status=done&width=542)

查看当前 pods
![image.png](https://cdn.nlark.com/yuque/0/2019/png/290620/1555555358574-95bb7028-50a7-4e64-845a-cc1a4d6bb0c7.png#align=left&display=inline&height=94&name=image.png&originHeight=94&originWidth=513&size=11465&status=done&width=513)
