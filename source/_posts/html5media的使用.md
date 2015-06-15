title: html5media的使用
date: 2015-05-26 20:53:43
tags:
---
###问题产生
----------
今天接到一个需求:在所有主流浏览器(包括IE7)中播放mp4视频。根据张先生的一篇[文章](http://www.zhangxinxu.com/wordpress/2010/03/%E8%AE%A9%E6%89%80%E6%9C%89%E6%B5%8F%E8%A7%88%E5%99%A8%E6%94%AF%E6%8C%81html5-video%E8%A7%86%E9%A2%91%E6%A0%87%E7%AD%BE/)很快就搞定了。但在上传静态资源的时候遇到一个神奇的现象：本地引用[线上](http://api.html5media.info/1.1.8/html5media.min.js)的js是正常的，但是拷贝到本地的时候IE7/8就一直出不来了。html5media网上的教程很多，但是这个坑找了很久都没找到。 <!--more-->
###解决方法
----------
html5media的做法是当浏览器不支持video标签的时候讲视频转成flash格式来播放。在html5media中找到以下片段：
```
i.flowplayerSwf=v+"flowplayer.swf",
i.flowplayerAudioSwf=v+"flowplayer.audio.swf",
i.flowplayerControlsSwf=v+"flowplayer.controls.swf",
i.expressInstallSwf=v+"expressInstall.swf";
```
所以必须把html5media.js和你需要用到的播放器放在**同一个**目录下面，如下图
![目录结构](/img/html5media.png)
至此，问题已经解决。其实一早就该想到这个原因了，日了狗了。而偏偏在IE下面找不到这个文件也不会报错，然后1个小时就这样没了。
如果你对样式有要求可以使用[vedio.js](http://www.videojs.com/),这也是个非常好的插件。
>今天注定是悲剧的日子，误用发布器，把测试的东西直接就发到了线上。然后就引起了一场风波，自己也被吓了两跳，不过还好遇到好的大佬（谁没个犯错的时候呢····）。经过这次教训，以后严格把关好每一步，杜绝再现此糗事！