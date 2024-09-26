---
title: Serv00上搭建一个若梦图床 + 接入Cloudflare R2 
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-09-10 12:00:57
updated:
tags:
- Serv00
- 图床
- 好看的
categories:
- 学习中
keywords:
description:
top: 66
top_img:
comments:
cover: https://serv.200038.xyz/2024/09/19/052317.webp
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
  - 本文介绍如何在Serv00上搭建一个图床，接入到 Cloudflare R2, 自己有VPS的也可在宝塔上面部署，可用于博客，存储照片。
    
---

###  Serv00上搭建一个图床,内存太小,我们可以接入到CFR2 足够个人使用。自己有VPS的也可在宝塔上面部署
---
### 面板页
![png](https://assets.vviptuangou.com/a7851a9a4cb48ce3008bdf5b6835f6f2b2446aba.jpg)

### 后台页
![png](https://assets.vviptuangou.com/81b3a97608fce33725b887f5888863903a6b70de.jpg)

**友情提示 使用Serv00搭建的好像不支持PNG格式上传 上传后会显示空白不显示图片**

### 安装前准备

[Serv00账号注册](https://www.serv00.com/) 

{% link Github,项目地址,https://github.com/JLinMr/PixPro/ %}

## 安装步骤

1. 注册好Serv00账号打开网页进入到面板端添加域名或者用自己的域名都行，这里我用别的网站注册的二级域名。如下图添加
![img](https://assets.vviptuangou.com/65b5e8853269dc1517f0c29312f405ec4ff93aac.jpg)

2. 把里面的A记录解析你托管到CF的域名或者别的地方申请的
![img](https://assets.vviptuangou.com/89fad1033d1bc063cc48549c59ccc86f90fc45b7.jpg)
![png](https://assets.vviptuangou.com/42cb9cc5ef879bd3ff44afae6058f2b589f3ad04.jpg)

3. 按照下图打开域名的权限
![png](https://assets.vviptuangou.com/65f930477953843e868fa55a5b9303716e659ed3.jpg)
![png](https://assets.vviptuangou.com/6bead65cbca8e9bf5284e0bd0809cbccd524fbd6.jpg)
点击Save等待成功

4. 创建MySQL数据库（保存账号及地址）
![png](https://assets.vviptuangou.com/495fafb3a994859395fceac7d6af587ecae551a9.jpg)
![png](https://assets.vviptuangou.com/6e54144c39f77ee9fdfa22683ebcd946f136993e.jpg)

5. {% btns rounded grid5 %}
{% cell 下载ZIP文件, https://github.com/JLinMr/PixPro/releases/tag/v1.7.6, anzhiyufont anzhiyu-icon-github %}
{% endbtns %}

6. 上传安装包并解压进入文件管理器
![image](https://i.111666.best/image/lwU3tB1yOBMU3BGgCgbYEP.png)

7. 进入public_html文件夹删除其下所有文件
![image](https://i.111666.best/image/rW0Dia44iDyGLjkFJf65zT.png)

8. 上传安装包到你添加的域名或者Serv00自带域名下
![undefined](https://assets.vviptuangou.com/b7301c6bb01e09fa8212834c3e6af4b68ac3bab7.jpg)
![undefined](https://assets.vviptuangou.com/0a35e541298e16d5b424e37711df220196fcb608.jpg)

9. 选择你们下载文件的路径上传好如下图
![undefined](https://assets.vviptuangou.com/475b0cc5380aa5c6a098a587c96d960f2bea8bb6.jpg)
![undefined](https://assets.vviptuangou.com/7bbf3b21347003fd80c632298441fad9fdecb043.jpg)
![undefined](https://assets.vviptuangou.com/d8ab33579a8b00b259be673f18c53cfcd373bb71.jpg)

### 和上一步一样

10. 进去后如下图所以我们`Shift`建一直按着然后点击鼠标左键全选
![undefined](https://assets.vviptuangou.com/fffb74f2162d5d0bc0c382ceea298fb9c0fcc8eb.jpg)

11. 移动到我们开始创建域名目录下的`public_html`
![png](https://assets.vviptuangou.com/048b5580f71361a883e023b5016b137ac4ab5bdd.jpg)

12. 修改PHP版本 在域名目录下创建一个文本，名为：`.htaccess`  
![png](https://assets.vviptuangou.com/fa3c6470d9afea1785903b6c93046186052fb2e8.jpg)
![png](https://assets.vviptuangou.com/167e762e94fa1e2ddd4bd29064e573a59934a377.jpg)

13. 添加PHP版本
![E.png](https://assets.vviptuangou.com/b6f389d7bbf07970ae10d26445b1ec5017906da9.jpg)

**选择`Text Editor` 添加以下代码**

```
AddType application/x-httpd-php81 .php
```
![png](https://assets.vviptuangou.com/8846fa57b96c746e82c98c3cff83192c333978e0.jpg)

14. 访问你的域名开始安装系统，管理员账户和密码自己设置 ，如果要接入`CFR2`我们存储选择 `S3` 下面我会写`S3`安装方式
![png](https://assets.vviptuangou.com/88ae10370b1c2c2a1e9c2980228371982944f72b.jpg)
![png](https://assets.vviptuangou.com/a3bf9c47a9b8cd6590165729e0c3c79f1169ac9b.jpg)
![png](https://assets.vviptuangou.com/41eba336ae11799d9f93b9e2ea430626be4a8705.jpg)

15. 点击回到首页就可以上传图片了
![png](https://assets.vviptuangou.com/1b0c08bb32bc384db6982aac4ed6f58ac464fd92.jpg)

---
### 接入R2 前提 已开通 Cloudflare R2

### 进入到 Cloudflare 面板 找到 R2 右边有一个管理 R2API 令牌点击创建 API令牌 ，创建好后里面有我们需要的访问密钥和机密访问密钥

![3K](https://assets.vviptuangou.com/127c616330870251adb6897b04d0ca0e8ba830b0.jpg)

### 1. 进入到 Cloudflare 面板 找到 R2 点击创建存储桶

![1](https://assets.vviptuangou.com/eee36ef2f9e5086de6d3dbb93e8b28ff4fe26577.jpg)

   
### 2. 进入后名称随便写。位置选择亚太地区后点击创建存储桶

![2](https://assets.vviptuangou.com/2de4727294de8dde45ea7c6b773cbc1628d70abe.jpg)

### 3. 创建好后点击设置拉到下面看到 R2.dev 子域点击后面的允许访问 ， 连接域需要添加你托管到CF上面域名

![3](https://assets.vviptuangou.com/99e549d954615e6279ee8295e75d63e920075cf8.jpg)

### 4. 14 步我们安装选择`S3`后看到下图 

![4](https://assets.vviptuangou.com/89d9aa12a4d7de30f6ce84acd5d395b920d3e4e0.jpg)

| 参数 | 值 |
| --- | --- |
| S3 Region | auto |
| S3 Bucket | 你的存储桶名称 |
| S3 Endpoint | 你的S3API 后面不要加你的存储桶名称 |
| S3 Access Key ID | R2API令牌访问密钥 |
| S3 Access Key Secret | R2API令牌机密访问密钥 |
| S3 自定义域名 | R2.dev 添加的自定义域 或 R2 分配的域名 |

### 5. 点击完成安装即可。这是我们上传好的图片 我下面的域名就是我们 R2 分配的域名 

![5](https://assets.vviptuangou.com/debdfa2a267ad44bde508936288285b528bd781b.jpg)

### 6. 我们回到 Cloudflare R2 就会看到刚刚上传的图片

![6](https://assets.vviptuangou.com/8f23c10386b3907fc6a5e03a026af498e6fd9767.jpg)


### 在给大家推荐一个的在线生成封面网站，专为博客、短视频、社交媒体等生成个性化封面

{% link GitHub,项目地址,https://github.com/JLinMr/Mini-Cover,https://github.githubassets.com/assets/pinned-octocat-093da3e6fa40.svg %}

{% link 封面部署教程参考友链,周润发,https://blog.001315.xyz/p/58 %}

### 这个封面可以和图床结合。 封面做好后我们不用去上传到图床直接点击封面网站的外链即可,前提已部署`PixPro` 图床

### 感谢作者梦爱吃鱼下面是他的博客，欢迎大家去预览、哈哈哈

{% sitegroup %}
{% site 梦爱吃鱼, url=https://blog.bsgun.cn/, screenshot=https://fastly.jsdelivr.net/gh/niceao/img/2024/09/19/711811.webp, avatar=https://oss-cdn.bsgun.cn/logo/avatar.256.png, description=但愿日子清静抬头遇见的满是柔情 %}
{% endsitegroup %}

