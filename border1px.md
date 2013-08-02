使用border-image实现类似iOS7的1px底边
===================

iOS7已经发布有一段时间，扁平化设计风格有很多值得称赞的地方，其中有很多设计细节都是值得研究的。

首先，来看下面iOS设置的截图中的border：

<img width="320" src="http://maxzhang.github.com/articles/images/ios7_settings.png" />

从上面的截图可以看到iOS7的设计是非常精细的，border是一根非常细的线。这篇文章将说明如何使用border-image实现iOS7的border效果。

在看下面的内容之前，需要先了解devicePixelRatio和border-image，不熟悉的同学请自行脑补：

* [设备像素比devicePixelRatio简单介绍](http://www.zhangxinxu.com/wordpress/2012/08/window-devicepixelratio/)
* [CSS3 border-image详解、应用及jQuery插件](http://www.zhangxinxu.com/wordpress/?p=518)


### `border`属性实现效果

我们在实现border时通常都是使用`border`属性，如下：
```
.border-1px {
    border-width: 1px 0;
    border-style: solid;
    border-color: #333;
}
```

显示效果对比：

![border对比效果](http://maxzhang.github.com/articles/images/border_compare.png)

上面这张图片可以看到，在手机上`border`无法达到我们想要的效果。这是因为devicePixelRatio特性导致，iPhone的devicePixelRatio==2，而`border-width: 1px`描述的是设备独立像素，所以，border被放大到物理像素2px显示，在iPhone上就显得较粗。

### 使用`border-image`属性实现物理1px

通常手机端的页面设计稿都是放大一倍的，如：为适应iphone retina，设计稿会设计成640*960的分辨率，图片按照2倍大小切出来，在手机端看着就不会虚化，非常清晰。

同样，在使用`border-image`时，将border设计为物理1px，如下：

![border image 放大](https://raw.github.com/maxzhang/maxzhang.github.com/master/articles/images/border_zoom.png)

样式设置：

```
.border-image-1px {
    border-width: 1px 0px;
    -webkit-border-image: url("border.png") 2 0 stretch;
    border-image: url("border.png") 2 0 stretch;
}
```

显示效果对比：

![border image 对比效果](http://maxzhang.github.com/articles/images/border_image_compare.png)

这里在手机上的效果和iOS7已经非常接近了。

样例：http://maxzhang.github.com/examples/border1px/index.html

### 结束语

博客迁移到GitHub的第一篇文章，Hello GitHub!
