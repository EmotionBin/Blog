草稿
1.px + pt(1.逻辑像素 2.物理像素)
2.rem + rpx (小程序的rpx单位就是（物理像素/逻辑像素） 1rpx = 375/750=0.5px)
3.移动端适配解决方案

参考:

1.https://blog.csdn.net/huangpb123/article/details/89323266
2.https://www.jianshu.com/p/039201217b15
3.https://www.cnblogs.com/xiaocaiyuxiaoniao/p/10156680.html
4.https://www.jianshu.com/p/0540d2623e52

# 关于移动端适配

这里会讲解一些关于移动端的知识，比如逻辑像素、物理像素等，这些也是我们前端攻城狮所必备的知识  

----

## 物理像素与逻辑像素

首先要来了解两个重要的概念，就是物理像素与逻辑像素  

**物理像素:**也叫物理分辨率，设备屏幕实际拥有的像素点，比如 iPhone 6 的屏幕在宽度方向有 750 个像素点，高度方向有 1334 个像素点，所以 iPhone 6 总共有 750 * 1334 个物理像素点，它的物理分辨率是 750 * 1334，在同一个设备上，它的物理像素是固定的，这是厂商在出厂时就设置好了的  

**逻辑像素:**也叫显示屏分辨率，比如 iPhone 6 的逻辑像素是 375 * 667，可以理解为反映在 CSS / JS 代码里的像素点数  

这里再来一个概念，**设备像素比(Device Pixel Ratio,简称 DPR)**，它是指一个设备的物理像素与逻辑像素之比  

一般情况下，电脑显示屏的设备像素比是 1，也就是说它的逻辑像素和物理像素是相等的，CSS 里写个 1px，屏幕就给你渲染成 1 个实际的像素点  

但是在手机屏幕下，设备像素比不一定是 1，比如 Retina 屏幕，比如 iPhone 6 的物理像素是 750 * 1334，逻辑像素是 375 * 667，设备像素比是 2，也就是 1 个逻辑像素点用 4(2 X 2) 个实际像素点来渲染  

看到这里你可能一脸懵逼，物理像素、逻辑像素、设备像素比，what?????，没关系，下面会慢慢讲解  

![BHdxYR.png](https://s1.ax1x.com/2020/11/09/BHdxYR.png)  

看上面这张图，以 iPhone 6 为例子，它的物理像素是 750 * 1334，也就是横向 750 个像素点，纵向 1334 个像素点，图中每一个**白色**小方块表示一个像素点  

[![BHBpqO.png](https://s1.ax1x.com/2020/11/09/BHBpqO.png)](https://imgchr.com/i/BHBpqO)

再来看这张图，还是以 iPhone 6 为例子，它的逻辑像素是 375 * 667，也就是横向 375 个像素点，纵向 667 个像素点，图中每一个**红色**小方块表示一个像素点  

最后来综合看这两张图，细心观察会发现，**红色小方块的边长是白色小方块的边长的 2 倍，一个红色小方块刚好由 4 个白色小方块组成**，看下图  

![BHXfHK.png](https://s1.ax1x.com/2020/11/09/BHXfHK.png)  

所以在 iPhone 6 中，逻辑像素(CSS 像素) 1px 等于物理像素(设备实际像素点的个数) 2px，设备像素比(DPR) 为 2，2 个设备实际的像素点表示 1 个 CSS 像素点  

下面我会用代码来证明这个结论  

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style type="text/css">
    #box1 { width: 375px; height: 667px; background: blueviolet; }
  </style>
</head>
<body>
  <div id="box1">
  </div>
</body>
</html>
```

![BHvQJg.png](https://s1.ax1x.com/2020/11/09/BHvQJg.png)  

通过这个图可以看到，一个宽 375px，高 667px 的 div 正好占满了整个屏幕，验证了 iPhone 6 的逻辑像素就是 375 * 667  

**如何获取设备的物理像素与逻辑像素**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>显示手机分辨率</title>
    <script>
      var width = window.screen.width;
      var height = window.screen.height;
      var dpr = window.devicePixelRatio;
      document.write("物理分辨率-宽度：" + width + "<br/>");
      document.write("物理分辨率-高度：" + height + "<br/><br/>");
      document.write("逻辑分辨率-宽度：" + width * dpr + "<br/>");
      document.write("逻辑分辨率-高度：" + height * dpr);
    </script>
  </head>
  <body></body>
</html>
```






