# Facebook-loading-gif-CSS-animation
How to implement Facebook animation using CSS

本文作者：George Phillips
翻译自：[原文地址](http://cloudcannon.com/deconstructions/2014/11/15/facebook-content-placeholder-deconstruction.html)

Facebook首页，鼠标滚动到底，实时加载新动态，加载过程会是下面的动态效果。这种效果不是gif图，而是CSS动画实现。下面剖析如何实现。

![preview.gif](http://upload-images.jianshu.io/upload_images/2058960-650fc408a8cd2d73.gif?imageMogr2/auto-orient/strip)
### HTML
```HTML
<div class="timeline-wrapper">
    <div class="timeline-item">
        <div class="animated-background">
            <div class="background-masker header-top"></div>
            <div class="background-masker header-left"></div>
            <div class="background-masker header-right"></div>
            <div class="background-masker header-bottom"></div>
            <div class="background-masker subheader-left"></div>
            <div class="background-masker subheader-right"></div>
            <div class="background-masker subheader-bottom"></div>
            <div class="background-masker content-top"></div>
            <div class="background-masker content-first-end"></div>
            <div class="background-masker content-second-line"></div>
            <div class="background-masker content-second-end"></div>
            <div class="background-masker content-third-line"></div>
            <div class="background-masker content-third-end"></div>
        </div>
    </div>
</div>
```
### 外部容器
最外面是包裹这段动画的居中div容器。
![](http://upload-images.jianshu.io/upload_images/2058960-42532bda5021b2c3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
``` CSS
.timeline-item {
    background: #fff;
    border: 1px solid;
    border-color: #e5e6e9 #dfe0e4 #d0d1d5;
    border-radius: 3px;
    padding: 12px;

    margin: 0 auto;
    max-width: 472px;
    min-height: 200px;
}
```
### 动态背景
接下来实现动态背景效果，使用CSS animation和背景渐变linear-gradient。

![](http://upload-images.jianshu.io/upload_images/2058960-e75b8f85aa95035c.gif?imageMogr2/auto-orient/strip)
```CSS
@keyframes placeHolderShimmer{
    0%{
        background-position: -468px 0
    }
    100%{
        background-position: 468px 0
    }
}

.animated-background {
    animation-duration: 1s;
    animation-fill-mode: forwards;
    animation-iteration-count: infinite;
    animation-name: placeHolderShimmer;
    animation-timing-function: linear;
    background: #f6f7f8;
    background: linear-gradient(to right, #eeeeee 8%, #dddddd 18%, #eeeeee 33%);
    background-size: 800px 104px;
    height: 96px;
    position: relative;
}
```
### 添加大量阻挡住背景的div
到现在效果看起来，就像一个巨大的进度条。我们添加大量的div，用来遮挡下面的背景动态效果。

![](http://upload-images.jianshu.io/upload_images/2058960-6f533e174d81f67a.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
.background-masker {
    background: #fff;
    position: absolute;
}

/* Every thing below this is just positioning */

.background-masker.header-top,
.background-masker.header-bottom,
.background-masker.subheader-bottom {
    top: 0;
    left: 40px;
    right: 0;
    height: 10px;
}

.background-masker.header-left,
.background-masker.subheader-left,
.background-masker.header-right,
.background-masker.subheader-right {
    top: 10px;
    left: 40px;
    height: 8px;
    width: 10px;
}

.background-masker.header-bottom {
    top: 18px;
    height: 6px;
}

.background-masker.subheader-left,
.background-masker.subheader-right {
    top: 24px;
    height: 6px;
}


.background-masker.header-right,
.background-masker.subheader-right {
    width: auto;
    left: 300px;
    right: 0;
}

.background-masker.subheader-right {
    left: 230px;
}

.background-masker.subheader-bottom {
    top: 30px;
    height: 10px;
}

.background-masker.content-top,
.background-masker.content-second-line,
.background-masker.content-third-line,
.background-masker.content-second-end,
.background-masker.content-third-end,
.background-masker.content-first-end {
    top: 40px;
    left: 0;
    right: 0;
    height: 6px;
}

.background-masker.content-top {
    height:20px;
}

.background-masker.content-first-end,
.background-masker.content-second-end,
.background-masker.content-third-end{
    width: auto;
    left: 380px;
    right: 0;
    top: 60px;
    height: 8px;
}

.background-masker.content-second-line  {
    top: 68px;
}

.background-masker.content-second-end {
    left: 420px;
    top: 74px;
}

.background-masker.content-third-line {
    top: 82px;
}

.background-masker.content-third-end {
    left: 300px;
    top: 88px;
}
```
### 结语
当网站的数据异步加载时，给与用户加载的指示，让人心理上觉得等待时间变短，更倾向于继续留在网页上浏览。
你可以点击链接在线查看效果：[live demo](https://wuyanwuyan.github.io/facebook_css_animation/)。
