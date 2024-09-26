---
title: Serv00最简单的哪吒搭建方式
cover: https://serv.200038.xyz/2024/09/16/825387.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-07-26 22:23:31
updated:
tags:
- Serv00
- 一键哪吒
- 最简单的哪吒教程
categories:
- 学习中
keywords:
description:
top: 8
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

  Serv00最简单的哪吒搭建教程
---
  
###  1. 首先注册一个Serv00账号
  - [网址链接](https://www.serv00.com/)

  - 建议使用大厂邮箱注册，注册好会有一封邮箱上面写着你注册时的用户名和密码。
![e722f861dcbc0c156df7e.png](https://telegra.ph/file/e722f861dcbc0c156df7e.png)

  -  **Serv00哪吒项目地址**  https://github.com/k0baya/nezha4serv00

  -  **连接工具`FINSHELL`**
   - **免费正版**: [下载链接](https://www.hostbuf.com/t/988.html)

- **演示网站**  https://dongfang.serv00.net/
---

###  2. 安装前需准备好以下工作
---

-  2. 登入邮件里面发你的 `DevilWEB webpanel` 后面的网址，进入网站后点击 `Change languag` 把面板改成英文

-  3. 然后在左边栏点击 `Additonal services` ,接着点击 `Run your own applications` 看到一个 `Enable` 点击

-  4. 找到 `Port reservation` 点击后面的 `Add Port` 新开二个端口，随便写，也可以点击 `Port`后面的 `Random`随机选择`Port tybe` 选择 `TCP`

-  5. 然后点击 `Port list` 你会看到二个端口
![47f7ff3cef24bb73eb488.png](https://telegra.ph/file/47f7ff3cef24bb73eb488.png)

-  6. 如果要用Serv00自带域名把网站里面的删除即可。

-  7. 找到左边栏 `WWW websites` 点击 `Add nwe websites` 填写你的域名，也可以用别的域名。这里我用Serv00自带的域名
![fba8c3dc4c813fec7e447.png](https://telegra.ph/file/fba8c3dc4c813fec7e447.png)

-  8. 如果想用别的域名只需要解析你添加到serv00里面的A记录即可。找到 `WWW websites` 点击后面的 `Mange SSL` 就可以看到二个IP，一般添加第一个IP就可以了。

-  9. 添加自己的域名开启DNS的话 在左边栏 `DNS zones`也可以看到A记录

-  10. 在Serv00面板申请添加别的域名证书点击 `WWW websites` 找到 `Manage SLL`看到图片后面的 `Manage`点击

![sss.png](https://openai-75050.gzc.vod.tencent-cloud.com/openaiassets_b336d06fe3d3ce7e0fae18658bcb2a7e_2579861726332171009.png) 
 
![CC3_HQ$_UOMMIQT{PV0D3FR.png](https://openai-75050.gzc.vod.tencent-cloud.com/openaiassets_1273d8d2946d6da4ca3e406109642125_2579861726332578331.png)

###  3. 准备Github里面的三个东西，按照以下步骤后保存到一边
---

-  2. 进入Gihub点击右上角头像找到 `Settings` 点击后往下拉找到左边栏下面的 `Developer settings` 点击

-  3. 然后会看到三个应用点击 `OAuth Apps` 找到 `New OAuth App`点击后 按照下图所填，然后点击 `Register application`
![32ecbc30da793dac3ff4d.png](https://telegra.ph/file/32ecbc30da793dac3ff4d.png)

-  4. 进入后会看到下图
![bd2aaa18338036461586d.png](https://telegra.ph/file/bd2aaa18338036461586d.png)

-  5. 看到 `Client ID`下面的ID  `Client secrets` 点击左边的 `Generate seceet` 后你会得到一个密码保存好后面会用到。

-  6. 这里的`Application name` 可以随便写, `Authorization callback URL`的代码复制下面的,记得前面的网址改成你的。

``` SHELL
https://dongfang.serv00.net/oauth2/callback
```
- **也可以这样输入 http://128.204.223.94:9888/oauth2/callback 。上面第二步里面的`URL` 也可以这样填防止登录不到面板端**

- **如果解析的域名登录不上面板记得改成 `Github` 的第`2`步 。如下图**
![7d44eb52a636ace3c32f2.png](https://telegra.ph/file/7d44eb52a636ace3c32f2.png)

##   这样我们前期工作已经准备完成
---

##  开始安装

###  1. 用我们前面下载的工具登入SSH

###  2. 第一次连接还是会弹出输出密码记得点X ,按照下图添加密码
![d2d36f604b23ad7a9eb46.png](https://telegra.ph/file/d2d36f604b23ad7a9eb46.png)

###  3. 进入到面板后复制下面代码到面板安装

``` SHELL
bash <(curl -s https://raw.githubusercontent.com/k0baya/nezha4serv00/main/install-dashboard.sh)
```
###  4. 然后按照以下提升输入

| 名字 | 内容 |
| --- | --- |
| 请输入 OAuth2 提供商(github/gitlab/jihulab/gitee，默认 github):  | 回车就行 |
| 请输入 Oauth2 应用的 Client ID | 前面页面里面保存的ID |
| 请输入 Oauth2 应用的 Client Secret | 右边保存的密码 |
| 请输入 GitHub/Gitee 登录名作为管理员，多个以逗号隔开 | 页面头像后面的用户名 |
| 请输入站点标题 | 随便写 |
| 请输入站点访问端口 | Serv00网站设置的第一个端口 |
| 请输入用于 Agent 接入的 RPC 端口 | 第二个端口 |

###  5. 这样我们面板端就安装好了,接着去浏览器里面输入里面的链接如下图所示 
![2ea8ff0a3fc80a42a37a7.png](https://telegra.ph/file/2ea8ff0a3fc80a42a37a7.png)

###  6. 登入到面板端后点击右边用户名的管理后台找到设置里面的未接入CDN的面板服务器域名/IP

-    **填入解析的IP或者域名后保存** 
![~RAM.png](https://img.131213.xyz/file/09de917acb94db98a2f08.png)

-    **点击服务器新增服务器，名称随便填点击下面的的新增**
![TSKLSC7Q01DFHSZ}31~TA08.png](https://img.131213.xyz/file/b1040312a90d5264f67f9.png)

-    **下来会看到一个服务器后面的密钥下面我们会用到**
![N}~OUW1JC7ZV07(SAA){6ZK.png](https://img.131213.xyz/file/4d0bf1d7daf9a83ed60f4.png) 

###  7. 下来我们配置把serv00服务器添加到上面

###  复制以下代码

``` SHELL
bash <(curl -s https://raw.githubusercontent.com/k0baya/nezha4serv00/main/install-agent.sh)
```
###  填写以下内容

| 名字 | 内容 |
| --- | --- |
| 请输入 Dashboard 站点地址  | 解析的IP或者域名 |
| 请输入面板 RPC 端口： | 第二个端口 |
| 请输入 Agent 密钥 | 面板服务器后面的密钥 |

### 接下来直接回车就行了。然后我们去到网址点击服务器前面的图像就会看到我们的服务器在线了。
![abe072ecaf54139e44aea.png](https://telegra.ph/file/abe072ecaf54139e44aea.png)

### Serv00清理系统命令

``` SHELL
pkill -kill -u ${你的用户名}
chmod -R 755 ~/* \
chmod -R 755 ~/.* \
rm -rf ~/.* \
rm -rf ~/*
```
### 清理完后切断Serv00SSH连接，清理后重新连接即可

``` SHELL
killall -9 -u $(whoami)
```

### 如果你是V6鸡,需要先装一个Warp，然后在安装F大隧道版哪吒

``` SHELL
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh [option] [lisence/url/token]
```

### VPS F大 Argo版哪吒脚本

``` SHELL
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen2/Argo-Nezha-Service-Container/main/dashboard.sh)
```
### [Argo 认证的获取方式: json 或 token链接]( https://fscarmen.cloudflare.now.cc)




* 最后我就是一个小白啦。
* 这个搭建的应该是最简单了,但是写起来是真复杂，基本看了都会操作，有点小累阿。
* 希望大家都可以搭建成功啦。
* 提示如果你的面板端或者监控端掉了重新输出上面的代码即可。**面板端输入第一个**，**监控端输入第二个**。