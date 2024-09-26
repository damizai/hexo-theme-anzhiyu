---
title: Hexo博客搭建 Hexo + GitHub Pages + Cloudflare Pages 搭建教程
cover: https://serv.200038.xyz/2024/09/19/722451.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-08-03 12:20:08
updated:
tags:
- Hexo
- Github
- 个人博客
- Cloudflare pages
- Noge.js
- Git
- Markdown
- 静态网站
categories:
- Hexo
keywords:
description:
top: 88
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

- 这篇文章介绍如何使用 Hexo+ GitHub Pages + Cloudflare Pages搭建个人专属博客
---
{% note blue 'anzhiyufont anzhiyu-icon-bullhorn' simple %}
博客视频 ,来自[CMLiussss](https://blog.cmliussss.com/p/HexoBlogNo1/),记录方便以后学习。
{% endnote %}

# 搭建Hexo博客，快速简洁高效，零成本搭建个人博客：Hexo + GitHub Pages + Cloudflare Pages 搭建教程

<div class="video-container">
[<iframe width="970" height="546" src="https://www.youtube.com/embed/GtYcFZ55GJI" title="【Hexo博客系列】No.1 搭建Hexo博客，快速简洁高效，零成本搭建个人博客：Hexo + GitHub Pages + Cloudflare Pages 完整指南 #blog" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>]
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

## 本文详细介绍了如何使用Hexo框架搭建一个个人博客，并将其部署到GitHub Pages和Cloudflare Pages上。主要内容包括：

- 2. 环境准备：安装Node.js和Git
- 3. 配置Git和GitHub：设置SSH密钥，创建GitHub仓库
- 4. 初始化Hexo项目：安装Hexo，创建新博客
- 5. 部署到GitHub Pages：配置部署设置，推送静态文件
- 6. 部署到Cloudflare Pages：连接GitHub仓库，自动部署
- 7. 基本使用方法：创建新文章，本地预览，发布更新

### 这个教程适合那些想要快速搭建个人博客，但又不想花费太多成本的人。通过使用Hexo、GitHub和Cloudflare的免费服务，您可以轻松创建一个高效、简洁的博客网站。

---

## 1. 准备工作

-   `域名` （**非必须**，你也可以使用免费域名，或者`GitHub.io`或`Pages.dev`分配的域名也可以）
-   [Github](https://github.com/) （**必须**，你需要注册一个GitHub帐号）
-   [Cloudflare](https://dash.cloudflare.com/)（非必须，你需要注册一个Cloudflare帐号，这样你就可以将博客部署在CF的CDN里加速，但是你也可以直接使用GitHub.io分配的域名）

---

## 2. 软件支持

1. [Node](./#2-1安装-Node)（必须）
2. [Git](./#2-2安装-Git)（必须）
3. [VSCode](https://code.visualstudio.com/)（非必须，这是一款轻量型的代码编辑器，可以帮助你养成一个很好的编程习惯）

## 3.1.安装 Node

1. 打开Node官网，下载和自己系统相配的Node的安装程序，否则会出现安装问题。下载地址：https://nodejs.org/en
2. 下载后安装，安装的目录可以使用默认目录 `C:/Program Files/nodejs/`
3. 安装完成后，检查是否安装成功。在键盘按下Win + R键，输入CMD，然后回车，打开CMD窗口，执行 `node -v` 命令，看到版本信息，则说明安装成功。
4. 修改npm源。npm下载各种模块，默认是从国外服务器下载，速度较慢，建议配置成华为云镜像。打开CMD窗口，运行如下命令：


``` CMD
npm config set registry https://mirrors.huaweicloud.com/repository/npm/
```
## 4.1.安装 Git

1. 进入官网下载适合你当前系统的 Git：**https://git-scm.com/downloads**
2. 下载后安装Git即可，安装的目录最好使用默认目录`C:/Program Files/Git`
3. 点击电脑左下角开始即可看见`Git CMD`、`Git Bash`、`Git GUI`。

-  **`Git CMD`是windows 命令行的指令风格**
-  **`Git Bash` 是linux系统的指令风格（建议使用）**
-  **`Git GUI`是图形化界面（新手学习不建议使用）**

---

## 5. 配置 Git 密钥并连接至 Github

### 常用 Git 命令

``` BASH
git config -l  //查看所有配置
git config --system --list //查看系统配置
git config --global --list //查看用户（全局）配置
```

## 6. 配置用户名和邮箱

``` BASH
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```
- **通过`git config -l` 检查是否配置成功。**

## 7. 配置公钥连接Github

-   执行以下命令生成ssh公钥，此公钥用于你的计算机连接Github

``` BASH
ssh-keygen -t rsa -C "你的邮箱"
```
- **提示`Enter file in which to save the key`直接一路回车即可，新手小白不推荐设置密钥**

-   之后打开`C`盘下用户文件夹下的`ssh`的文件夹，会看到二个文件

-   **`id_rsa`私钥**
-   **`id_rsa.pub`公钥**

-   用记事本打开`id_rsa.pub`中的公钥，复制里面的内容，然后开始在github中配置ssh密钥。

-   将 `SSH KEY` 配置到 `GitHub`
进入github，点击右上角头像 选择`settings`，进入设置页后选择 `SSH and GPG keys`，名字随便起，公钥填到Key那一栏。

-   测试连接，输入以下命令

``` BASH
ssh -T git@github.com
```
- **第一次连接会提示`Are you sure you want to continue connecting (yes/no/[fingerprint])?`，输入yes即可**

##  出现连接到账户的信息，说明已经大功告成，至此完成了环境准备工作。

---

## 8. 创建GitHub.io仓库

-   点击右上角的`+`按钮，选择`New repository`，创建一个<用户名>.`github.io`的仓库。
-   仓库名字的格式必须为：`<用户名>.github.io` (注意：前缀必须为用户名，此为预览博客需要，后期可修改仓库名)
-   可见性必须选择 `Public` 方便第一次部署检查问题，点击 `Creat repository `进行创建即可

## 9. 初始化 Hexo 博客

-   创建一个文件夹来保存博客源码（我这里选的路径为`D:/Hexo-Blog`），在文件夹内右键鼠标，选择`Open Git Bash here`
-   在`Git BASH`输入如下命令安装 `Hexo`

``` BASH
npm install -g hexo-cli && hexo -v
```
-   安装完后输入`hexo -v`验证是否安装成功。
-   初始化 Hexo 项目安装相关依赖。

``` BASH
hexo init blog-demo
cd blog-demo
npm i
```
-   初始化项目后，打开`blog-demo`有如下结构

| 文件名 | 解释 |
| --- | --- |
|node_modules  | 依赖包 |
| scaffolds | 生成文章的一些模板 |
| source | 用来存放你的文章 |
| themes | 主题 |
| .npmignore | 发布时忽略的文件（可忽略） |
| _config.landscape.yml | 主题的配置文件 |
| config.yml | 博客的配置文件 |
| package.json | 项目名称、描述、版本、运行和开发等信 |
-   打开**Open Git Bash here输入**`hexo cl && hexo s`启动项目

-   打开浏览器，输入地址：**http://localhost:4000/** ，看到视频里的效果，说明你的博客已经构建成功了。

## 10. 将静态博客挂载到 GitHub Pages

-   安装 **hexo-deployer-git**

``` BASH
npm install hexo-deployer-git --save
```
-   修改 `_config.yml` 文件

-  **在blog-demo目录下的_config.yml，就是整个Hexo框架的配置文件了。可以在里面修改大部分的配置。详细可参考官方的配置描述。**
-  **修改最后一行的配置，将repository修改为你自己的github项目地址即可，还有分支要改为`main`代表主分支（注意缩进）**

``` YAML
deploy:
  type: git
  repository: git@github.com:你的Github名/你的Github名.github.io.git
  branch: main
```
-   修改好配置后，运行如下命令，将代码部署到 GitHub（Hexo三连）。

``` BASH
// Git BASH终端
hexo clean && hexo generate && hexo deploy  

// 或者

// VSCODE终端
hexo cl; hexo g; hexo d
```

- ***hexo clean***：删除之前生成的文件，可以用`hexo cl`缩写。
- ***hexo generate***：生成静态文章，可以用`hexo g`缩写
- ***hexo deploy***：部署文章，可以用`hexo d`缩写

- **注意：`deploy`时可能要你输入 `username` 和 `password`。**
- **如果出现`Deploy done`，则说明部署成功了。**

### 稍等两分钟，打开浏览器访问：https://你Github的用户名.github.io ，这时候我们就可以看到博客内容了。

---

## 12. 将静态博客挂载到 Cloudflare Pages

-   在 **Workers** 和 **Pages** 中选择 `Pages` 的 连接到 `Git`
-   然后登录你`Blog`仓库对应的`GitHub`帐号
-   点击`保存并部署`后等待部署完成。
-   提示成功！您的项目已部署到以下区域：全球后，浏览器访问：`Cloudflare Pages` 分配的域名 ，这时候我们就可以看到博客内容了。
-   当然也可以添加自己的自定义域名
-  **这时你也就可以将你的`<用户名>.github.io`的仓库设置为`Private`私库了**

---

## 13. 如何使用

-   新建一篇博文

``` BASH
hexo new 这是一篇新的博文
```

-  然后用文本编辑器去编辑`_posts/`这是一篇新的博文.md里的内容即可，注意要使用`Markdown`格式书写。
详细使用方法可以查阅 https://hexo.io/zh-cn/docs/writing


-   编辑完文章保存后可以使用如下命令，生成本地页面 http://localhost:4000/ ，进行预览

``` BASH
// Git BASH终端
hexo cl && hexo s

// 或者

// VSCODE终端
hexo cl; hexo s
```
-   确认无误后使用以下命令，将本地文章推送至`GitHub`仓库即可

``` BASH
// Git BASH终端
hexo cl && hexo g && hexo d

// 或者

// VSCODE终端
hexo cl; hexo g; hexo d
```
---

###  VSCODE 终端首次执行报错 使用管理员身份打开 `powershell` ,输入以下命令

``` POWERSHELL
Set-ExecutionPolicy RemoteSigned
```

### Hexo 部分数据无法更新，或者新生成的文件与上一版本完全相同，请清理缓存后重试。

``` SHELL
  hexo clean
```
--- 

{% link 本博文转载自,CM喂饭大佬,https://blog.cmliussss.com/p/HexoBlogNo1/ %}
###  CM大佬 :  **Blog**  https://blog.cmliussss.com
###  CM大佬 : **YouTobe** https://www.youtube.com/@CMLiussss
###  项目地址 : **Hexo** https://github.com/hexojs/hexo

###  参考资料

**https://hexo.io/zh-cn/**
**https://www.fomal.cc/posts/e593433d.html**
**https://docs.anheyu.com/**

###  主题美化  

- 项目地址 : https://github.com/anzhiyu-c/hexo-theme-anzhiyu
- 官方文档 : https://docs.anheyu.com/initall.html

###  主题美化参考资料 

https://docs.anheyu.com/initall.html
https://www.fomal.cc/posts/4aa2d85f.html
https://github.com/anzhiyu-c/hexo-theme-anzhiyu/blob/dev/README.md?plain=1
https://blog.csdn.net/COCO56/article/details/103840966
