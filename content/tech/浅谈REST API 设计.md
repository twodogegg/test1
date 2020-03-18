---
title: "浅谈REST API 设计"
date: 2020-03-18T14:14:15+08:00
slug: "talk-rest-api-design"
tags:
  - rest-api
dropCap: false
description: "谈一谈自己的理解api设计，没有严格按照rest来。做了一些精简"
---

## 前言

对于 APi 的设计相信大家都不会感到陌生。只是各个公司的规范都不一样，或者干脆没有规范。一遍写的时候才一遍形成规范。极不利于团队合作和快速开发。

这篇文章会参照 [RESTful API](https://crifan.github.io/http_restful_api/website/) [^1]和 [lumen-api-demo](https://github.com/liyu001989/lumen-api-demo) 然后结合自己的实际情况编写

希望可以给大家做个参考，api 的划分我就按照四个类型划分吧。把业务中所有的情况尽可能的考虑进去。按请求方式划分

## APi 划分[^2]

### 1. GET 请求

```
例子： 用户，帖子，评论
get    /api/posts                   帖子列表
get    /api/posts?limit=10&page=1   帖子列表分页
get    /api/user/posts           当前用户的帖子列表 | 列表
get    /api/users/4/posts        id为4的用户的帖子列表
get    /api/posts/5/comments/8   id为5的帖子的id为8的评论详情
get    /api/posts/5/comments     帖子5的评论列表
get    /api/posts/5                 id为5的帖子详情
```

### 2. POST 请求

```
post   /api/posts                   创建帖子
post   /api/posts/5/comments     添加评论
```

### 3. PUT|PATCH 请求

put 更新全部信息， patch 更新部分信息，偷懒就全部用 put 得了

```
put    /api/posts/5                 替换帖子5的全部信息
patch  /api/posts/5                 修改部分帖子5的信息
put    /api/posts/5/comments/8   替换帖子评论内容
patch  /api/posts/5/comments/8   部分更新帖子评论
```

### 4. DELETE 请求

```
delete /api/posts/5                 删除帖子5
delete /api/posts/5/comments/8   删除某个评论
delete /api/posts [5,8] 批量删除,如下图
```

![图片](/images/WX20200318-151747@2x.png)

## 不好的 API 设计风格[^3]

详情看引用部分说的很清楚了，着重的说下，不要在接口里面出现动词！

还有禁用用户和启用用户不要用两个接口。 一个 `put|patch` /api/users/5 完事了！

## 数据返回格式[^4]

标准的 rest 规范是如果产生了错误是抛出异常的，返回异常信息，并且错误码放到 http 状态码上。
在一般的公司项目中为了方便用 `code`, `message`, `data` 定义

- code

  - 返回 http 状态码，也可以自定义

- code 省事参考

  - 正常 200

  - 提交的参数错误 422

  - 一般的异常 400

  - 服务器未知异常 500

  - 自定义异常，例如用户 token 过期什么的 自定义

- message
  - 异常 返回错误信息
  - 正常 ok
- data
  - 对象
    接口示例 get /api/posts/5, post/put 请求是否返回按情况而定
  - 对象的数组 返回一个 对象的数组 外面不嵌套一层 list 例如 data:[对象 1,对象 2 ]
    接口示例 get /api/posts
  - null
    接口示例 delete /api/posts/5

## 分页设计[^5]

分页的数据对象上面需要嵌套一个 `list` 标签

请求格式:

```
get /api/posts?limit=10&page=1
```

返回格式：

```
{
  "code": 200,
  "message": "ok",
  "data": {
    "curPageNum": 1,
    "hasNext": false,
    "hasPrev": false,
    "numPerPage": 10,
    "totalNum": 3,
    "totalPageNum": 1,
    "list": [
      {
        "id": "5c628227bfaa44aa7b2f56a5",
        "active": "Y",
        "audio": ""
      }
    ]
  }
}

```

[^1]: [HTTP 后台端：RESTful API 接口设计](https://crifan.github.io/http_restful_api/website/)
[^2]: [接口示例](https://github.com/liyu001989/lumen-api-demo)
[^3]: [不好的 API 设计风格](https://crifan.github.io/http_restful_api/website/restful_experience/bad_design.html)
[^4]: [RESTful API 接口返回数据的格式和风格](https://crifan.github.io/http_restful_api/website/restful_experience/resp_data_style.html)
[^5]: [分页设计](https://crifan.github.io/http_restful_api/website/restful_experience/pagination.html)
