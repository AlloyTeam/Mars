iOS Issues
===

* [Position fixed & scrolling on iOS](http://remysharp.com/2012/05/24/issues-with-position-fixed-scrolling-on-ios/)
* `iOS 5.0-` 的`Date`构造函数不支持规范标准中定义的`YYYY-MM-DD`格式，如 `new Date('2013-11-11')` 是 `Invalid Date`, 但支持`YYYY/MM/DD`格式，可用 `new Date('2013/11/11')` 
* IOS（7.1.1版本）使用webapp模式时滚动元素无法滚动到头，解决办法是设置 `<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />` 让APP占用整个屏幕空间布局。参考[官方文档](https://developer.apple.com/library/safari/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)
* IOS（7.1.1版本）滚动元素中设定其中某个元素的 `innerHTML` 属性一定机率导致画面闪动（估计是触发了重绘），解决办法是设置文字时使用`textContent`属性。
* IOS（7.1.1版本）动态改变滚动元素中某个元素 `top` 属性一定机率导致画面闪动，解决办法是使用 `translateY` 替代
* IOS（7.1.1版本）通过`-webkit-overflow-scrolling: touch`方式设定的滚动元素时，如果滚到头的时候拖动，会出现页面的整体滚动，解决办法见<https://github.com/chemzqm/scrollfix/blob/master/index.js>
* IOS8一个页面内播放超过15个video之后触发解码器错误，将不能继续播放其他video。
