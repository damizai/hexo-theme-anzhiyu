---
title: Serv00搭建Alist个人网盘
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-09-22 23:17:13
updated:
tags:
- serv00
- Alist
- 云盘
categories:
- 学习中
keywords:
description:
top:
top_img:
comments:
cover: https://serv.200038.xyz/2024/09/19/857815.webp
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
 
---

### 零成本搭建Alist个人网盘

一、配置基础运行环境

1. 开放运行权限

    1. 登录serv00控制台，进入`Additional services-Run your own applications`，允许运行第三方软件。

2. 部署alist [上传文件创建数据库可以看这篇文章](https://hexo.200038.xyz/jinx/tuchuang/)

    1. 上传文件 https://github.com/uubulb/alist-freebsd

3. 首次运行并配置alist

    1. 这里需要先登录ssh，可以用cmd的ssh命令来登录，也可以选择`Finshell`这类的软件来登录，登录地址以及用户名、密码在注册时发送的邮件里面有，用户密码就是控制台的登录账户密码。

    2. 登录ssh后先进入存放alist对应的文件夹，比如我这里域名为xxx，那这个文件夹实际路径为~/domains/xxx，依次输入以下命令运行alist：
``` SHELL
进入alist所在文件夹
cd ~/domains/xxx
给予alist运行权限
chmod +x alist
运行alist
./alist server
```
**友情提示 : 这里首次运行后会停止，此时已经生成管理员密码，且还需要修改配置文件，输出的内容中`the initial password is`这句后面就是密码，这个需要记住，等下会用上**。

4. 第一次运行完成后进入serv00控制台-`File manager`，配置`Alist`的配置文件。进入`Alist`存放目录，再进入`data`文件夹，打开并编辑`config.json`，这个就是`Alist`的配置文件

5. 这里只需要编辑三个地方，一个是数据库部分（database），把一开始建立好的数据库信息填入，只需要修改数据库类型（type，刚刚建立的是mysql就填这个）、数据库地址（host）、数据库名称（name）、数据库用户名（user）以及数据库密码（password），其他部分不用改动；

6. 第二部分是监听部分（scheme），这里监听地址（address）为了安全起见，改成“127.0.0.1”，运行端口部分（http_port）改成一开始在控制台开放的运行端口

7. 最后还需要把s3存储部分（s3）的端口（port）改成0，这里的0意思是不使用s3存储，因为默认的端口会有端口冲突，99%童鞋是不会用s3的，这里就干脆不用。修改完成后保存，就完成了alist配置
![png](https://assets.vviptuangou.com/e08f9bf3109f00d1b299cbdbe46f5eaca05a9044.jpg)
![png](https://assets.vviptuangou.com/ef3ebee963092acba84a04440bfd03b76b909786.jpg)

8. 运行Alist 配置无误后回到ssh，进入对应的文件夹，再次运行alist：

``` SHELL
./alist server
```
9. 但是此时是无法退出shh界面的，linux/freebsd正常情况下退出ssh就会结束当前运行的进程，为了能让alist在后台运行（退出ssh也能运行），则需要修改运行的命令，注意此时需要先结束掉原本在运行的alist程序，在ssh下同时按住ctrl+c就可以结束当前运行的程序，再输入以下命令

``` SHELL
screen ./alist server
```
**此时就可以关掉 `ssh`，`alist`也可以正常访问**。