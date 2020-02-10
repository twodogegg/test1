+++
title = "记录自己Hugo-Meme博客的搭建"
date = 2020-02-10T20:29:05+08:00
slug = "hugo-meme-blog"
+++

算起来这已经算是我的第三个博客了，不知道是不是我最后一个，反正这是我目前用的最好看的博客了吧，换博客是因为觉得自己原来写的东西，学的东西都好幼稚，想重新开始了，以前写的东西，是面对自己的，现在想面向大众

## 前言

这款主题来自[io-oi.me]([reuixiy](https://io-oi.me/)) 第一眼看到的时候就被经验了，居然有这么简洁而又精美的主题。特别是这博客的分类方式，简直打破了我原本的想象，原来的我，其实经常会为了分类而纠结。分的太细，分类好像摆设，按照编程语言来分，又会显得过多。现在我参考他的，分类主要分成量部分，我分成了生活和编程相关的，更细节的区分用标签。



## 博客主题介绍

1. 使用 [hugo](https://gohugo.io) 生成

2. 主题 [meme](https://themes.gohugo.io/hugo-theme-meme/)

3. netlify 自动化部署

## 安装 Hugo

    mac 示例

1. 安装 hugo

```bash
brew install hugo
```

2. 新建一个站点

```bash
hugo new site quickstart
```

3. 添加主题

```bash
cd quickstart
git init
git submodule add https://github.com/reuixiy/hugo-theme-meme.git themes/meme
```

## 运行博客
   
1. 将 `config.toml` 替换成 [config.toml](https://github.com/reuixiy/hugo-theme-meme/blob/master/config-examples/en-us/config.toml)

2. 新建一篇文章和一个关于页面
```bash
hugo new "posts/hello-world.md"
hugo new "about/_index.md"
```
3. 运行
```bash
hugo server -D
```

## 部署博客



 