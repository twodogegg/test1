+++
title= "Es6 必学常用的新特性"
date=2020-02-14T15:39:00+08:00
draft=true
tags = ["es6"]
+++

前言，es6 出来也有几年了以前也学过一些，可是学的又不够系统。想看着教程学，教程又太庞大了。所以就按照 阮一峰 的教程，从上到下的写一遍。只记录自己以前常用的和经常看到的用法

## 1. let 和 const

`let` 和 `const` 和es5 的变量声明 `var` 有所不同，是个块级作用域

let
声明一个块级作用域的变量

const
声明一个块级作用域的常量，**约定用大写声明**

```
let a = 1;
CONST MAX = 5
```

## 2. 变量的解构赋值

个人几个常用的场景

### (1) 批量定义变量

```js
let [a, b, c] = [1, 2, 3];
```

### (2) 从函数返回多个值

```js
// 返回一个数组

function example() {
  return [1, 2, 3];
}
let [a, b, c] = example();

// 返回一个对象

function example() {
  return {
    foo: 1,
    bar: 2
  };
}
let { foo, bar } = example();
```

### (3) 提取 JSON 数据

```js
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);
```

### (4) 函数参数的默认值

```js
jQuery.ajax = function (url, {
  async = true,
  beforeSend = function () {},
  cache = true,
  complete = function () {},
  crossDomain = false,
  global = true,
  // ... more config
} = {}) {
  // ... do stuff
};
```

指定参数的默认值，就避免了在函数体内部再写 `var foo = config.foo || 'default foo';` 这样的语句。


### (5) 遍历 Map 结构

```
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```

### (6) 载入模块指定的方法

```
const { SourceMapConsumer, SourceNode } = require("source-map");
```

