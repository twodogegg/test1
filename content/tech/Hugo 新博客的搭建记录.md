+++
title = "记录自己Hugo-Meme博客的搭建"
date = 2020-02-10T20:29:05+08:00
description = "记录自己的第一篇博客，使用Hugo + Meme ，美炸了！"
slug = "hugo-meme-blog"
tags = ["hexo"]
+++

算起来这已经算是我的第三个博客了，不知道是不是我最后一个，反正这是我目前用的最好看的博客了吧，换博客是因为觉得自己原来写的东西，学的东西都好幼稚，想重新开始了，以前写的东西，是面对自己的，现在想面向大众

## 前言

这款主题来自[io-oi.me]([reuixiy](https://io-oi.me/)) 第一眼看到的时候就被经验了，居然有这么简洁而又精美的主题。特别是这博客的分类方式，简直打破了我原本的想象，原来的我，其实经常会为了分类而纠结。分的太细，分类好像摆设，按照编程语言来分，又会显得过多。现在我参考他的，分类主要分成量部分，我分成了生活和编程相关的，更细节的区分用标签。

## 博客主题介绍

1. 使用 [hugo](https://gohugo.io) 生成

2. 主题 [meme](https://themes.gohugo.io/hugo-theme-meme/)

3. `netlify` 自动化部署

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

博客采用的是自动化部署方式部署在 [netlify](https://app.netlify.com/)，可以参考这个项目 [reuixiy/io-oi.me](https://github.com/reuixiy/io-oi.me)

1. 参考上诉项目对项目进行修改

2. `netlify.toml` 改成如下

```bash
[build]
  publish = "public"
  command = "npm run build"

[build.environment]
  HUGO_VERSION = "0.64.0"
  HUGO_ENV = "production"
  HUGO_ENABLEGITINFO = "true"
```

3. `config.toml` 启用版本管理

```bash
# 是否启用 Git 版本信息
enableGitInfo = true
```

4. push 到自己 `github` 的仓库

5. 在 `Netlify` 登录并绑定git 的这个仓库

6. 构建完成以后会出现一个 默认的域名

## Netlify 配置自定义域名

1. 点击下方按钮添加自定义域名，域名状态应该为未解析状态
   ![hugo-meme-blog-1.png](/images/hugo-meme-blog-1.png)

2. 域名解析

添加完域名后会出现一个 `Check DNS configuration` 点击它

域名解析该域名

例：

`heuristic-lichterman-5f458f.netlify.com`

![hugo-meme-blog-2.png](/images/hugo-meme-blog-2.png)

## 参考资料

1. [Hugo 主题 MemE 文档](https://io-oi.me/tech/documentation-of-hugo-theme-meme/)
2. [将 Hexo 静态博客部署到 Netlify](https://io-oi.me/tech/deploy-static-site-to-netlify/)