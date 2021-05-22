---
title: Node.js 与PHP urlencode的差异
urlname: iay0qq
date: '2019-11-18 00:14:46 -0800'
tags: []
categories: []
---

# 1、背景:

当前业务需要对接第三方接口，为了确保数据的准确性，添加了签名规则。
第三方那边说，中文要做 urlencode 处理。
php 语言的话，就是参数数组做 http_build_query( ) 处理，然后拼接 计算 md5。

我方才用的是 Node.js encodeURIComponent 进行去编码，发现签名始终通不过，
经过对比，是 urlencode 之后产生的结果有一丝丝的差异
比如空格的 urlencode:
php http_build_query( )=>  +
NodeencodeURIComponent=>  %20

# 2、解决办法

```javascript
this.urlencode = (str) => {
  str = `${str}`.toString();

  return encodeURIComponent(str)
    .replace(/!/g, "%21")
    .replace(/'/g, "%27")
    .replace(/\(/g, "%28")
    .replace(/\)/g, "%29")
    .replace(/\*/g, "%2A")
    .replace(/%20/g, "+");
};
```
