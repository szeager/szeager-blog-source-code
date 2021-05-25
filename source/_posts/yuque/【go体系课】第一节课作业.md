---
title: 【go体系课】第一节课作业
urlname: somslw
date: '2021-05-17 06:59:13 -0700'
tags: []
categories: []
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

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621260201162-a98a6dff-69ea-4e6b-8ddf-2763190286a6.png#clientId=u720ca13e-8081-4&from=paste&height=771&id=uf43edb0a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=771&originWidth=1212&originalType=binary&size=179148&status=done&style=none&taskId=ud67e34c3-6b6a-4e7f-8b6f-2803dbcb5c0&width=1212)

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

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621260341230-f0b4fd44-2146-4266-a96e-fc54e6bdb296.png#clientId=u720ca13e-8081-4&from=paste&height=506&id=u70356252&margin=%5Bobject%20Object%5D&name=image.png&originHeight=506&originWidth=1139&originalType=binary&size=103341&status=done&style=none&taskId=u9a72da07-3190-4a72-ba36-2fc8e5f134b&width=1139)

```
[root@32dc92a782a2 code]# go build -x hello.go
```

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621260966852-50f9b11a-bde7-412a-b5da-f4823b7718a3.png#clientId=u720ca13e-8081-4&from=paste&height=975&id=u28e778d1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=975&originWidth=1907&originalType=binary&size=297914&status=done&style=none&taskId=u19681f61-15b1-482c-b828-d602dfd2670&width=1907)

### 2、使用 readelf 工具，查看编译后的进程入口地址&在 dlv 调试工具中，使用断点功能找到代码位置

```
[root@1f558add4864 code]# readelf -h hello

[root@003a3639e337 code]# dlv debug
Type 'help' for list of commands.
(dlv) b *0x455780
Breakpoint 1 set at 0x455780 for runtime.vdsoParseSymbols() /usr/lib/golang/src/runtime/vdso_linux.go:247

```

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621263202382-505f0a5c-2114-4843-9796-c28fe794f5dd.png#clientId=u157e1589-c31a-4&from=paste&height=469&id=u2bed5392&margin=%5Bobject%20Object%5D&name=image.png&originHeight=469&originWidth=998&originalType=binary&size=90816&status=done&style=none&taskId=u16702050-9eb5-4dce-b870-cfd815e6d55&width=998)

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

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621348666602-bead13da-00bc-4ef6-a914-103e36049299.png#clientId=u40059bce-f853-4&from=paste&height=291&id=u67ac32f0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=291&originWidth=1104&originalType=binary&size=77636&status=done&style=none&taskId=u9966194b-7f48-4dd6-b24e-85a9e0b8a1b&width=1104)

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621348749726-eaf96c05-3f75-4098-ad16-440dff6f6d93.png#clientId=u40059bce-f853-4&from=paste&height=792&id=u0458a8f9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=792&originWidth=982&originalType=binary&size=152440&status=done&style=none&taskId=u520ef340-2217-4f65-91d2-138ce2c96b7&width=982)
![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621348781026-c0ffa09e-4ba6-4462-9e18-5b16760d70ba.png#clientId=u40059bce-f853-4&from=paste&height=589&id=uf9a62ad4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=589&originWidth=848&originalType=binary&size=124490&status=done&style=none&taskId=u1d790573-abf3-4e12-95ee-54ea2a721df&width=848)

### 4、使用 IDE 查看函数的调用方

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621349578038-827ca94f-c886-486f-9fdf-f03a8390feea.png#clientId=u40059bce-f853-4&from=paste&height=775&id=u58d0a64e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=775&originWidth=1412&originalType=binary&size=180910&status=done&style=none&taskId=u4232c30d-11d0-4a63-862d-eb778849bd1&width=1412)
![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621349641160-7382931e-a9fd-45e1-a52f-0c290db5962b.png#clientId=u40059bce-f853-4&from=paste&height=740&id=u1e28dc5d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=740&originWidth=1413&originalType=binary&size=162383&status=done&style=none&taskId=u4f5929d4-0e13-40c6-9166-ab11685d0c9&width=1413)

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
