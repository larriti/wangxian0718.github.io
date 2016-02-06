---
layout:post
---
# Archlinux install chromium pepper flash player
---
最近一直被chromium浏览器的flash player插件困扰，之前也安装了试了好几种方案都没有成功过。现在我就把我以前试过的几种方法说下，方便大家参考。

一、通过`pacman` 安装 `adobe flash player` 发现这个flash player是firefox的插件，在谷歌上根本没用，于是放弃此方案。

二、在网上查询之后发现谷歌不支持`adobe flash player`插件，谷歌浏览器支持的插件是`pepper flash player` 于是进`archlinux wiki` 发现有 `chromium-pepper-flash` 于是用yaourt进行安装，于是由遇到问题，然而下载都下载不下来，所以这种方法也失败。

三、在网上查了一下还是没有解决方法。所以选择放弃，因为发现外国网站现在大部分都是用`HTML5`,不再使用`flash player`了。也就放弃了。

---

最近闲下来了，发现国内有很多视频网站都还是用flash player，无奈只能再想办法一定要解决下这个问题，于是在网上搜索了各种方法，无意间在一篇博客[http://blog.sina.com.cn/s/blog_858820890102v63w.html](http://blog.sina.com.cn/s/blog_858820890102v63w.html)上看到很像我这种情况，于是有感而发，因为他博客是2014年的想必现在用不了他的方法，但是我看到他最后一种方法思路是对的。就是既然`chrome`浏览器内置`flash player`插件，那我们就可以从包里面找到`pepper flash player`插件，于是我在网上下载chrome，记得要下载`.rpm`的包，根据自己电脑选择32位还是64位--下载地址: [chrome download](https://www.google.com/chrome/browser/desktop/)

下载好了，将`.rpm`包解压找到 `opt/google/chrome/` 中的 `PepperFlash` 文件夹。我发现这个文件夹中只有一个 `libpepflashplayer.so` 就想这是一个动态库文件，那我只要把这个文件放到 `/usr/lib`下面就行了吧，于是动手就做，发现还是无果。觉得奇怪之后还是利用博客中方法说是要改什么文件，发现并没有所提到的 `/etc/chromium-browser/default` 这个文件，我只发现和`libpepflashplayer.so` 一起的只有 `manifest.json` 这个文件。之后脑袋一灵光就把整个 `PepperFlash` 文件夹放到 `/usr/lib/` 下面，之后发现终于可以了。
来一张效果图：

![效果图](/images/screenshot.png)
