---
title: Cloudflare + pages +R2 部署一个图床
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-09-14 02:11:15
updated:
tags:
- R2
- 图床
- pages
categories:
- Cloudflare
keywords:
description:
top: 
top_img:
comments:
cover: https://serv.200038.xyz/2024/09/19/064237.webp
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
ai:

- 这篇文章介绍如何使用 Cloudflare + pages +R2 实现的免费图床。
---

### 部署前提已注册CloudFlare并开通R2服务

{% link 项目地址,GitHub,https://github.com/roimdev/roim-picx %}

### 预览地址

[roim-picx](https://roim.page/)

### 介绍

**一款基于Cloudflare的Worker、R2、Pages实现的图床应用，具有以下特点**：
- 10GB的免费存储空间
- 每月300W次的不计流量的图片访问，每天10W的限制。
- 每月100W次的图片上传次数
- 不需要自己购买服务器，克隆代码后部署CloudFlare即可使用。
- 独立部署不需要担心被第三方删除数据。

### 已实现功能
- 图片批量上传
- 图片列表查询
- 图片删除
- 目录创建
- 按目录查询
- 链接地址点击复制
- 简单的身份认证功能，进入管理页面需要授权

### TODO
* 上传时支持选择目录。
* 提供删除图片的访问链接
* 管理页面支持分页加载图片

* 部署教程我也不会因为项目的图片挂了

{% link 部署教程看不懂,你们试试吧,https://lhyan.cn/pages/11f476/ %}

{% link Github,推荐图床,https://github.com/MarSeventh/CloudFlare-ImgBed?tab=readme-ov-file,anzhiyu-icon-github %}