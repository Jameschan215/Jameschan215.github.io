---
title: "可选链"
layout: post
date: 2019-01-20 12:41
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

**★ 只有可选链的任意一个环节不为`nil`时，才能对其进行读取和存入，否则都会导致存取失败，即便没有runtime error。**

## 链的多层连接
* 如果你访问的值不是可选项，它会因为可选链而变成可选项；  
  *如果你尝试通过可选链取回一个 Int 值，就一定会返回 Int? ，不论通过了多少层的可选链；*
* 如果你访问的值已经是可选的，它不会因为可选链而变得更加可选。

