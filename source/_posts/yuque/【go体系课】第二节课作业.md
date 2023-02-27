---
title: 【go体系课】第二节课作业
urlname: xtodfv
date: '2021-05-20 06:47:07 -0700'
tags: [golang]
categories: [计算机]
typora-root-url: ../../..
---

### 必做：channel ⼀⻚中，找出所有红线报错在 runtime 中的位置

#### ![1](/images/yuque/【go体系课】第二节课作业/1.png)

#### send on closed channel

![2](/images/yuque/【go体系课】第二节课作业/2.png)

#### close of closed channel

![3](/images/yuque/【go体系课】第二节课作业/3.png)

#### 测试代码

```
package main

// close of nil channel
func main() {
	var ch chan int
	close(ch)
	ch <- 1
}

// close of closed channel
func main() {
	ch := make(chan int, 1)
	ch <- 1
	close(ch)
	close(ch)
}

// send on closed channel
func main() {
	ch := make(chan int, 1)
	ch <- 1
	close(ch)
	ch <- 2

}

```

#### panic 源代码

![4](/images/yuque/【go体系课】第二节课作业/4.png)

![5](/images/yuque/【go体系课】第二节课作业/5.png)

### 选做 1：修复[https://golearn.coding.net/p/gonggongbanji/files/all/DF12](https://golearn.coding.net/p/gonggongbanji/files/all/DF12)中的 test case

![6](/images/yuque/【go体系课】第二节课作业/6.png)

### 选做 2：扩展其功能，增加更多的操作符号⽀持(随意发挥)
