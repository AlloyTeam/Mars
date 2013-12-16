# CSS动画属性性能

* CSS动画属性会触发整个页面的重排relayout、重绘repaint、重组recomposite
* Paint通常是其中最花费性能的，尽可能避免使用触发paint的CSS动画属性，这也是为什么我们推荐使用`webkit-transform: translateX(2em)`的方案代替使用`left: 3em`，因为`left`会额外触发layout与paint，而`webkit-transform`只触发整个页面composite

![CSS Property Animation on the Web](https://f.cloud.github.com/assets/677114/1752383/1f8c5e8e-661c-11e3-9725-306f7e5c73f5.png)


## 参考
* [#perfmatters: 60fps layout and rendering](https://docs.google.com/presentation/d/1CH8ifryioHDLT1Oryyy8amusUmq2FytpCPCpk0G3E4o/edit#slide=id.p)
