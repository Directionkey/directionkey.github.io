---
title: 分辨率，设计开发中的单位
date: 2021-09-27
tags:
  - 单位
categories:
  - Design
---

<h3>就，很烦！</h3>
一大堆什么px，pt，dp，rpx，dpi，ppi乱七八糟的，我真是看麻了，秉着长痛不如短痛的原则，结果看了看了一堆，写了一大堆天书，还是啰里八嗦的。

<h3>DPI and PPI</h3>

作为设计者，只要清楚 web 图像靠像素（的宽高），不靠 DPI\PPI，您甭管 PPI、DPI 怎么设置，a x b 的像素尺寸是雷打不动的！

:unicorn:
DPI,英文 Dots Per Inch(每英寸的点数)，打印机知道吧，描述这玩意的性能的，用来打印图像，与数字图像无关！所以某某显示器有几千几百 DPI，让他滚蛋，你家显示器里有墨水！可是这类现象普遍存在，厂商往往混淆了二者的概念，其实指的是 PPI，自己转换下就好。

另外在 ps 中新建画布可以设置 PPI，affinityDesigner 中却又是设置 DPI，我认为在这些作图软件中 PPI=DPI 都是作为图片的一个`输出属性`，告知打印机我要按多少 DPI 打印。

:unicorn:
PPI,英文 Pixel Per Inch(每英寸容纳的像素)。

1. 显示器 PPI 就是由一定数量的发光点构成，光电越多越密集，那么显示器给人的颗粒感就越少，甚至人眼已经感受不出了。但终归一张屏幕是根据出产设定容纳指定数量的发光点（像素），所以就显示器来说像素是一个物理单位。

所以同样是 1920x1080 尺寸的手机和电脑显示屏，哪个看起来更清晰呢？

当然是手机了，小小的身子里塞了辣么多的发光点。

IOS 规定 163dpi 为 1 倍图（以最早开发的手机为准，这里的 dpi 与打印的 dpi 性质不同，指的是抽象的屏幕的坐标单位，也是开发基准）

Android 规定 160dpi 为 1 倍图

举个例子，iphone6，说的就是你，平常开发看你看的最多！它的物理分辨率是 `750*1334`，也就是一个屏幕里有 `750 个像素点(光点)*1334 个像素点(光点)`，
像素密度为 326PPI，公式为`PPI=√（X^2+Y^2）/ Z （X：长度像素数；Y：宽度像素数；Z：屏幕大小(英寸)）`或者是`PPI = 屏幕横向像素尺寸/屏幕横向物理尺寸（英寸）`。

这里补充一下对应的逻辑分辨率的理解，它是软件所能达到的分辨率，按照缩放因子（DPR）的倍数放大便是物理分辨率，一个 app 页面能展示多少内容是要看它的逻辑分辨率的大小，而不是物理分辨率，物理分辨率决定的是精细程度。

作为开发一般只需要关心逻辑分辨率的尺寸就完事。当然也有特殊情况，例如 pm 要求一条 1px 高度的分割线。那就判断缩放因子 DPR， 而后 transform：scale(X)就完事。

pt: ios 开发单位，非绝对长度，1pt = 1 / DPI

dp: 也称 dip，Density-independent pixel, 是安卓开发用的长度单位，1dp 表示在屏幕像素点密度为 160PPI 时 1px 长度。

那么同样安卓类型的手机开发的长度单位 dp 就可以以此计算了 `1dp=(屏幕 PPI/160)px`，而字体单位 sp 与 dp 类似，通常 1sp=1dp，字体尺寸较大时，1sp>1dp。

2. 图像 PPI，指数字图像中的像素密度。这和打印有关，300PPI 往往是行业标准。但在 web 中 72PPI 和 300PPI 没有任何区别，因为使用者的显示器的像素密度是固定的。72ppi 的图片你把它改成 300ppi，这只会增大图像的体积以及像素长宽度，通过差值计算出的像素并不会提高图片的清晰度。

至于你会经常看到什么 72PPI，这是一种单纯的遵循惯例。

[通俗易懂解释二者定义-暮成雪](https://www.zhihu.com/question/40506180)

[DPI 与 PPI 的差异 很关键](https://99designs.hk/blog/tips/ppi-vs-dpi-whats-the-difference/)

[网页设计是否必须将图像保持在 72 dpi？](https://graphicdesign.stackexchange.com/questions/13777/is-it-mandatory-to-keep-images-at-72-dpi-for-web-design)

[IOS](https://www.jianshu.com/p/551bc62f1c8d)