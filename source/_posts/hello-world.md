---
title: 图床解决方案：Cloudflare R2+PicGo+WebP Cloud
cover: https://serv.200038.xyz/2024/09/19/837691.webp
top_group_index: 10
background: '#fff'
date: 2024-07-11 20:49:52
updated:
tags:
- 图床解决方案：Cloudflare 
- Cloudflare R2
- PicGo+WebP Cloud
categories:
- Cloudflare
- Hexo
keywords:
description:
top: 3
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

- 这篇文章介绍了作者从 Telegraph 图床迁移到 Cloudflare R2 + PicGo + WebP Cloud 的过程。由于 Telegram 的审查问题，Telegraph 的图床服务不再可靠，作者寻找新的解决方案，期望其可靠、易用且免费。文章详细描述了如何启用 Cloudflare R2、设置 PicGo 以及使用 WebP Cloud 进行代理，最后提到使用 PicGo 插件 pic-migrater 迁移旧图片。作者确认在2024年9月的部署方式有效，并提供了具体的操作步骤。
---

此前我的图床是基于 `Cloudflare + Telegraph` 这两位大善人的，我本以为他们会比我的博客活得更久，因此我默认这是一个长期的解决方案，足够可靠易用，最重要的是免费。

但最近 Telegram CEO 被捕，韩国也因为审查方面的原因和 `Telegram` 有冲突，可能受此影响，`Telegraph` 的图床服务已经不能上床新的图片，旧的图片尚且可以访问，但也不知道什么时候就会完蛋。

于是我开始寻找新的图床解决方案，我的期望是可靠易用，最好免费，`Cloudflare R2+PicGo+WebP Cloud` 就是这样的解决方案。

本文主要参考了[这篇文章](https://sspai.com/post/90170)，另外包括了 `WebP Cloud` 自定义域名 和 从 `Telegraph 迁移图片到 R2 图床` 的内容。

---

## 部署


### 您需要

1. Cloudflare 账号，并绑定信用卡（开启 R2 的必要条件）
2.  一个域名（非必须）
接下来让我们开始吧...

### 1. 启用 Cloudflare R2
1. 打开 [Cloudflare](https://dash.cloudflare.com/) 控制台，选择 `R2`，在这里您可以看到 `R2` 的免费额度，点击同意启用。
2. 新建一个 bucket`（Create bucket）`
    1. 输入你喜欢的名字，例如 `image`。
    2. 选择你希望的地区，例如 `APAC`
	3. 点击 `Create bucket` 进行创建。
3. 点击刚创建的名为 `image` 的 bucket。
    1. 如果您有域名，进入 `setting`，设置 `Custom Domains`（如果您的域名就在 Cloudflare，可以很快速得直接添加）。
    2. 如果您没有域名，进入 `setting`，点击 `R2.dev subdomain` 旁的 `Allow Access`，输入 `allow`，你将会获得一个 `xxxxxx.r2.dev` 的地址。
    3. 现在您应该可以上传图片了，您可以在 `image bucket` 中的 `Objects` 板块中上传图片进行测试。
4. 现在点击页面左边的 `R2`，回到 `Overview`，在 `Account details` 下，点击 `Account ID`下的 `Manage R2 API Tokens`。
    1. 点击 `Create API token` 创建一个新的 `API token`。
    2. 取一个名字，例如 `image-R2`。
    3. Permission 选择 `Object Read & Write`。
    4. Specify buckets 下选择刚刚创建的 `image`。
    5. 点击 `Create API Token` 创建。
    6. 您将获得 `PicGo` 所需的信息，包括 `Access Key ID`、`Secret Access Key` 以及 `endpoints`。只会显示一次，请先保存下来。
5. 至此，Cloudflare dashboard 中的操作已经完全结束。

### 2.设置 PicGo

1. 下载 [PicGo](https://github.com/Molunerfinn/PicGo)。
2. 安装后点击插件设置，搜索 `s3`，找到作者为 `WayJam So` 的插件，安装。
3. 进入图床设置，找到 `Amazon S3`，添加或者修改默认的设置。
    1. 图床配置名随便写，如 `r2`。
    2. 应用密钥 `ID` 为 `Access Key ID`。
    3. 应用密钥 为 Secret `Access Key`。
    4. 桶名 为您设置的 `bucket`名字，在这里为 `image`。
    5. 自定义节点 为 `endpoints`。
    6. 自定义域名 为 您设置的 `Custom Domain`s 或 `Cloudflare` 为您分配的 `xxxxxx.r2.dev` 地址。
    7. 点击确定。

### 至此，您应该可以通过 PicGo 上传照片了。

### 3.使用 WebP Cloud 对您的地址进行代理。

1. 进入 [WebP Cloud Dashboard](https://dashboard.webp.se)，登陆。
2. 进入左侧的 `Price` 板块中您可以看到免费额度。
3. 进入左侧的 `Home` 板块，点击右下角的 `Create Proxy`。
    1. 选择你喜欢的地区，这里我选择 `Hillsboro, OR`。
    2. `Proxy Nam`e 随便填，例如 `R2-image`。
    3. `Proxy Origin URL` 填入您设置的 `Custom Domains 或` `Cloudflare` 为您分配的 `xxxxxx.r2.dev` 地址。
    4. 点击 `Create` 进行创建。
    5. 这时候将会给您分配一个 `xxxxxx.webp.li` 地址。

7. 如果您希望设置自定义域名，进入刚创建的这条 `Proxy`，点击 `Custom domain`，根据提示在你的 DNS 解析中添加对应的条目，稍等片刻后您就可以在 `Custom domain` 中 `activate` 您的自定义域名了。

8. 接下来您需要在 `PicGo` 中更改 自定义域名 为您在 `WebP Cloud` 中设置的自定义域名或者是 `WebP Cloud` 为您分配的 `xxxxxx.webp.li` 地址。

### 4. 迁移

1. 我有一大堆图片保留在 Telegraph 的图床中，我希望将其全部迁移到 R2 中，PicGo 的插件 pic-migrater 是一个好的选择，开发者为 Molunerfinn。

2. 下载插件后，点击插件设置，点击插件右下角的小齿轮，点击 配置 `plugin - picgo-plugin-pic-migrater`。
新文件名后缀随便填，例如 `_new`。
3. 我将 旧内容写入新文件 设置为 `no`，被转换过的文件就会被命名为 源文件名`_new.md`，我可以方便对这些文件进行检查。
但对于某些 `markdown` 文件， `pic-migrater` 会出现无法迁移的情况，尚且不知道如何解决。我的做法是针对落单的文件一个一个手动处理。

{% link 博文转载自,Jayden,https://xxu.do/posts/geek/Cloudflare-R2+PicGo+WebP-Cloud %}




Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)
