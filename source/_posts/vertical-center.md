title: 不定高元素实现垂直居中
date: 2015-06-19 16:10:16
tags:
---
有时候我们会遇到图片垂直居中的情况，更准确来说应该是在一个元素内适配图片。而且这种垂直居中图片的高度也是不确定的，这就给页面布局带来了一定的挑战。
###整体效果
---
首先，让我们先来看一下整体的效果：
<iframe src="http://s.codepen.io/wilsonup/debug/zGEwwJ?" width="100%" height="300px" frameborder="0"></iframe><!--more-->
###完整代码
---
html
```html
<div class="g-wrap">
  <img src="http://www.wilsonup.xyz/img/toCode/yy.jpg" alt="" />
</div>
```

css
```css
.g-wrap {
  display: table-cell;
  width: 250px;
  height: 250px;
  text-align: center;
  background-color: #ccc;
  vertical-align: middle;
}
img {
  vertical-align: middle;
}
```

###后续
----
当然，这不仅仅局限于图片，文本也是OK的。
<iframe src="http://s.codepen.io/wilsonup/debug/EjwmbO?" width="100%" height="300px" frameborder="0"></iframe><!--more-->
###说明
---
本实例在IE7+,chrome,FireFox测试通过。