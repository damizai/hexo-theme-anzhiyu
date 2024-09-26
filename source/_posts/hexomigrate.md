---
title: Hexo博客如何迁移到新电脑
cover: https://serv.200038.xyz/2024/09/19/828325.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-08-15 15:10:05
updated:
tags:
- Hexo迁移
- 个人博客
categories:
- Hexo
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

  Hexo博客如何迁移到新电脑
---

## Hexo博客如何迁移到新电脑

### 参考教程：[CSDN:Hexo博客迁移到新电脑](https://blog.csdn.net/qq_43698421/article/details/120407042)

### 1. 在新电脑行进行环境准备工作，[具体的步骤看Hexo博客搭建教程](https://hexo.200038.xyz/jinx/HexoBlog/)，大家在新电脑上跟着做即可（注意千万不要做第9步，`hexo init blog-demo`这一步会覆盖并还原你原本的的源码文件）

### 2. 这时候新建一个文件夹`new-blog`，用来装你的新博客源码的，进入这个文件夹，准备复制我们旧的博客源码进来，我们可以看到旧的博客项目结构是如下样子的：
![undefined](https://img.200038.xyz/api/file/868db7f446a06eda9c531.png)

- 这里红框内的都是需要复制迁移到新的博客的，具体的要不要保留见下表
| 需要复制的 | 需要删除的 |
| --- | --- |
| _config.yml：站点配置文件 | .git：无论是在站点根目录下，还是主题目录下的.git文件，都可以删掉 |
| _config.butterfly.yml：主题配置文件，为了方便主题升级剥离出来的配置文件 | node_modules：npm install会根据package.json生成 |
| package.json：说明使用哪些依赖包 | public：hexo g会重新编译生成 |
| scaffolds：文章的模板 | .deploy_git：在使用hexo d时也会重新生成 |
| source：自己写的博客源码 | db.json文件：hexo s快速启动所需的数据库 |
| themes：主题文件夹（魔改都在里面啦） | package-lock.json：记录依赖之间的内部依赖关系，可以根据package.json重新生成 |
| .gitignore：说明在提交时哪些文件可以忽略 |  |

### 3. 复制所需的文件到新电脑的文件夹之后，在`git bash`中切换目录到新拷贝的文件夹里，使用`npm install` 命令，进行模块安装。这里绝对不能使用`hexo init`初始化，因为有的文件我们已经拷贝生成过来了，所以不必用`hexo init`去整体初始化，如果不慎用了，则站点的配置文件`_config.yml`里面内容会被重置，所以这一步一定要慎重：

``` BASH
npm i
```

### 4. 执行以下命令情况并启动项目，进入`http://localhost:4000`进行验证：

``` BASH
hexo cl; hexo g; hexo s
```

### 5. 当本地能成功启动，之后就可以部署到Github，执行以下代码：

``` BASH
hexo d
```

### 6. 如果出现Deploy done，则说明部署成功，稍等两分钟，打开浏览器访问之前的域名就可以看到之前的博客，以后你可以在这台新电脑上魔改和写文章了~