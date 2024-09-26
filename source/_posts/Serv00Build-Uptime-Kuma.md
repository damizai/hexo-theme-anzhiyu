---
title: Serv00 搭建网站监控 Uptime-Kuma
cover: https://serv.200038.xyz/2024/09/18/623949.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-08-02 00:18:06
updated:
tags:
- Serv00 
- 网站监控
- TCPping
- VPSping
- CloudFlared Tunnels
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

  Serv00搭建网站监控 Uptime-Kuma
---

##  1. 首先注册一个Serv00账号
  - [网址链接](https://www.serv00.com/)

  - 建议使用大厂邮箱注册，注册好会有一封邮箱上面写着你注册时的用户名和密码。
![e722f861dcbc0c156df7e.png](https://telegra.ph/file/e722f861dcbc0c156df7e.png)

  -  **连接工具`FINSHELL`**
   - **免费正版**: [下载链接](https://www.hostbuf.com/t/988.html)

---

## 部署应用的一些准备工作

**在部署自己的应用之前，我建议提前安装好 pm2 以及 Cloudflared （可选）。前者是进程管理工具，用来方便开机自启，以及程序崩溃后自启，查阅进程运行情况等等。后者是 Cloudflare 的 Argo 隧道客户端，用它也可以给自己部署的应用加域名。特别是 Uptime Kuma ，更加推荐使用 Cloudflared 加域名，而不建议使用面板自带的 Proxy 。**

## Pm2

在 SSH 连接 serv00 之后，使用以下脚本安装 pm2 ：

``` BASH
bash <(curl -s https://raw.githubusercontent.com/k0baya/alist_repl/main/serv00/install-pm2.sh)
```
-  **如果安装完成后执行 pm2 提示命令未找到，你可以断开 SSH 连接，再重新连接，即可。**

## Cloudflared Tunnels

### 创建并进入Cloudflared 的工作目录：

``` BASH
mkdir -p ~/domains/cloudflared && cd ~/domains/cloudflared
```
### 下载 Cloudflared：

``` BASH
wget https://cloudflared.bowring.uk/binaries/cloudflared-freebsd-latest.7z && 7z x cloudflared-freebsd-latest.7z && rm cloudflared-freebsd-latest.7z && mv -f ./temp/* ./cloudflared && rm -rf temp
```
### 测试运行：

``` BASH
./cloudflared tunnel --edge-ip-version auto --protocol http2 --heartbeat-interval 10s run --token ARGO_TOKEN
```
-  **其中 `ARGO_TOKEN` 要替换成自己的。确定运行没有问题后，按 `Ctrl+c`即可停止运行。**

### 使用 pm2 启动 Cloudflared：

``` BASH
pm2 start ./cloudflared -- tunnel --edge-ip-version auto --protocol http2 --heartbeat-interval 10s run --token ARGO_TOKEN
``` 
-  **其中 `ARGO_TOKEN` 要替换成自己的。**

---

## 准备工作完成下来安装 Uptime-Kuma

-  1. 登入邮件里面发你的 `DevilWEB webpanel` 后面的网址，进入网站后点击 `Change languag` 把面板改成英文

-  2. 然后在左边栏点击 `Additonal services` ,接着点击 `Run your own applications` 看到一个 `Enable` 点击

-  3. 找到 `Port reservation` 点击后面的 `Add Port` 新开一个端口，随便写，也可以点击 `Port`后面的 `Random`随机选择`Port tybe` 选择 `TCP`

### 也可以按照下图所示填写 `Add a New Website `：

| 名字 | 内容 |
| --- | --- |
| Domain | xxx.USERNAME.serv00.net（也可以把原有的USERNAME.serv00.net删掉后重新添加 |
| Website Type | proxy |
| Proxy Target | localhost |
| Proxy URL | 留空 |
| Proxy port | False |
| Use HTPPS | Serv00网站设置的第一个端口 |
| DNS support | True |

### 添加完新站点后，继续点击上方的 `Manage SSL certificates` ，接着在出口 IP 的右侧点击 `Manage` ，再点击 `Add certificate` ：

| 名字 | 内容 |
| --- | --- |
|Generate Let’s Encrypted certificate	| 与刚刚添加的站点域名保持一致（如果是原有的USERNAME.serv00.net ，可以省略此步）|

### 接着 SSH 登入，并进入刚刚你新建的域名目录下：

``` BASH
# 下载 v1.22.1 版本的源代码
cd ~/domains && wget https://github.com/louislam/uptime-kuma/archive/refs/tags/1.22.1.zip && unzip 1.22.1.zip && rm -rf public_html && mv -f uptime-kuma-1.22.1 public_html && rm -f 1.22.1.zip && cd public_html
```
### 设置生产模式：

``` BASH
npm ci --production
```

### 下载dist文件：

``` BASH
wget https://github.com/louislam/uptime-kuma/releases/download/1.22.1/dist.tar.gz && tar -xzvf dist.tar.gz && rm dist.tar.gz
```

### 安装补充依赖：

``` BASH
npm install
```
-  **安装过程中多少会有报错，无视就好，实际上最后可以正常运行。内置的Cloudflared反向代理在FreeBSD平台上无法使用，但是可以使用上述的外置的Cloudflared进行反代，使用自己的域名。**

### 测试运行：

``` BASH
node server/server.js --port=PORT
```
- **记得把`PORT`替换成你放行的端口。确定运行没有问题后，按 `Ctrl+c`即可停止运行。**

### 使用pm2管理后台运行：

``` BASH
pm2 start server/server.js --name uptime-kuma -- --port=PORT
```
- **把`PORT`替换成你放行的端口**

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

```
  最后我就是一个小白啦。
  希望大家都可以搭建成功啦。
```

{% link 本博文转载自,Saika,https://saika.us.kg/2024/01/27/serv00_logs/#Uptime-Kuma %}