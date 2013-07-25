##active的兼容(来自薛端阳)

今天发现，要让a链接的Css active伪类生效，只需要给这个a链接的touch系列的任意事件touchstart/touchend绑定一个空的匿名方法即可hack成功

	<style>
	a {
	color: #000;
	}
	a:active {
	color: #fff;
	}
	</style>
	<a herf=”asdasd”>asdasd</a>
	<script>
	var a=document.getElementsByTagName(‘a’);
	for(var i=0;i<a.length;i++){
	a[i].addEventListener(‘touchstart’,function(){},false);
	}
	</script>

##消除transition闪屏

两个方法

	-webkit-transform-style: preserve-3d;
	/*设置内嵌的元素在 3D 空间如何呈现：保留 3D*/
	-webkit-backface-visibility:?hidden;
	/*（设置进行转换的元素的背面在面对用户时是否可见：隐藏）*/
	
##消除ie10里面的那个叉号
[http://msdn.microsoft.com/en-us/library/windows/apps/hh767361.aspx](http://msdn.microsoft.com/en-us/library/windows/apps/hh767361.aspx "article4")

	input:-ms-clear{display:none;}
	
##关于ios与os端字体的优化(横竖屏会出现字体加粗不一致等)
[http://blog.sina.com.cn/s/blog_6da647a601011u4v.html](http://blog.sina.com.cn/s/blog_6da647a601011u4v.html "article5")
[http://stackoverflow.com/questions/3220662/uiwebview-font-is-thinner-in-portrait-than-landscape](http://stackoverflow.com/questions/3220662/uiwebview-font-is-thinner-in-portrait-than-landscape "article5")
 

##js事件
click 事件普遍 300ms 的延迟
在手机上绑定click 事件，会使得操作有300ms 的延迟，体验并不是很好。
开发者大多数会使用封装的 tap 事件来代替click 事件，所谓的 tap 事件由 touchstart 事件 + touchmove 判断 + touchend 事件封装组成

##ios点击会慢300ms

 [https://developers.google.com/mobile/articles/fast_buttons?hl=de-DE](https://developers.google.com/mobile/articles/fast_buttons?hl=de-DE "article5")
 [http://stackoverflow.com/questions/12238587/eliminate-300ms-delay-on-click-events-in-mobile-safari](http://stackoverflow.com/questions/12238587/eliminate-300ms-delay-on-click-events-in-mobile-safari "article5")

使用css3动画的时尽量利用3D加速，从而使得动画变得流畅。动画过程中的动画闪白可以通过backface-visibility 隐藏。

	-webkit-transform-style: preserve-3d;
	-webkit-backface-visibility: hidden;
 
	
##ie10的特殊鼠标事件

[http://www.mansonchor.com/blog/blog_detail_73.html](http://www.mansonchor.com/blog/blog_detail_73.html "article5")

##不让android识别邮箱

	<meta content="email=no" name="format-detection" />
	
##禁止ios弹出各种操作窗口

	-webkit-touch-callout:none
##禁止用户选中文字

	-webkit-user-select:none
	
##动画效果中，使用translate比使用定位性能高

<http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/>

##拿到滚动条

	window.scrollY
	window.scrollX
 
 比如要绑定一个touchmove的事件，正常的情况下类似这样(来自呼吸二氧化碳)
 
	$('div').on('touchmove', function(){
	//.….code
	{});
	
而如果中间的code需要处理的东西多的话，fps就会下降影响程序顺滑度，而如果改成这样

	$('div').on('touchmove', function(){
	setTimeout(function(){
	//.….code
	},0);
	{});
	
把代码放在setTimeout中，会发现程序变快.

##关于ios系统中，webapp启动图片在不同设备上的适应性设置

http://stackoverflow.com/questions/4687698/mulitple-apple-touch-startup-image-resolutions-for-ios-web-app-esp-for-ipad/10011893#10011893

##关于ios系统中，中文输入法输入英文时，字母之间可能会出现一个六分之一空格(焦点科技葛亮)
可以通过正则去掉 

	this.value = this.value.replace(/\u2006/g, '');
##关于android webview中，input元素输入时出现的怪异情况
见图
![怪异图](http://cdn.bielousov.com/wp-content/uploads/2012/08/android-input-label-text-issue.png)

Android web视图,至少在HTC EVO和三星的Galaxy Nexus中，文本输入框在输入时表现的就像占位符。情况为一个类似水印的东西在用户输入区域，一旦用户开始输入便会消失(见图片)。
在android的默认样式下当输入框获得焦点后,若存在一个绝对定位或者fixed的元素，布局会被破坏,其他元素与系统输入字段会发生重叠(如搜索图标将消失为搜索字段),可以观察到布局与原始输入字段有偏差(见截图)。
这是一个相当复杂的问题，以下简单布局可以重现这个问题:

	<label for="phone">Phone: *</label>
	<input type="tel" name="phone" id="phone" minlength="10" maxlength="10" inputmode="latin digits" required="required" />
	
解决方法

	-webkit-user-modify: read-write-plaintext-only
	
详细参考<http://www.bielousov.com/2012/android-label-text-appears-in-input-field-as-a-placeholder/>
注意，该属性会导致中文不能输入词组，只能单个字。感谢鬼哥与飞（游勇飞）贡献此问题与解决方案


##JS动态生成的select下拉菜单在Android2.x版本的默认浏览器里不起作用

解决方法删除了overflow-x:hidden; 然后在JS生成下来菜单之后focus聚焦，这两步操作之后解决了问题。(来自岛都-小Qi)

参考<http://stackoverflow.com/questions/4697908/html-select-control-disabled-in-android-webview-in-emulator>