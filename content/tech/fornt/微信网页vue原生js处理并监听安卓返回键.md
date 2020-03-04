---
title: "微信网页vue原生js处理并监听安卓返回键"
date: 2020-03-04T21:48:56+08:00
draft: true
tags:
  - vue
  - 微信网页开发
---

## 前言

今天遇到一个需求是这样的：自己开发的网页，在首页的需要打开一个二维码，打开二维码的时候如果安卓按了手机底部的返回键，希望关闭二维码。

## 解决思路：

进入应用时二维码的显示和是否返回就关闭存到 store 里面。

有二维码时关闭二维码

没有二维码时退出应用

若是进到其他页面则将 返回就关闭变量 改成 false

## 流程图

![](/images/WX20200304-222436@2x.png)

## 遇到的坑：

1. 由于 vue 是 单页面应用，我写了按键监听以后，若是在其他页面点击返回也会触发。然后一直触发到退出。

## 核心代码展示

`store`

```js
state: {
  showQrCode: false,
  backIsClose: true
},
```

`main.js`

```js
router.beforeEach((to, from, next) => {
  if (to.path !== "/") {
    page.$store.state.backIsClose = false;
  }
  next();
});

... 省略代码

const page = new Vue({
  router,
  store,
  render: (h) => h(App)
}).$mount('#app')

window.history.pushState('', '', window.location.href)
window.addEventListener('popstate', () => {
  /**
   * 如果返回不是在首页返回的，则使用路由返回，并且 backIsClose 标记为ture
   * 下次在首页返回的时候就可以关闭公众号页面了
   * 每次新进页面的时候都将  backIsClose 改成 false
   */
  if (page.$route.path !== '/') {
    page.$store.state.backIsClose = false
    page.$router.back()
  } else {
    if (page.$store.state.showQrCode) {
      page.$store.state.showQrCode = false
    } else {
      if (!page.$store.state.backIsClose) {
        page.$store.state.backIsClose = true
        return false
      }

      // 微信js sdk 关闭网页
      // weixin-js-sdk
      page.$wx.closeWindow()
    }
  }
})

```
