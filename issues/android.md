Andorid Issues
==============
1. 三星I9100 （Android 4.0.4）不支持display:-webkit-flex这种写法的弹性布局.  
但支持display:-webkit-box这种写法的布局,   
相关的属性也要相应修改，如-webkit-box-pack: center;  
移动端采用弹性布局时，建议直接写display:-webkit-box系列的布局  

2. touchmove事件在Android部分机型(如LG Nexus 5 android4.4，小米2 android 4.1.1)上只会触发一次  
解决方案是在触发函数里面加上e.preventDefault(); 记得将e也传进去。

3. HTC Desire HD A9191 (Android 2.3.5) display:table-cell 元素上设置 position:relative 不起作用,   
解决办法是只在 display:block 元素上设置 position:relative

4. HTC Desire HD A9191 (Android 2.3.5) 为 display:none 元素通过添加 css class 设置的 display:block 无法起作用，解决办法是使用内联样式 `el.styls.display=‘block'`显示元素

5. HTC Desire HD A9191 (Android 2.3.5) 显示遮罩层后调用`window.scrollTo` 滚动到顶不起作用，解决办法是先调用 `scrollTo`方法，再显示遮罩层

