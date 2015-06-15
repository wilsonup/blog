title: 3d方块旋转
date: 2015-05-29 20:14:07
tags:
---
随着css3的普及，普通的css hover效果已经不能满足我们追求极致的欲望。闲着无聊，写了一个hover的3d旋转效果，看似简单，但还是遇到了几个坑。（PS：T_T 我只想说，在哪个地方摔倒，我就要证明那个地方有坑）
###整体效果
----
首先，让我们先来看一下整体的效果：
<iframe src="http://s.codepen.io/wilsonup/debug/VLPVNo?" width="100%" frameborder="0"></iframe>
###基础知识
----
想要3D效果，那么必须要有一个3D场景。可以给需要3D效果元素的最外层加上:<!--more-->
```css
    perspective: 5000px;
```
**注意：**这里忽略浏览器前缀，请自行脑补，下同


那么问题来了，对于`perspective`我们应该怎么理解呢？[Showcase Board](http://fangyexu.com/tool-CSS3Inspector.html)可以解除你的疑惑,这里就不多说此概念了，这是我见过对`perspective`最好的解释，没有之一。

此外，给需要进行3D变换的元素加上：
```css
transform-style: preserve-3d;
```
现在，你已经打好地基了，可以开始你的3D之路。
###简单思路
----
1.用两张图片搭建出一个立体的框架。前面的图片很简单，直接绝对定位就搞定，底部的图片则需要旋转。旋转我知道的有两种做法，第一种需要`transform-origin`，第二种则不需要。本文采用第二种做法，代码如下：
```css
.bottomPic{
   transform: rotateX(-91deg) translateZ(40px);
}
```
这里有一下几点需要注意：
1.`rotateX`和`translateZ`的顺序不能颠倒，其实道理很简单，你必须先旋转（相对于中心点），然后再移动，而移动的方向是根据你旋转后为基点的。
2.当旋转角度超过90度时，要加上`backface-visibility: hidden;`，不然用户会看到元素的背部，如下图：
![没有去除元素背部效果](/img/3dRotate/backface.png)
此外，如果你在做动画效果时，发现元素会闪烁，大多数情况下加上`backface-visibility: hidden;`即可解决。
###完整代码
----
html:
```html
 <div class="g-item">
        <div class="innerItem">
            <div class="frontPic">
                <a href="#">
                    <img src="img/front.png" alt="">
                </a>
            </div>
            <div class="bottomPic">
                <a href="#">
                    <img src="img/bottom.jpg" alt="">
                </a>
            </div>
        </div>
    </div>
```
css:
```css
.g-item {
    width: 254px;
    height: 85px;
    background: url(img/rbg.png) center top no-repeat;
    padding: 8px;
    -webkit-perspective: 5000px;
    perspective: 5000px;
}

.g-item .innerItem {
    width: 254px;
    height: 85px;
    transition: -webkit-transform .5s;
    transition: transform .5s;
    -webkit-transform-style: preserve-3d;
    transform-style: preserve-3d;
    position: relative;
}

.g-item .innerItem .frontPic {
    position: absolute;
    left: 0;
    top: 0;
  -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-transform: translateZ(42px);
    transform: translateZ(42px);
    z-index: 1;
}

.g-item .innerItem .bottomPic {
    position: absolute;
    left: 0;
    top: 0;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-transform: rotateX(-91deg) translateZ(40px);
    transform: rotateX(-91deg) translateZ(40px);
}

.g-item .innerItem:hover {
    -webkit-transform: translateZ(-42px) rotateX(91deg);
    transform: translateZ(-42px) rotateX(91deg);
}
```
###文章推荐
----
[好吧，CSS3 3D transform变换，不过如此！](http://www.zhangxinxu.com/wordpress/2012/09/css3-3d-transform-perspective-animate-transition/)