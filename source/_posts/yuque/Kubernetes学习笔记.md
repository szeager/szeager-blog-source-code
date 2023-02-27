---
title: Kubernetes学习笔记
urlname: fx5d8u
date: '2020-04-13 06:17:35 -0700'
tags: []
categories: []
---

一、概念理论
k8s
k8s 是一组服务器集群，k8s 所管理的集群节点上的容器

功能
自我修复
弹性伸缩:实现根据服务器的并发情况，增加或缩减容器数量
自动部署
回滚
服务发现和负载均衡
机密和配置共享管理

两类节点
master node: 主
worker node: 工作

master 节点的组件(程序)
apiserver 接收客户端操作 k8s 的指令（增删查改）
scheduler 调度-从多个 worker node 节点的组件中选举一个来启动服务
controller manager 向 worker 节点的 kubelet 发送指令 （控制后端节点启动 Docker 容器）
etcd 数据库
分布式键值存储系统。
用于保存集群状态数据，比如 Pod,Service 等对象信息

worker 节点的组件(程序)
kubelet 向 docker 发送指令，管理 docker 容器（启动 docker 镜像）
kubeproxy   管理 docker 容器的网络

![1](/images/yuque/Kubernetes学习笔记/1.png)

核心概念
Pod
最小部署单元
可以有一个或者多个容器的一组容器的集合
又称为容器组
一个 Pod 中的容器共享网络命名空间
是短暂的

controller: 控制器，控制 pod，启动、停止、删除
ReplicaSet
Deployment
Statefulset
DaemonSet
Job
Cronjob: 定时任务

Service ：服务--防止 Pod 失联
将一组 pod 关联起来，提供一个统一的入口

Label :   标签
一组 Pod 有一个统一的标签
servicie 是通过标签和一组 pod 进行关联

Namespace: 名称空间

隔离 pod 运行，在逻辑上彼此隔离（默认情况下，pod 是可以相互访问的）
为不同的用户提供隔离的 pod 运行环境
为开发环境、测试环境、生产环境分别准备不同的名称空间，进行隔离

二、搭建一个完整的 Kubernetes 集群
1、生产环境 K8s 平台规划
2、服务器硬件配置推荐
3、官方提供三种部署方式
4、为 Etcd 和 APIService 自带 SSL 证书
5、Etcd 数据库集群部署
6、部署 Master 组件
7、部署 Node 组件
8、部署 k8s 集群网络
9、部署 WebUI(DashBoard)
10、部署集群内部 DNS 解析服务（CoreDNS）
