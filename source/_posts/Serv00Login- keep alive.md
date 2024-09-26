---
title: Serv00登录保活
cover: https://serv.200038.xyz/2024/09/19/041677.webp
swiper_index: 10
top_group_index: 10
background: '#000000'
date: 2024-07-23 09:03:55
updated:
tags:
- Serv00保活登录
- GitHub
- Vercel
categories:
- 学习中
keywords:
description:
top: 5
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

  Serv00保登录的二种方式
---

# Serv00登录的方式 1

## GitHub

{% link Serv00,项目地址,https://github.com/lopins/serv00-auto-scripts %}

---

## 使用方法

- 1.  进入到该项目直接Fork.

- 2.  在 GitHub 仓库中，点击仓库中 `Settings`

- 3.  在侧边栏找到 `Secrets and variables`，点击展开选择 `Actions`，点击 `New repository secret`

- 4.  然后创建一个名为 `ACCOUNTS_JSON`的 `Secret`，将 JSON 格式的账号密码字符串作为它的值，如下格式：

``` SHELL
[  
  { "username": "qishihuang", "password": "zhanghao", "panelnum": "3" },  
  { "username": "zhaogao", "password": "daqinzhonggong", "panelnum": "1" },  
  { "username": "heiheihei", "password": "shaibopengke", "panelnum": "2" }  
]
```
### 其中`panelnum`参数为你登录时的serv00.com中的数值。比如 `s6.serv00.com`

- 5. 添加好之后回到项目页面找到 `Actions` 后去里面运行显示如下图就可以了
 ![ee6411f62c4a7acaf7c67.png](https://telegra.ph/file/ee6411f62c4a7acaf7c67.png)

---

# Serv00登录的方式 2

## Vercel

- **Vercel注册**
- [网址链接](https://vercel.com/)

{% link Vercel,项目地址,https://github.com/amakerlife/serv00-auto-renew %}

## 使用方法

- 1.  进入到该项目直接Fork.

- 2.  进入到项目点击
<a href="https://vercel.com/new/weilais-projects-8f6dd81b/clone?repository-url=https%3A%2F%2Fgithub.com%2Famakerlife%2Fserv00-auto-renew&env=BASIC_AUTH_USERNAME%2CBASIC_AUTH_PASSWORD%2CCRON_SECRET%2CHOST1%2CUSERNAME1%2CPASSWORD1&project-name=serv00-auto-renew&repository-name=serv00-auto-renew" style="display: inline-block; padding: 5px 10px; font-size: 14px; font-weight: bold; color: #fff; background-color: #333; border: 1px solid #444; border-radius: 4px; text-decoration: none;">
<span style="display: inline-block; margin-right: 5px;">&#9650;</span> <!-- 这个符号代表三角形 -->
    Deploy
</a>

-   会直接跳转到 `vercel` ,前提是已注册好账号。

- 3.  填写完必需环境变量后部署，如需添加多个，可在 `Settings` 里继续填写。

- 4.  部署完毕可在 https://your-domain.com/api/ssh-connect 确认是否可用。

### 环境变量	        

| 变量名 | 内容 |
| --- | --- |
| BASIC_AUTH_USERNAME | HTTP 基本认证用户名 |
| BASIC_AUTH_PASSWORD | HTTP 基本认证密码 |
| CRON_SECRET | Vercel 进行 Cron Jobs 时所用密码 |
| HOSTx | 例如 HOST1,可配置多个,为 SSH 连接地址 |
| USERNAMEx | 例如 USERNAME1,可配置多个,为 SSH 连接用户名 |
| PASSWORDx | 例如 PASSWORD1,可配置多个,为 SSH 连接密码 |
| BARKx (可选) | 例如 BARK1,可配置多个,为 BARK 密钥 |

### 如需添加多个，格式如下

``` SHELL
BASIC_AUTH_USERNAME=
BASIC_AUTH_PASSWORD=
CRON_SECRET=
HOST1=xxx1
USERNAME1=xxx1
PASSWORD1=xxx1
BARK1=

HOST2=xxx2
USERNAME2=xxx2
PASSWORD2=xxx2
```

- 5.  **修改好变量后点击部署成功后如下图**
![383f0a1aa574503ca4d63.png](https://telegra.ph/file/383f0a1aa574503ca4d63.png)

- 6.  部署完毕用Vercle分配的域名加上 `/api/ssh-connect`确认是否可用。

- 7.  打开网站后让你输入密码,输入你填写前面的二个变量后显示下图就可以了。
![ead76da2ec01facc04350.png](https://telegra.ph/file/ead76da2ec01facc04350.png)

- 8.  然后去看下日志成功没，如下图所示:
![d70612df78a92ee4ce7fa.png](https://telegra.ph/file/d70612df78a92ee4ce7fa.png)


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


  ``希望大家都能成功部署、 我只是一个小白啦``
 