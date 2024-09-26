---
title: Hexo美化：个性化主题加载页面教程
swiper_index: 10
top_group_index: 10
background: '#fff'
date: 2024-08-20 20:17:49
updated:
tags:
- Hexo
- Hexo美化
- 首页加载
categories:
- Hexo
keywords:
description:
top: 
top_img:
comments:
cover: https://serv.200038.xyz/2024/09/19/895251.webp
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

## 加载动画结语

- 1. Hexo是一款快速、简洁且高效的静态博客框架，它的加载页是展示个人品牌和风格的重要组成部分。通过定制加载页，你可以为你的网站增添个性化的风格，提升用户体验，以及传达特定的信息。

- 2. 本文以本站使用的主题 `anzhiyu` 为例，在本教程中，我们将深入探讨如何更换Hexo加载页，从简单的概念到具体的实施步骤，帮助你轻松地定制属于自己的加载页。

- 3. 加载页的作用：加载页是指在网页加载完成之前显示的页面，通常用于展示品牌标识、加载进度和欢迎信息。它不仅可以提升用户体验，还可以传达网站的特色和个性。

- 5. 加载页设计的考虑因素：在定制加载页时，需要考虑网站的整体风格和目标受众。加载页应该与主题风格一致，同时尽量简洁明了，以保持用户的注意力和耐心。

- 6. 原教程中使用的是`butterfly`主题，本教程将以`anzhiyu`的格式进行更改，在此，感谢**煮雪话河山**和**SNTube Studio**整合并提供了详细的配置教程，他们的博客链接如下：
{% sitegroup %}
{% site 煮雪话河山, url=https://blog.cent1pedee.top/, screenshot=https://img.131213.xyz/file/a4e14d2f60e093235d1e0.jpg, avatar=https://img.cent1pedee.top/img/wechat.jpg , description= %}
{% site SNTube Studio, url=https://satera.cn/, screenshot=https://img.131213.xyz/file/ccba54443f95207c58938.jpg, avatar=https://satera.cn/img/logo.png, description= %}
{% endsitegroup %}

##  首页加载预览效果
{% folding 加载预览效果 %}
![](https://img.cent1pedee.top/img/Loading.gif)
{% endfolding %}

{% link 本博文视频转载自,煮雪话河山,https://blog.cent1pedee.top/posts/576038b4.html %}

## 操作步骤

## 1. 新建文件

- `themes/anzhiyu/layout/includes/loading/`里，新建文件`wizard.pug`，内容如下

```
#loading-box
  .loading-left-bg
  .loading-right-bg
  .wizard-scene
    .wizard-objects
      .wizard-square
      .wizard-circle
      .wizard-triangle
    .wizard
      .wizard-body
      .wizard-right-arm
        .wizard-right-hand
      .wizard-left-arm
        .wizard-left-hand
      .wizard-head
        .wizard-beard
        .wizard-face
          .wizard-adds
        .wizard-hat
          .wizard-hat-of-the-hat
          .wizard-four-point-star.--first
          .wizard-four-point-star.--second
          .wizard-four-point-star.--third

script.
  const preloader = {
    endLoading: () => {
      document.getElementById('loading-box').classList.add("loaded");
    },
    initLoading: () => {
      document.getElementById('loading-box').classList.remove("loaded")
    }
  }
  window.addEventListener('load',()=> { preloader.endLoading() })
  setTimeout(function(){preloader.endLoading();},10000)
``` 

## 2. 修改index.pug   

-  找到`themes/anzhiyu/layout/includes/loading/`的`index.pug`文件，并替换文件内容

``` 
if theme.preloader.source === 1
  include ./fullpage-loading.pug
else if theme.preloader.source === 2
  include ./pace.pug
else if theme.preloader.source === 3
  include ./fullpage-loading.pug
  include ./pace.pug
else 
  include ./wizard.pug
``` 

## 3. 修改loading.styl

- 找到`themes/anzhiyu/source/css/_global/`,拷贝一份loading.styl并重命名为`default.styl`
- 为了便于后续管理,在此目录下新建`load_style`文件夹，将`default.styl`放入`load_style`文件夹中
- 修改`loading.styl`文件，并替换以下内容

```  STYLUS
if hexo-config('preloader.enable')
  if hexo-config('preloader.source') == '1'
    @import './personalized/_load_style/default.styl'
  else if hexo-config('preloader.source') == '2'
    @import './personalized/_load_style/default.styl'
  else if hexo-config('preloader.source') == '3'
    @import './personalized/_load_style/default.styl'
  else
    @import './personalized/_load_style/wizard.styl'
```

## 4. 新建wizard.styl

- 找到`themes/anzhiyu/source/css/_global/load_style/`并新建一个`wizard.styl`，内容如下

``` STYLUS
.loading-bg
  position fixed
  z-index 1000
  width 50%
  height 100%
  background var(--anzhiyu-card-bg)
  
#loading-box
  .loading-left-bg
    @extend .loading-bg
    left 0
  .loading-right-bg
    @extend .loading-bg
    right 0
  &.loaded
    z-index -1000
    .loading-left-bg
      transition all 1.0s
      transform translate(-100%, 0)
    .loading-right-bg
      transition all 1.0s
      transform translate(100%, 0)
      
#loading-box
  position fixed
  z-index 1000
  display -webkit-box
  display flex
  -webkit-box-align center
  align-items center
  -webkit-box-pack center
  justify-content center
  -webkit-box-orient vertical
  -webkit-box-direction normal
  flex-direction column
  flex-wrap wrap
  width 100vw
  height 100vh
  overflow hidden

  &.loaded
    .wizard-scene
      display none

.wizard-scene
  position fixed
  z-index 1001
  display -webkit-box
  display flex

.wizard
  position relative
  width 190px
  height 240px

.wizard-body
  position absolute
  bottom 0
  left 68px
  height 100px
  width 60px
  background #3f64ce
  &::after
    content ""
    position absolute
    bottom 0
    left 20px
    height 100px
    width 60px
    background #3f64ce
    -webkit-transform skewX(14deg)
    transform skewX(14deg)

.wizard-right-arm
  position absolute
  bottom 74px
  left 110px
  height 44px
  width 90px
  background #3f64ce
  border-radius 22px
  -webkit-transform-origin 16px 22px
  transform-origin 16px 22px
  -webkit-transform rotate(70deg)
  transform rotate(70deg)
  -webkit-animation right_arm 10s ease-in-out infinite
  animation right_arm 10s ease-in-out infinite
  .right-hand
    position absolute
    right 8px
    bottom 8px
    width 30px
    height 30px
    border-radius 50%
    background #f1c5b4
    -webkit-transform-origin center center
    transform-origin center center
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)
    -webkit-animation right_hand 10s ease-in-out infinite
    animation right_hand 10s ease-in-out infinite
  .wizard-right-hand
    &::after
      content ""
      position absolute
      right 0px
      top -8px
      width 15px
      height 30px
      border-radius 10px
      background #f1c5b4
      -webkit-transform translateY(16px)
      transform translateY(16px)
      -webkit-animation right_finger 10s ease-in-out infinite
      animation right_finger 10s ease-in-out infinite

.wizard-left-arm
  position absolute
  bottom 74px
  left 26px
  height 44px
  width 70px
  background #3f64ce
  border-bottom-left-radius 8px
  -webkit-transform-origin 60px 26px
  transform-origin 60px 26px
  -webkit-transform rotate(-70deg)
  transform rotate(-70deg)
  -webkit-animation left_arm 10s ease-in-out infinite
  animation left_arm 10s ease-in-out infinite
  .wizard-left-hand
    position absolute
    left -18px
    top 0
    width 18px
    height 30px
    border-top-left-radius 35px
    border-bottom-left-radius 35px
    background #f1c5b4
    &::after
      content ""
      position absolute
      right 0
      top 0
      width 30px
      height 15px
      border-radius 20px
      background #f1c5b4
      -webkit-transform-origin right bottom
      transform-origin right bottom
      -webkit-transform scaleX(0)
      transform scaleX(0)
      -webkit-animation left_finger 10s ease-in-out infinite
      animation left_finger 10s ease-in-out infinite

.wizard-head
  position absolute
  top 0
  left 14px
  width 160px
  height 210px
  -webkit-transform-origin center center
  transform-origin center center
  -webkit-transform rotate(-3deg)
  transform rotate(-3deg)
  -webkit-animation head 10s ease-in-out infinite
  animation head 10s ease-in-out infinite
  .wizard-beard
    position absolute
    bottom 0
    left 38px
    height 106px
    width 80px
    border-bottom-right-radius 55%
    background #ffffff
    &::after
      content ""
      position absolute
      top 16px
      left -10px
      width 40px
      height 20px
      border-radius 20px
      background #ffffff
  .wizard-face
    position absolute
    bottom 76px
    left 38px
    height 30px
    width 60px
    background #f1c5b4
    &::before
      content ""
      position absolute
      top 0px
      left 40px
      width 20px
      height 40px
      border-bottom-right-radius 20px
      border-bottom-left-radius 20px
      background #f1c5b4
    &::after
      content ""
      position absolute
      top 16px
      left -10px
      width 50px
      height 20px
      border-radius 20px
      border-bottom-right-radius 0px
      background #ffffff
    .wizard-adds
      position absolute
      top 0px
      left -10px
      width 40px
      height 20px
      border-radius 20px
      background #f1c5b4
      &::after
        content ""
        position absolute
        top 5px
        left 80px
        width 15px
        height 20px
        border-bottom-right-radius 20px
        border-top-right-radius 20px
        background #f1c5b4
  .wizard-hat
    position absolute
    bottom 106px
    left 0
    width 160px
    height 20px
    border-radius 20px
    background #3f64ce
    &::before
      content ""
      position absolute
      top -70px
      left 50%
      -webkit-transform translatex(-50%)
      transform translatex(-50%)
      width 0
      height 0
      border-style solid
      border-width 0 34px 70px 50px
      border-color transparent transparent #3f64ce transparent
    &::after
      content ""
      position absolute
      top 0
      left 0
      width 160px
      height 20px
      background #3f64ce
      border-radius 20px
    .wizard-hat-of-the-hat
      position absolute
      bottom 78px
      left 79px
      width 0
      height 0
      border-style solid
      border-width 0 25px 25px 19px
      border-color transparent transparent #3f64ce transparent
      &::after
        content ""
        position absolute
        top 6px
        left -4px
        width 35px
        height 10px
        border-radius 10px
        border-bottom-left-radius 0px
        background #3f64ce
        -webkit-transform rotate(40deg)
        transform rotate(40deg)
    .wizard-four-point-star
      position absolute
      width 12px
      height 12px
      &::after
        -webkit-transform rotate(156.66deg) skew(45deg)
        transform rotate(156.66deg) skew(45deg)
      &.--first
        bottom 28px
        left 46px
      &.--second
        bottom 40px
        left 80px
      &.--third
        bottom 15px
        left 108px

.wizard-head .wizard-hat .wizard-four-point-star::after, .wizard-head .wizard-hat .wizard-four-point-star::before
  content ""
  position absolute
  background #ffffff
  display block
  left 0
  width 141.4213%
  top 0
  bottom 0
  border-radius 10%
  -webkit-transform rotate(66.66deg) skewX(45deg)
  transform rotate(66.66deg) skewX(45deg)

.wizard-objects
  position relative
  width 200px
  height 240px

.wizard-square
  position absolute
  bottom -60px
  left -5px
  width 120px
  height 120px
  border-radius 50%
  -webkit-transform rotate(-360deg)
  transform rotate(-360deg)
  -webkit-animation path_square 10s ease-in-out infinite
  animation path_square 10s ease-in-out infinite
  &::after
    content ""
    position absolute
    top 10px
    left 0
    width 50px
    height 50px
    background #9ab3f5

.wizard-circle
  position absolute
  bottom 10px
  left 0
  width 100px
  height 100px
  border-radius 50%
  -webkit-transform rotate(-360deg)
  transform rotate(-360deg)
  -webkit-animation path_circle 10s ease-in-out infinite
  animation path_circle 10s ease-in-out infinite
  &::after
    content ""
    position absolute
    bottom -10px
    left 25px
    width 50px
    height 50px
    border-radius 50%
    background #c56183

.wizard-triangle
  position absolute
  bottom -62px
  left -10px
  width 110px
  height 110px
  border-radius 50%
  -webkit-transform rotate(-360deg)
  transform rotate(-360deg)
  -webkit-animation path_triangle 10s ease-in-out infinite
  animation path_triangle 10s ease-in-out infinite
  &::after
    content ""
    position absolute
    top 0
    right -10px
    width 0
    height 0
    border-style solid
    border-width 0 28px 48px 28px
    border-color transparent transparent #89beb3 transparent


/** 10s animation - 10% = 1s */
@-webkit-keyframes right_arm
  0%
    -webkit-transform rotate(70deg)
    transform rotate(70deg)
  10%
    -webkit-transform rotate(8deg)
    transform rotate(8deg)
  15%
    -webkit-transform rotate(20deg)
    transform rotate(20deg)
  20%
    -webkit-transform rotate(10deg)
    transform rotate(10deg)
  25%
    -webkit-transform rotate(26deg)
    transform rotate(26deg)
  30%
    -webkit-transform rotate(10deg)
    transform rotate(10deg)
  35%
    -webkit-transform rotate(28deg)
    transform rotate(28deg)
  40%
    -webkit-transform rotate(9deg)
    transform rotate(9deg)
  45%
    -webkit-transform rotate(28deg)
    transform rotate(28deg)
  50%
    -webkit-transform rotate(8deg)
    transform rotate(8deg)
  58%
    -webkit-transform rotate(74deg)
    transform rotate(74deg)
  62%
    -webkit-transform rotate(70deg)
    transform rotate(70deg)

@keyframes right_arm
  0%
    -webkit-transform rotate(70deg)
    transform rotate(70deg)
  10%
    -webkit-transform rotate(8deg)
    transform rotate(8deg)
  15%
    -webkit-transform rotate(20deg)
    transform rotate(20deg)
  20%
    -webkit-transform rotate(10deg)
    transform rotate(10deg)
  25%
    -webkit-transform rotate(26deg)
    transform rotate(26deg)
  30%
    -webkit-transform rotate(10deg)
    transform rotate(10deg)
  35%
    -webkit-transform rotate(28deg)
    transform rotate(28deg)
  40%
    -webkit-transform rotate(9deg)
    transform rotate(9deg)
  45%
    -webkit-transform rotate(28deg)
    transform rotate(28deg)
  50%
    -webkit-transform rotate(8deg)
    transform rotate(8deg)
  58%
    -webkit-transform rotate(74deg)
    transform rotate(74deg)
  62%
    -webkit-transform rotate(70deg)
    transform rotate(70deg)

@-webkit-keyframes left_arm
  0%
    -webkit-transform rotate(-70deg)
    transform rotate(-70deg)
  10%
    -webkit-transform rotate(6deg)
    transform rotate(6deg)
  15%
    -webkit-transform rotate(-18deg)
    transform rotate(-18deg)
  20%
    -webkit-transform rotate(5deg)
    transform rotate(5deg)
  25%
    -webkit-transform rotate(-18deg)
    transform rotate(-18deg)
  30%
    -webkit-transform rotate(5deg)
    transform rotate(5deg)
  35%
    -webkit-transform rotate(-17deg)
    transform rotate(-17deg)
  40%
    -webkit-transform rotate(5deg)
    transform rotate(5deg)
  45%
    -webkit-transform rotate(-18deg)
    transform rotate(-18deg)
  50%
    -webkit-transform rotate(6deg)
    transform rotate(6deg)
  58%
    -webkit-transform rotate(-74deg)
    transform rotate(-74deg)
  62%
    -webkit-transform rotate(-70deg)
    transform rotate(-70deg)

@keyframes left_arm
  0%
    -webkit-transform rotate(-70deg)
    transform rotate(-70deg)
  10%
    -webkit-transform rotate(6deg)
    transform rotate(6deg)
  15%
    -webkit-transform rotate(-18deg)
    transform rotate(-18deg)
  20%
    -webkit-transform rotate(5deg)
    transform rotate(5deg)
  25%
    -webkit-transform rotate(-18deg)
    transform rotate(-18deg)
  30%
    -webkit-transform rotate(5deg)
    transform rotate(5deg)
  35%
    -webkit-transform rotate(-17deg)
    transform rotate(-17deg)
  40%
    -webkit-transform rotate(5deg)
    transform rotate(5deg)
  45%
    -webkit-transform rotate(-18deg)
    transform rotate(-18deg)
  50%
    -webkit-transform rotate(6deg)
    transform rotate(6deg)
  58%
    -webkit-transform rotate(-74deg)
    transform rotate(-74deg)
  62%
    -webkit-transform rotate(-70deg)
    transform rotate(-70deg)

@-webkit-keyframes right_hand
  0%
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)
  10%
    -webkit-transform rotate(-20deg)
    transform rotate(-20deg)
  15%
    -webkit-transform rotate(-5deg)
    transform rotate(-5deg)
  20%
    -webkit-transform rotate(-60deg)
    transform rotate(-60deg)
  25%
    -webkit-transform rotate(0deg)
    transform rotate(0deg)
  30%
    -webkit-transform rotate(-60deg)
    transform rotate(-60deg)
  35%
    -webkit-transform rotate(0deg)
    transform rotate(0deg)
  40%
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)
  45%
    -webkit-transform rotate(-60deg)
    transform rotate(-60deg)
  50%
    -webkit-transform rotate(10deg)
    transform rotate(10deg)
  60%
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)


@keyframes right_hand
  0%
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)
  10%
    -webkit-transform rotate(-20deg)
    transform rotate(-20deg)
  15%
    -webkit-transform rotate(-5deg)
    transform rotate(-5deg)
  20%
    -webkit-transform rotate(-60deg)
    transform rotate(-60deg)
  25%
    -webkit-transform rotate(0deg)
    transform rotate(0deg)
  30%
    -webkit-transform rotate(-60deg)
    transform rotate(-60deg)
  35%
    -webkit-transform rotate(0deg)
    transform rotate(0deg)
  40%
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)
  45%
    -webkit-transform rotate(-60deg)
    transform rotate(-60deg)
  50%
    -webkit-transform rotate(10deg)
    transform rotate(10deg)
  60%
    -webkit-transform rotate(-40deg)
    transform rotate(-40deg)

@-webkit-keyframes right_finger
  0%
    -webkit-transform translateY(16px)
    transform translateY(16px)
  10%
    -webkit-transform none
    transform none
  50%
    -webkit-transform none
    transform none
  60%
    -webkit-transform translateY(16px)
    transform translateY(16px)

@keyframes right_finger
  0%
    -webkit-transform translateY(16px)
    transform translateY(16px)
  10%
    -webkit-transform none
    transform none
  50%
    -webkit-transform none
    transform none
  60%
    -webkit-transform translateY(16px)
    transform translateY(16px)

@-webkit-keyframes left_finger
  0%
    -webkit-transform scaleX(0)
    transform scaleX(0)
  10%
    -webkit-transform scaleX(1) rotate(6deg)
    transform scaleX(1) rotate(6deg)
  15%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  20%
    -webkit-transform scaleX(1) rotate(8deg)
    transform scaleX(1) rotate(8deg)
  25%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  30%
    -webkit-transform scaleX(1) rotate(7deg)
    transform scaleX(1) rotate(7deg)
  35%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  40%
    -webkit-transform scaleX(1) rotate(5deg)
    transform scaleX(1) rotate(5deg)
  45%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  50%
    -webkit-transform scaleX(1) rotate(6deg)
    transform scaleX(1) rotate(6deg)
  58%
    -webkit-transform scaleX(0)
    transform scaleX(0)

@keyframes left_finger
  0%
    -webkit-transform scaleX(0)
    transform scaleX(0)
  10%
    -webkit-transform scaleX(1) rotate(6deg)
    transform scaleX(1) rotate(6deg)
  15%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  20%
    -webkit-transform scaleX(1) rotate(8deg)
    transform scaleX(1) rotate(8deg)
  25%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  30%
    -webkit-transform scaleX(1) rotate(7deg)
    transform scaleX(1) rotate(7deg)
  35%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  40%
    -webkit-transform scaleX(1) rotate(5deg)
    transform scaleX(1) rotate(5deg)
  45%
    -webkit-transform scaleX(1) rotate(0deg)
    transform scaleX(1) rotate(0deg)
  50%
    -webkit-transform scaleX(1) rotate(6deg)
    transform scaleX(1) rotate(6deg)
  58%
    -webkit-transform scaleX(0)
    transform scaleX(0)

@-webkit-keyframes head
  0%
    -webkit-transform rotate(-3deg)
    transform rotate(-3deg)
  10%
    -webkit-transform translatex(10px) rotate(7deg)
    transform translatex(10px) rotate(7deg)
  50%
    -webkit-transform translatex(0px) rotate(0deg)
    transform translatex(0px) rotate(0deg)
  56%
    -webkit-transform rotate(-3deg)
    transform rotate(-3deg)

@keyframes head
  0%
    -webkit-transform rotate(-3deg)
    transform rotate(-3deg)
  10%
    -webkit-transform translatex(10px) rotate(7deg)
    transform translatex(10px) rotate(7deg)
  50%
    -webkit-transform translatex(0px) rotate(0deg)
    transform translatex(0px) rotate(0deg)
  56%
    -webkit-transform rotate(-3deg)
    transform rotate(-3deg)
/** 10s animation - 10% = 1s */
@-webkit-keyframes path_circle
  0%
    -webkit-transform translateY(0)
    transform translateY(0)
  10%
    -webkit-transform translateY(-100px) rotate(-5deg)
    transform translateY(-100px) rotate(-5deg)
  55%
    -webkit-transform translateY(-100px) rotate(-360deg)
    transform translateY(-100px) rotate(-360deg)
  58%
    -webkit-transform translateY(-100px) rotate(-360deg)
    transform translateY(-100px) rotate(-360deg)
  63%
    -webkit-transform rotate(-360deg)
    transform rotate(-360deg)

@keyframes path_circle
  0%
    -webkit-transform translateY(0)
    transform translateY(0)
  10%
    -webkit-transform translateY(-100px) rotate(-5deg)
    transform translateY(-100px) rotate(-5deg)
  55%
    -webkit-transform translateY(-100px) rotate(-360deg)
    transform translateY(-100px) rotate(-360deg)
  58%
    -webkit-transform translateY(-100px) rotate(-360deg)
    transform translateY(-100px) rotate(-360deg)
  63%
    -webkit-transform rotate(-360deg)
    transform rotate(-360deg)

@-webkit-keyframes path_square
  0%
    -webkit-transform translateY(0)
    transform translateY(0)
  10%
    -webkit-transform translateY(-155px) translatex(-15px) rotate(10deg)
    transform translateY(-155px) translatex(-15px) rotate(10deg)
  55%
    -webkit-transform translateY(-155px) translatex(-15px) rotate(-350deg)
    transform translateY(-155px) translatex(-15px) rotate(-350deg)
  57%
    -webkit-transform translateY(-155px) translatex(-15px) rotate(-350deg)
    transform translateY(-155px) translatex(-15px) rotate(-350deg)
  63%
    -webkit-transform rotate(-360deg)
    transform rotate(-360deg)

@keyframes path_square
  0%
    -webkit-transform translateY(0)
    transform translateY(0)
  10%
    -webkit-transform translateY(-155px) translatex(-15px) rotate(10deg)
    transform translateY(-155px) translatex(-15px) rotate(10deg)
  55%
    -webkit-transform translateY(-155px) translatex(-15px) rotate(-350deg)
    transform translateY(-155px) translatex(-15px) rotate(-350deg)
  57%
    -webkit-transform translateY(-155px) translatex(-15px) rotate(-350deg)
    transform translateY(-155px) translatex(-15px) rotate(-350deg)
  63%
    -webkit-transform rotate(-360deg)
    transform rotate(-360deg)

@-webkit-keyframes path_triangle
  0%
    -webkit-transform translateY(0)
    transform translateY(0)
  10%
    -webkit-transform translateY(-172px) translatex(10px) rotate(-10deg)
    transform translateY(-172px) translatex(10px) rotate(-10deg)
  55%
    -webkit-transform translateY(-172px) translatex(10px) rotate(-365deg)
    transform translateY(-172px) translatex(10px) rotate(-365deg)
  58%
    -webkit-transform translateY(-172px) translatex(10px) rotate(-365deg)
    transform translateY(-172px) translatex(10px) rotate(-365deg)
  63%
    -webkit-transform rotate(-360deg)
    transform rotate(-360deg)

@keyframes path_triangle
  0%
    -webkit-transform translateY(0)
    transform translateY(0)
  10%
    -webkit-transform translateY(-172px) translatex(10px) rotate(-10deg)
    transform translateY(-172px) translatex(10px) rotate(-10deg)
  55%
    -webkit-transform translateY(-172px) translatex(10px) rotate(-365deg)
    transform translateY(-172px) translatex(10px) rotate(-365deg)
  58%
    -webkit-transform translateY(-172px) translatex(10px) rotate(-365deg)
    transform translateY(-172px) translatex(10px) rotate(-365deg)
  63%
    -webkit-transform rotate(-360deg)
    transform rotate(-360deg)
```

## 5. 修改主题配置文件

- 在主题配置文件中找到`preloader`,修改如下

```
# Loading Animation (加载动画)
preloader:
  enable: true
  # source
  # 1. fullpage-loading
  # 2. pace (progress bar)
  # 3. all
  # 4. wizard(custom)
  source: 4
  # pace theme (see https://codebyzach.github.io/pace/)
  pace_css_url:
  avatar: xxx # 自定加载动画义头像
```

### 6. 这个时候，如果你的文件配置正确，可以执行Hexo的三连命令来查看效果了！

``` SHELL
hexo clean; hexo g; hexo s
```
### 教程参考资料
{% link 【Hexo博客】自定义Butterfly主题 Loading 加载动画,百里飞洋,https://blog.meta-code.top/2022/06/18/2022-73/ %}
{% link 自定义加载动画魔改方案,Akilarの糖果屋,https://akilar.top/posts/3d221bf2/ %}
