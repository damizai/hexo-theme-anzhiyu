---
title: hexo-history-calendar 那年今日侧边栏卡片
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-08-24 18:05:28
updated:
tags:
- 那年今日
- Hexo
- 侧边栏卡片
categories:
- Hexo
keywords:
description:
top:
top_img:
comments:
cover: https://serv.200038.xyz/2024/09/19/784056.webp
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

 -  hexo-history-calendar 那年今日侧边栏卡片
---

{% note blue 'anzhiyufont anzhiyu-icon-bullhorn' simple %}
显示效果看侧边栏 ,此功能参考自[小冰博客](https://zfe.space/post/hexo-history-calendar.html),记录方便以后学习。
{% endnote %}

## 1. NPM 插件安装的部署方法：

###  注意，一定要加 `--save`，不然本地预览的时候可能不会显示

``` SHELL
npm i hexo-history-calendar --save

# 或者

cnpm i hexo-history-calendar --save
```

## 2. 新增网站根目录`_config` 配置项 (不是主题的)：

``` YAML
history_calendar:
  priority: 4
  enable: true
  enable_page: all
  layout:
    type: class
    name: sticky_layout
    index: 0
  temple_html: '<div class="card-widget card-history"><div class="card-content"><div class="item-headline"><i class="fas fa-clock fa-spin"></i><span>那年今日</span></div><div id="history-baidu" style="height: 100px;overflow: hidden"><div class="history_swiper-container" id="history-container" style="width: 100%;height: 100%"><div class="swiper-wrapper" id="history_container_wrapper" style="height:20px"></div></div></div></div>'
```

## 3. enable

- 参数：true/false
- 含义：是否开启插件

## 4. enable_page

- 参数：all
- 含义：路由地址，all 代表全局开启。如 / 代表主页。

## 5. priority

- 参数：1
- 含义：插件的叠放顺序，数字越大，叠放约靠前。

``` YAML
history_calendar:
  enable: true
  priority: 4 # 这里是参数
```

## 6. layout

1. 参数：type; （class&id）
2. 参数：name;
3. 参数：index；（数字）
4. 含义：如果说 history_calendar 是一幅画，那么这个 layout 就是指定了哪面墙来挂画
  -  而在 HTML 的是世界里有两种墙分别 type 为 id 和 class。
  -  其中在定义 class 的时候会出现多个 class 的情况，这时就需要使用 index，确定是哪一个。
  -  最后墙的名字即是 name;

``` HTML
<div desc="我是墙" id="recent-posts">
  <!-- id=>type  recent-posts=>name    -->
  <div desc="我是画框">
    <div desc="我是纸">
      <!--这里通过js挂载history_calendar，也就是画画-->
    </div>
  </div>
</div>
```

## 7. temple_html

- 参数：html 模板字段
- 含义：包含挂载容器

``` XML
<div class="card-widget card-history"> <!-- 挂载容器 -->
  <div class="card-content">
    <div class="item-headline">
      <i class="fas fa-clock fa-spin"></i>
      <span>那年今日</span>
    </div>
  <div id="history-baidu" style="height: 100px;overflow: hidden"> <!-- 挂载器 -->
    <div class="history_swiper-container" id="history-container" style="width: 100%;height: 100%">
          <div class="swiper-wrapper" id="history_container_wrapper" style="height:20px"></div>
    </div>
  </div>
</div>
```

### 8. 这个时候，如果你的文件配置正确，可以执行Hexo的三连命令来查看效果了！

``` SHELL
hexo clean; hexo g; hexo s
```