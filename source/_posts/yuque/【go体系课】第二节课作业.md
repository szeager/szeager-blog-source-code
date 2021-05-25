---
title: 【go体系课】第二节课作业
urlname: xtodfv
date: '2021-05-20 06:47:07 -0700'
tags: []
categories: []
---

### 必做：channel ⼀⻚中，找出所有红线报错在 runtime 中的位置

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621518463215-e873ae27-d459-4c23-aa4d-3c399b5fc53a.png#clientId=u13b444ac-8341-4&from=paste&height=823&id=u6256e48c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=823&originWidth=956&originalType=binary&size=489115&status=done&style=none&taskId=u2e674811-8ce6-4c6b-9a73-ac27f9a56d9&width=956)

#### close of nil channel

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621518433448-7cd537fa-4382-4204-bb2a-02940c25b3f9.png#clientId=u13b444ac-8341-4&from=paste&height=811&id=u6dc52f7f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=811&originWidth=1414&originalType=binary&size=131217&status=done&style=none&taskId=u7ca4b17b-a63d-4091-9a3e-87b876d66db&width=1414)

#### send on closed channel

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621518862467-eb85bdc8-62f0-4644-b580-28a9881daf25.png#clientId=u13b444ac-8341-4&from=paste&height=796&id=uc5259d9b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=796&originWidth=1446&originalType=binary&size=112510&status=done&style=none&taskId=u54295f0f-21e9-4ab9-a649-63d15284827&width=1446)

#### close of closed channel

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621518991346-51585564-1e0f-4dfa-9cc5-c1b3902145c0.png#clientId=u13b444ac-8341-4&from=paste&height=797&id=uf22ab00b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=797&originWidth=1406&originalType=binary&size=108608&status=done&style=none&taskId=ua51b090e-818f-4abc-b642-6f0ba5fbdd1&width=1406)

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

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621519060979-0fcf7135-dcc2-478a-ba40-ab2726942233.png#clientId=u13b444ac-8341-4&from=paste&height=791&id=u233b7a57&margin=%5Bobject%20Object%5D&name=image.png&originHeight=791&originWidth=1397&originalType=binary&size=157284&status=done&style=none&taskId=u0ecec50c-40dc-4cc2-b7f5-8855e3cdcbd&width=1397)
![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621519088635-4da10425-becf-4fd8-8254-5ba8bee9f131.png#clientId=u13b444ac-8341-4&from=paste&height=788&id=u5eccbf5d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=788&originWidth=1400&originalType=binary&size=148277&status=done&style=none&taskId=uaf45b04e-7d0f-4731-9113-61c8eddcca2&width=1400)

### 选做 1：修复[https://golearn.coding.net/p/gonggongbanji/files/all/DF12](https://golearn.coding.net/p/gonggongbanji/files/all/DF12)中的 test case

![image.png](https://cdn.nlark.com/yuque/0/2021/png/290620/1621520762795-77a89664-389e-4d71-8896-92c244f66762.png#clientId=u13b444ac-8341-4&from=paste&height=815&id=ub5ad5eb3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=815&originWidth=1407&originalType=binary&size=118999&status=done&style=none&taskId=uaa5e29ad-7987-4c9a-873d-7d4c10f1581&width=1407)

### 选做 2：扩展其功能，增加更多的操作符号⽀持(随意发挥)
