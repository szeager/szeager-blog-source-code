---
title: 【go体系课】第一节课作业
urlname: somslw
date: '2021-05-17 06:59:13 -0700'
tags: [golang]
categories: [计算机]
---

### 1、部署好本机的 docker 环境，使用 ppt 中的 dockerfile build 自己的环境

```
➜  mkdir docker_test
➜  cd docker_test
➜  touch Dockerfile
➜  docker_test ls
Dockerfile
➜  cd docker_test
➜  sudo  docker build -t test .
```

![1](/images/yuque/【go体系课】第一节课作业/1.png)

```
➜  docker_test sudo docker images
REPOSITORY    TAG       IMAGE ID       CREATED              SIZE
test          latest    8f7733761a0d   About a minute ago   762MB
hello-world   latest    d1165f221234   2 months ago         13.3kB
centos        latest    300e315adb2f   5 months ago         209MB

➜  docker_test sudo docker run -it --rm test bash

[root@32dc92a782a2 code]# touch hello.go
[root@32dc92a782a2 code]# vi hello.go
[root@32dc92a782a2 code]# go build hello.go
[root@32dc92a782a2 code]# ls
bin  dev  etc  hello  hello.go	home  lib  lib64  lost+found  media  mnt  opt  proc  root  run	sbin  srv  sys	tmp  usr  var
[root@32dc92a782a2 code]# readelf -h ./hello

```

![2](/images/yuque/【go体系课】第一节课作业/2.png)

```
[root@32dc92a782a2 code]# go build -x hello.go
```

![3](/images/yuque/【go体系课】第一节课作业/3.png)

### 2、使用 readelf 工具，查看编译后的进程入口地址&在 dlv 调试工具中，使用断点功能找到代码位置

```
[root@1f558add4864 code]# readelf -h hello

[root@003a3639e337 code]# dlv debug
Type 'help' for list of commands.
(dlv) b *0x455780
Breakpoint 1 set at 0x455780 for runtime.vdsoParseSymbols() /usr/lib/golang/src/runtime/vdso_linux.go:247

```

![4](/images/yuque/【go体系课】第一节课作业/4.png)

### 3、使用断点调试功能，查看 Go 的 runtime 的下列函数执行流程

```
➜  go-test dlv debug
Type 'help' for list of commands.
(dlv) breakpoints
Breakpoint runtime-fatal-throw (enabled) at 0x43f700 for runtime.fatalthrow() /usr/local/go/src/runtime/panic.go:1163 (0)
Breakpoint unrecovered-panic (enabled) at 0x43f780 for runtime.fatalpanic() /usr/local/go/src/runtime/panic.go:1190 (0)
	print runtime.curg._panic.arg
(dlv) b main.main
Breakpoint 1 (enabled) set at 0x706018 for main.main() ./main.go:34
(dlv) b runtime.runqget
Breakpoint 2 (enabled) set at 0x44f653 for runtime.runqget() /usr/local/go/src/runtime/proc.go:5895
(dlv) b runtime.globrunqget
Breakpoint 3 (enabled) set at 0x44ec13 for runtime.globrunqget() /usr/local/go/src/runtime/proc.go:5615
(dlv) b runtime.globrunqput
Breakpoint 4 (enabled) set at 0x44eacf for runtime.globrunqput() /usr/local/go/src/runtime/proc.go:5584
(dlv) b runtime.globrunqget

```

![5](/images/yuque/【go体系课】第一节课作业/5.png)

![6](/images/yuque/【go体系课】第一节课作业/6.png)

![7](/images/yuque/【go体系课】第一节课作业/7.png)

### 4、使用 IDE 查看函数的调用方

![8](/images/yuque/【go体系课】第一节课作业/8.png)
![9](/images/yuque/【go体系课】第一节课作业/9.png)

### 感受

```
虽然按照作业要求操作了一遍
但是实际上不是很懂这个流程要怎么去读懂运用
希望能在接下来的课程里把这些调试用起来
```

​

### 参考链接

```
https://github.com/chai2010/advanced-go-programming-book/blob/master/ch3-asm/ch3-09-debug.md
```

​

​
