---
title: Rin 是一个基于 Cloudflare Pages + Workers + D1 + R2 的博客，只需要一个解析到CF的域名即可部署
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-09-13 16:24:20
updated:
tags:
- Rin
- D1 + R2
- 博客
categories:
- Cloudflare
keywords:
description:
top: 16
top_img:
comments:
cover: https://serv.200038.xyz/2024/09/19/817686.webp
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

- Rin 是一个基于 Cloudflare Pages + Workers + D1 + R2 全家桶的博客，无需服务器无需备案，只需要一个解析到 Cloudflare 的域名即可部署唯一的，缺点便是减速CDN特有的国内很慢了，不过对于博客来说也是能够勉强接受的

---

{% note blue 'anzhiyufont anzhiyu-icon-bullhorn' simple %}
Rin部署教程视频 ,来自[科技自习室](https://www.youtube.com/watch?v=Zij4EcehANk/),记录方便以后学习。
{% endnote %}
---
<div class="video-container">
<iframe width="560" height="315" src="https://www.youtube.com/embed/Zij4EcehANk?si=H_PIgAFHyTVUOqRe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

<style>
.video-container {
    position: relative;
    width: 100%;
    padding-top: 56.25%; /* 16:9 aspect ratio (height/width = 9/16 * 100%) */
}

.video-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}
</style>

### 介绍
Rin 是一个基于 Cloudflare Pages + Workers + D1 + R2 全家桶的博客，无需服务器无需备案，只需要一个解析到 Cloudflare 的域名即可部署

唯一的缺点便是减速CDN特有的国内很慢了，不过对于博客来说也是能够勉强接受的


### 特性
1. 支持 Github OAuth 登录，默认第一个登录的用户拥有管理权限，其他用户均为普通用户
2. 支持文章的写作与编辑
3. 支持本地实时保存对任意文章的修改/编辑且多篇文章互不干扰
4. 支持设置为仅自己可见，可以充当云端同步的草稿箱或者记录隐私性较强的内容
5. 支持拖拽/粘贴上传图片到支持 S3 协议的存储桶并生成链接
6. 支持设置文章别名，可通过形如 https://blog.xiaobai.cloudns.be/ 链接访问文章
7. 支持文章不列出在首页列表中
8. 支持添加友链，同时后端每间隔 20 分钟定期检查更新友链可访问状态
9. 支持回复评论文章/删除评论
10. 支持通过 Webhook 发送评论通知
11. 支持自动识别文章中的第一张图片并作为头图展示在文章列表中
12. 支持输入形如"#博客 #部署 #Cloudflare"之类的标签文本并自动解析为标签
13. 支持日夜间模式

### 部署
由于部署过程过于复杂建议参考[Rin官方部署教程](https://github.com/openRin/Rin/blob/main/docs/DEPLOY.md)和[Rin 博客简易部署教程](https://blog.obdo.cc/feed/10)。在此对两位作者表达感谢。