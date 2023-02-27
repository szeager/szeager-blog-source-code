---
title: JavaScript如何对几十上百G的大文件读写处理
urlname: aw74gg
date: '2020-01-06 19:53:59 -0800'
tags: []
categories: []
---

## 1、背景

对 MongoDB 导出的 Json 文本进行统计处理， 但导出的 Json 文本因为是不规则的 Json 形式，无法使用 Json.parse。但是又要对数据进行各种计算聚合，达到业务所需的结果。

## 2、错误想法 ❎

由于没有处理过大文件的经历，没想到导出来的 Json 文件竟然高达几十 G。
平时直接使用,fs.readFile， 读起文件来，直接崩溃。

```javascript
const fs = require('fs');
const Promise = require('bluebird');
const readFileAsync = Promise.promisify(fs.readFile);
let content = await readFileAsync(filePath, 'utf8’);
```

## 3、着手学习 Stream 模块【流】

> // 引入 Node 文档解释
> Node.js 中有四种基本流类型：
>
> - Writable：可以向其中写入数据的流（例如 fs.createWriteStream()）。
> - Readable：可以从中读取数据的流（例如 fs.createReadStream()）。
> - Duplex：同时为 Readable 和的流 Writable（例如 net.Socket）。
> - Transform：Duplex 可以在写入和读取数据时修改或转换数据的流（例如 zlib.createDeflate()）。
>
> 流可以是可读的，可写的，或两者兼有。所有流都是的实例 EventEmitter

所以，流是什么，就如同水。
写入流就是像倒水，一点一点慢慢的倒入杯中，
读取流就是像喝水，一口一口的喝进肚子里。

## 4、重写脚本 ✅

```javascript
const fs = require("fs");
const Promise = require("bluebird");

// 数据处理
function dataProcessing(row) {
  // 业务处理
  return row;
}

// 进度show
function show(userCount, startTime) {
  const jindu = Math.floor((userCount / 10000000) * 100 * 100) / 100;
  console.log(
    `总数量:10000000, 当前处理数量:${userCount}, 进度百分比: ${jindu}%`
  );
  if (userCount === 10000000) {
    const endTime = Date.now();
    console.log(`共用时：${(endTime - startTime) / 1000}秒。`);
  }
}

// 读写流文件处理
const streamFileFunc = (readFilePath, writeFilePath) =>
  new Promise((resolve, reject) => {
    console.log("开始读写流");
    let data = "";
    const readStreamFile = fs.createReadStream(readFilePath);
    const writeStreamFile = fs.createWriteStream(writeFilePath, {
      flags: "w",
      encoding: "utf8",
    });
    let i = 1;
    const startTime = Date.now();

    readStreamFile.on("data", (chunk) => {
      // 暂停读取, 做业务处理
      readStreamFile.pause();

      // 对不规则Json文本， 读一段，切割一段
      data += String(chunk);
      data = data.split("}},");
      // 剩下末尾不完整的，留到下一次拼接
      const lastData = data.pop();

      data.map((v) => {
        // 处理成能使用，JSON.parse的格式
        if (v[0] !== "{") v = `{${v}`;
        v += "}}}";

        // 业务逻辑处理
        const ret = dataProcessing(JSON.parse(v));

        // 流-写入数据
        writeStreamFile.write(String(JSON.stringify(ret)));

        // 计数，看进度
        i += 1;
        show(i, startTime);
        return v;
      });
      data = lastData; // 末尾拼接

      readStreamFile.resume(); // 恢复读取并触发data事件
    });

    readStreamFile.on("end", () => {
      console.log("流文件读取完成.....");
      writeStreamFile.end();
    });

    readStreamFile.on("error", (err) => {
      console.log(`read stream file err: ${err}`);
      reject(err);
    });
    writeStreamFile.on("error", (err) => {
      console.log(`write stream file err: ${err}`);
      reject(err);
    });
  });

// main
async function main(readFilePath, writeDataPath) {
  try {
    if (fs.existsSync(readFilePath)) {
      await streamFileFunc(readFilePath, writeDataPath);
    }
  } catch (err) {
    console.log("main catch err:", err);
  }
}

// 执行
main("./xxx.json", "./data.json");
```

## 5、参考教程：

[https://www.iteye.com/blog/justcoding-2307215](https://www.iteye.com/blog/justcoding-2307215)
[https://nodejs.org/dist/latest-v12.x/docs/api/stream.html#stream_class_stream_writable](https://nodejs.org/dist/latest-v12.x/docs/api/stream.html#stream_class_stream_writable)
