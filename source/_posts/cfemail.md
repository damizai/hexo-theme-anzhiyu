---
title: 利用cloudflare+work+pages部署一个简易的临时邮件系统
cover: https://serv.200038.xyz/2024/09/19/783646.webp
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-08-07 12:28:34
updated:
tags:
- cloudflare
- wrok
- pages
- Cloudflare Temporary Mail
categories:
- Cloudflare
keywords:
description:
top: 
top_img: 
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

- 这篇文章介绍如何使用 Cloudflare + Pages 搭建一个简易的临时邮件系统
---

## 利用cloudflare+work+pages部署一个简易的临时邮件系统
---

{% link 视频转载自,MilaoneChannel,https://www.youtube.com/watch?v=HdDI5oaWzoA&t=905s %}

<div class="video-container">
[<iframe width="560" height="315" src="https://www.youtube.com/embed/HdDI5oaWzoA?si=RCTK8IBMDRwo1RUQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>]
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

## 项目官方文档
https://temp-mail-docs.awsl.uk/

## 项目github仓库
https://github.com/dreamhunter2333/cloudflare_temp_email

## 安装过程

### 1. 首先要定义两个域名

- 2. 前端url `mail.jinx.com`
- 3. 后端url `cfmail-api.jinx.com`

### 2. 数据库设置

- 2. 在`works`和`pages`中选D1数据库
- 3. 创建数据库起名字`dev`
- 4. 创建后进入到`dev`数据库,然后打开`consol`标签
-把 **https://github.com/dreamhunter2333/cloudflare_temp_email/blob/main/db/schema.sql**这个schema.sql文件中的内容复制到donsol中,然后点击Execute按钮
- 5. 数据库创建完成

### 3. 后台程序部署

- 2. 在`works`和`pages`中,创建应用程序,选**workers**
- 3. 起名字`cfmail-api`,保存,然后点右下角完成.
- 4. 然后界面中右上角点`edit code`.
- 5. 然后再左边点击文件按钮,右键点`works.js`然后删除.
- 6. 再下载 [works.js](https://github.com/dreamhunter2333/cloudflare_temp_email/releases/latest/download/worker.js)
- 7. 右键点击,出现上传,把下载的`works.js`上传上去,然后右上角部署
- 8. 再来到项目的`settings-->Variables`中,添加变量
- 9. 开始部署时我们只添加4个变量,文章结尾我附带了可设置的变量代码示例说明

```
ADMIN_PASSWORDS = ["1234"]
PASSWORDS = ["1234"]
DOMAINS = ["jinx.com"]
JWT_SECRET =["xxxyyyzzz"]
```

### 4. 在KV Namespace Bindings中添加一个KV KV变量名 `KV`

- 2. 创建一个KV,起名字`dev`
- 3. 然后在这里`Variable name`填 KV 大写.
- 4. KV Namespace选择创建的KV库`dev`

### 5. 添加D1数据库 D1变量名 `DB`

- 2. 同样在`settings-->Variabl`e中,找到`D1 Database`,添加上一步创建的数据库`dev` 
最后再进行部署一次.

### 6. 后端验证

- 2. 后端设置完成后,可以通过访问后端域名的url及目录进行验证,前面的域名改成你部署的域名
- 3. **mail.jinx.com** 返回结果OK
- 4. **mail.jinx.com/health_check** 返回结果OK
- 5. 则说明后端配置完成.后期可随时在变量中增删内容以达到配置效果

### 7. 前台程序部署

- 2. 在`works`和`pages`中,创建应用程序,选`Pages`
- 3. 选择`Create using direct upload`,然后再选择`Upload assets`按钮
- 4. 然后来到作者的官方文档中 [点击这里生成配置文件](https://temp-mail-docs.awsl.uk/zh/guide/ui/pages.html)
在该页面中的地址栏输入后端的域名的https地址,比如我使用的地址是https://cfmail-api.jinx.com 生成配置,得到下载一个frontend.zip文件,上传到pages中.
- 5. 最后在Custom Domain给前端自定义一个域名,例如我使用的是mail.jinx.com
- 6. 前端验证,访问前端https://mail.jinx.com,此时应该出现界面并提示输入密码.

### 8. 邮件路由设置

- 2. 来到https://dash.cloudflare.com 面板首页,然后选择需要使用的域名进入.
- 3. 左边选择`Email`菜单,在`Email Routing`中选择`Routing ruls`中**Catch-all address**
激活,并且`edit`.
- 4. 其中的`Action`选择的是**Send to a Worker** ,目标选择后端的`worker`名字
- 5. 验证:截止到现在登录前端url已经可以

### 9. 发送邮件设置

- 2. https://resend.com/domains进行域名验证
- 3. 然后在`API-Key `中创建一个**api**,全部权限,然后把密码拷贝
- 4. 到后端的`Worker`中`settings-->Environment Variables-->`添加一个变量
- 5. RESEND_TOKEN = re_PxW46o6o_HJrmMYARCGdhMtB3JHD(上一步拷贝出来的密码)
- 6. 截止到以上步骤,就可以完整的收发邮件了.

### 10. 变量说明
```
[vars]
# TITLE = "Custom Title" # 自定义网站标题
PREFIX = "tmp" # 要处理的邮箱名称前缀，不需要后缀可配置为空字符串
# 如果你想要你的网站私有，取消下面的注释，并修改密码
# PASSWORDS = ["123", "456"]
# admin 控制台密码, 不配置则不允许访问控制台
# ADMIN_PASSWORDS = ["123", "456"]
# admin 联系方式，不配置则不显示，可配置任意字符串
# ADMIN_CONTACT = "xx@xx.xxx"
DOMAINS = ["xxx.xxx1" , "xxx.xxx2"] # 你的域名, 支持多个域名
JWT_SECRET = "xxx" # 用于生成 jwt 的密钥, jwt 用于给用户登录以及鉴权
BLACK_LIST = "" # 黑名单，用于过滤发件人，逗号分隔
# 是否允许用户创建邮件, 不配置则不允许
ENABLE_USER_CREATE_EMAIL = true
# 允许用户删除邮件, 不配置则不允许
ENABLE_USER_DELETE_EMAIL = true
# 允许自动回复邮件
ENABLE_AUTO_REPLY = false
# 是否启用 webhook
# ENABLE_WEBHOOK = true
# 前端界面页脚文本
# COPYRIGHT = "Dream Hunter"
# 默认发送邮件余额，如果不设置，将为 0
# DEFAULT_SEND_BALANCE = 1
# Turnstile 人机验证配置
# CF_TURNSTILE_SITE_KEY = ""
# CF_TURNSTILE_SECRET_KEY = ""
# dkim config
# DKIM_SELECTOR = "mailchannels" # 参考 DKIM 部分 mailchannels._domainkey 的 mailchannels
# DKIM_PRIVATE_KEY = "" # 参考 DKIM 部分 priv_key.txt 的内容
# telegram bot 最多绑定邮箱数量
# TG_MAX_ACCOUNTS = 5
# 全局转发地址列表，如果不配置则不启用，启用后所有邮件都会转发到列表中的地址
# FORWARD_ADDRESS_LIST = ["xxx@xxx.com"]
```

{% link 本博文转载自,MilaoneChannel,https://www.milaone.com/archives/79.html %}