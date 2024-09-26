---
title: NPM命令
cover: https://serv.200038.xyz/2024/09/19/049074.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-07-07 22:23:43
updated:
tags:
- npm命令
- 不太全
categories:
- 金克丝
keywords:
description:
top:
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
  
  NPM安装和使用命令
---
   
##  Npm命令

### 安装pm2

``` SHELL
 bash <(curl -s https://raw.githubusercontent.com/k0baya/alist_repl/main/serv00/install-pm2.sh)
```
{% link PM2,Saika,https://blog.rappit.site/2024/01/27/serv00_logs/ %}

### 如果你有安装自己使用 `go build` 构建的需求，你可以选择安装最新的 `go1.22` ，这里记录其安装过程

**由于 Serv00 服务器上并未提供 `go1.22` ，只提供了 `go1.20.3` ，无法正常进行构建工作，所以需要手动安装 `go1.22` 环境。**

``` SHELL
# 创建安装目录
mkdir -p ~/local/soft && cd ~/local/soft
# 下载编译好的 go1.22 的程序包
wget https://dl.google.com/go/go1.22.0.freebsd-amd64.tar.gz
# 解压
tar -xzvf go1.22.0.freebsd-amd64.tar.gz
# 删除压缩文件
rm go1.22.0.freebsd-amd64.tar.gz
# 修改 .profile 文件
echo 'export PATH=~/local/soft/go/bin:$PATH' >> ~/.profile
# 使 .profile 的修改生效
source ~/.profile
# 检查 go 版本
go version
```

### pm2启动命令

``` SHELL
package.json中
"scripts": {
    "start": "node ./bin/www",
    "dev": "cross-env EXPRESS_NODE_ENV=dev EXPRESS_PORT=3000 nodemon ./bin/www --exec babel-node",
    "sit": "cross-env EXPRESS_NODE_ENV=sit nodemon ./bin/www --exec babel-node",
  },
  
  
简单用法
1. npm run dev
2. pm2 start npm -- run dev
以上使用是等效的
  
pm2 start npm --watch --name nickname -- run sit
// 启动 npm run sit
eg: pm2 start npm --watch --name h5toolsit -- run sit
其中 --watch监听代码变化，--name 重命令任务名称，-- run后面跟脚本名字
```

### 常用命令

``` SHELL
npm install pm2 -g     # 命令行安装 pm2 
pm2 start app.js -i 4 #后台运行pm2，启动4个app.js 
                              # 也可以把'max' 参数传递给 start
                              # 正确的进程数目依赖于Cpu的核心数目
pm2 start app.js --name my-api # 命名进程
pm2 list               # 显示所有进程状态
pm2 monit              # 监视所有进程
pm2 logs               #  显示所有进程日志
pm2 stop all           # 停止所有进程
pm2 restart all        # 重启所有进程
pm2 reload all         # 0秒停机重载进程 (用于 NETWORKED 进程)
pm2 stop 0             # 停止指定的进程
pm2 restart 0          # 重启指定的进程
pm2 startup            # 产生 init 脚本 保持进程活着
pm2 web                # 运行健壮的 computer API endpoint (http://localhost:9615)
pm2 delete 0           # 杀死指定的进程
pm2 delete all         # 杀死全部进程
```

### 显示pm2版本

``` SHELL
 pm2 --version
```

### 显示所有由pm2管理的进程的状态

``` SHELL
pm2 status
```

### 查看每个进程的ID

``` SHELL
pm2 list |  pm2 ls
```
### 在系统重启时自动启动pm2和它的进程

``` SHELL
pm2 startup
```

### 停止pm2的进程

``` SHELL
pm2 stop <id>
```

### 删除pm2进程     

``` SHELL
pm2 delete <id>
```
### 删除全部进程

``` SHELL
pm2 delete all
```

### 停止所有应用程序

``` SHELL
pm2 stop all
```

### 重启所有应用程序

``` SHELL
pm2 restart all --update-env
```

### 保存当前应用列表 以便在重新启动或机器重启后自动恢复这些应用程序.

``` SHELL
pm2 save
```
### 设置开机自启动进程

``` SHELL
pm2 startup
```
### 查看运行时间和启动时间

``` SHELL
pm2 describe 进程ID | grep -E "uptime|created at"
```
### 获取进程详细情况

``` SHELL
pm2 describe 进程ID
```
### 监控每个node进程的cpu的内存使用情况

``` SHELL
pm2 monit
```
### 显示所有进程的日志信息

``` SHELL
pm2 logs
```
### 卸载pm2

``` SHELL
pm2 unstartup
pm2 delete all
npm uninstall -g pm2
```

### 使用pm2启动脚本：pm2 start 脚本 --interpreter=编程语言
### 不加--interpreter=编程语言有些也能运行

### 添加pm2到Path里面：

``` SHELL
步骤 1: 编辑你的 shell 配置文件
nano ~/.bashrc

步骤 2: 添加 cloudflared 到你的 PATH
在文件的末尾，添加以下行：
export PATH="$PATH:/home/pdf/.npm-global/bin"
按下 Ctrl + O 保存文件，然后回车，然后按 Ctrl + X 退出 nano。

步骤 3: 应用更改
重新加载 .bashrc 文件：
source ~/.bashrc

步骤 4: 验证更改
pm2 --version
```
###  我是一个热爱学习的小白希望大家多多帮助,谢谢大家么么哒。

### 另外感谢一位大佬，杨幂的脚，俗称CM喂饭大佬 下面是他的个人博客

{% sitegroup %}
{% site CM喂饭干货满满, url=https://blog.cmliussss.com, screenshot=https://img.090227.xyz/api/cfile/AgACAgUAAyEGAASOgsooAAMbZuEs2AeeHh93Z8PnjFINL7LpZXEAAr6_MRvVJAlXSYSISKu9iD4BAAMCAAN3AAM2BA, avatar=https://img.090227.xyz/file/5593a0a32f1082a8fb83d.jpg, description=CM喂饭干货满满 %}
{% endsitegroup %}