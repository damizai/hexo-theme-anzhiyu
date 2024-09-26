---
title: Serv00搭建影视站
cover: https://serv.200038.xyz/2024/09/19/932079.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-07-18 22:10:01
updated:
tags:
- Serv00
- 影视站搭建
categories:
- 学习中
keywords:
description:
top: 6
top_img:
comments:
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

  Serv00搭建影视站
---

## 欢迎大家来到我的博客,我是一个小白,正在学习中,希望大佬多多指教,这是我的[GitHub](https://github.com/damizai).偶然看到一个名叫杨幂的脚,俗称CM大佬喂饭大大,特别喜欢他的喂饭视频.希望大家多多支持。这是他的个人[GitHub](https://github.com/cmliu).还有博客[BLOG](https://blog.090227.xyz/)

---

{% link 视频转自,Tweek,https://www.youtube.com/watch?v=DBEoJL433pI&t=664s %}

<div class="video-container">
[<iframe width="560" height="315" src="https://www.youtube.com/embed/DBEoJL433pI?si=NFFIv7fY4i6xVXFE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>]
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

## Serv00搭建影视站

- **演示网站**      https://caoni.rr.nu/
-  打不开的开下代理试试
---
## 采集站地址       推荐黑木耳采集站

- **黑木耳采集站**  https://www.heimuer.tv/
- **华为8采集站**   https://huawei8.live
- **非凡采集站**    http://ffzy5.tv/
- **暴风采集站**    https://publish.bfzy.tv
- **索尼采集站**    https://suonizy.net
- **快看采集站**    https://kuaikanzy.net
- **量子采集站**    http://lzizy.net
- **360采集站**     https://360zy.com/360zy/

### 部署应用前的一些工作

- **下载苹果CMS源码**
  - [网址链接](https://www.maccms.la/down/maccms10.zip)

- **下载主题**
  - [网址链接](https://github.com/dockkkk/mxone/releases/download/mxone/mxone.zip)

## 安装和配置步骤

### 1. 添加域名和设置DNS 
-  登入Serv00面板添加自己的域名点击 `WWW websites` 然后点击`Add new websites`
-  注意添加自己的域名并关闭DNS。如果使用 Serv00 域名，需开启全局。
![undefined](https://openai-75050.gzc.vod.tencent-cloud.com/openaiassets_49222133649779c6087f4e6525a0bdb6_2579861726116348800.png)

###  2. 创建一个MySQL
-  进入控制面板，创建一个新的 `MySQL` 数据库。
![15b3ebc1bfc8de3d480a7.png](https://telegra.ph/file/15b3ebc1bfc8de3d480a7.png)

###  3. 进入WWW网站权限
-   进入 `WWW websites`，设置相应的权限。
![8d14277edf9ffb0470cc9.png](https://telegra.ph/file/8d14277edf9ffb0470cc9.png)

###  4. 开始上传前面下载的CMS并解压
-  使用 `File manager` 进入文件管理，删除指定文件夹中的所有文件。
-  上传下载的 CMS 压缩包并解压。
![83b9516d007b5e496e118.png](https://telegra.ph/file/83b9516d007b5e496e118.png)

###  5. 解压到**domains**–你的域名–**public html**文件下。然后删掉zip压缩包
-  然后鼠标右击文件，点击`Explore`，然后右击出现的文件，点击Extract开始解压到`domains`–你的域名–`public html`文件下。然后删掉zip压缩包   
![a20dbae6c2fa4278917ec.png](https://telegra.ph/file/a20dbae6c2fa4278917ec.png)

###  6. 上传并解压主题压缩包
- 进入 `maccms` 文件夹，上传并解压主题压缩包到 `template` 目录下。
- 将主题文件夹改名为 `mxone` 并删除压缩包。
![8ecccf8cbc26db7f32af3.png](https://telegra.ph/file/8ecccf8cbc26db7f32af3.png)

###  7. 然后进入template文件夹下
-  上传`mxone`压缩包，解压到`template`目录下，将主题文件改名为`mxone`，并删除zip文件
![1a7afbb6ee3fb7a772ca1.png](https://telegra.ph/file/1a7afbb6ee3fb7a772ca1.png)

###  8. 移动maccms文件
- 将`maccms`的所有文件到`public html`文件下，并删除maccms10-2024.1000.4010空文件
![890c82d8b7a5be55a6088.png](https://telegra.ph/file/890c82d8b7a5be55a6088.png)
![8fbeef0c5b911a1707b7b.png](https://telegra.ph/file/8fbeef0c5b911a1707b7b.png)

###  9. 在public html文件下找到admin.php文件
-  找到后将其改名，我以`admin123.php`为例**（可自行修改，这是后台的后缀）**
![9f5a9753ee73b8938369f.png](https://telegra.ph/file/9f5a9753ee73b8938369f.png)

###  10. 更改PHP版本为74**（这部及其重要，不然后面主题无法获取）**
-  进入domains–域名文件下，添加一个文档：- `.htaccess`
-  点击:heavy_plus_sign:–New empty file，
![47745843fc9fe56c8e68a.png](https://telegra.ph/file/47745843fc9fe56c8e68a.png)
-  右击文档 `.htaccess`，依次点击：**View/Edit --Choose other–Text Editor**
-  然后将代码放入文件中，点击左上角save保存

``` SHELL
AddType application/x-httpd-php74 .php
```
![fc48b8c453233a046a51e.png](https://telegra.ph/file/fc48b8c453233a046a51e.png)

###  11. 访问你的域名安装后台 看到此图片代表已经成功 然后点击同意并安装 
![890c9855f9e44011fc138.png](https://telegra.ph/file/890c9855f9e44011fc138.png)

###  12. PHP版本一定要对 -  PHP版本7.4
![4e1851ce1f0a45d5c3019.png](https://telegra.ph/file/4e1851ce1f0a45d5c3019.png)

###  13. 管理员账号密码，点击安装
-  数据库名称账号和密码就是前面`MySQL`申请的。对应填入即可，然后点击测试数据库连接。出现数据库连接成功**就没问题了。
![15bc54a1432c5213c8bf3.png](https://telegra.ph/file/15bc54a1432c5213c8bf3.png)

###  14. 先进入前台：打开一个新网页，输入你的域名  比如 https://jinx.200038.xyz
-  打开一个新网页，进入系统管理后台，你的域名/admin123.php**（后缀前面如果不一样进行对应调整）**
![308c0dbdbbcce70fe819e.png](https://telegra.ph/file/308c0dbdbbcce70fe819e.png)

###  15. 输入后台账号和密码 然后点击升级
![749ad2eac39e90daee446.png](https://telegra.ph/file/749ad2eac39e90daee446.png)

###  16.  配置主题
-  点击自定义菜单配置，复制下面的主题文字：（admin123.php前面改了对应调整），然后并保存

 ``` SHELL
mxoneX主题,/admin123.php/admin/mxone/mxoneset
``` 
![2178f06cf5e869cc94349.png](https://telegra.ph/file/2178f06cf5e869cc94349.png)        

###  17. 然后点击系统，网站参数配置 把网站模板和手机模板改为`mxone`，并保存
![05d9ea64de5af09e80e4c.png](https://telegra.ph/file/05d9ea64de5af09e80e4c.png)

###  18. 然后新开一个网页打开你的域名 比如 https://jinx.200038.xyz  变下图就可以了。
![731974881784ec37771f3.png](https://telegra.ph/file/731974881784ec37771f3.png)

###  19. 最后，刷新你的后台 - 点击`mxoneX`主题并保存。（后面可以自行调整里面配置）
![89b425bbe50e17c868eec.png](https://telegra.ph/file/89b425bbe50e17c868eec.png)

###  20. Serv00清理系统命令

``` SHELL
pkill -kill -u ${你的用户名}
chmod -R 755 ~/* \
chmod -R 755 ~/.* \
rm -rf ~/.* \
rm -rf ~/*
```
###  21. 清理完后切断Serv00SSH连接，清理后重新连接即可

``` SHELL
killall -9 -u $(whoami)
```
###  22. 无法访问以及运行内存超载导致的网站卡顿的解决方法

###  23. 首先用SSH连接上serv00上的服务器，在邮件里有SSH的地址，然后填写账号密码，我用的软件是FinalShell，进去之后，输入以下命令,  yourname替换为你的用户名

``` SHELL
pkill -kill -u yourname
```

###  24. 采集片源的话建议大家看视频,这里不方便添加图片了。

```
希望大家都能搭建好自己的影视站、 我只是一个小白啦 。
```  