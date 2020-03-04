---
title: "使用es6 Promise 和 Async 优化 SetTime"
date: 2020-02-23T20:57:04+08:00
draft: true
---

在es6以前若需要一段程序需要延迟执行，一般是这样写的 

```js
setTimeout(function () {
    // xxx
}, 1000)
```

感谢 es6 的推出可以使用更优雅的写法

我是这样实现的，在一个 util 文件中定义以下函数

```js
export function sleep (time) {
  return setTimeout(() => {
    return new Promise(resolve => {
      return resolve
    })
  }, time)
}
```

调用

```
await sleep(1000)
// xxx
```