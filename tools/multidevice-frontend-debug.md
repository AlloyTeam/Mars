# 移动端前端开发调试指南

原文地址：<http://yujiangshui.com/multidevice-frontend-debug/>

## 响应式测试

响应式现在基本是中小型项目的标配了，先来谈谈响应式测试技巧。

### 基础的响应式测试

响应式的测试特别简单，通过改变视窗大小（也就是缩放你的浏览器）即可测试。当然，你的 CSS 中 Media Queries 判断条件设置时要使用 `max-width` 才行，如果使用 `max-device-width` 则会根据你设备的屏幕尺寸来判断。区别详情请看 [这里](http://stackoverflow.com/questions/6747242/what-is-the-difference-between-max-device-width-and-max-width-for-mobile-web)。

对于 Chrome 浏览器，你可以将 Chrome DevTools 放在右边，这种布局方式尤其适合用在外接的大屏幕上。然后通过拖动 DevTools 快速测试响应式的显示效果：

![用 Chrome DevTools 快速测试](http://jiangshui.b0.upaiyun.com/blog/2013/12/chrome2.gif)

优点就是对于 Chrome 开发者可以快速查看响应式变化效果。缺点就是分辨率尺寸不会很精确，因为它的页面宽度是添加了滚动条之后的宽度，这样对 Media Queries 的临界值效果不好测试。

对于 Firefox 浏览器，不愧是早期开发的必备神器，它早就内置了响应式测试工具，可以通过  `Firefox 工具` -》`Web 开发者` -》`自适应设计视图` 启用：

![Firefox 自适应设计视图](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test0.png)

可以设置分辨率等参数，以及模拟 `touch` 事件、屏幕截图等功能，可以随意拖动。足够简单和流畅，很方便测试响应式的变化效果等。对于基础的响应式测试以及临界值变化情况测试，强烈推荐 Firefox 浏览器。

由于响应式测试太简单，于是有了一大堆的书签栏 JS 工具或者 Chrome 扩展，并且以很多交互特效、复杂的功能来吸引用户。实际上使用起来，你可能需要依靠网络才能使用，还会遇到切换缩放不够流畅、刷新不方便等等问题，在这里不推荐。

### Chrome 模拟设备尺寸

如果你需要测试某种明确的机型，Chrome 新版的 `Emulation` 就可以派上用场了。`Emulation` 现在变成了一个手机图标（![Chrome Emulation Phone icon](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test1.png)），之前的 `Emulation` 面板被放在了 DevTools 的分裂视图中了，如果你怀念以前的 `Emulation` 面板或者需要模拟地理位置、加速计等功能，在 DevTools 界面摁下 `ESC` 即可打开分裂视图。打开 DevTools 之后，点击这个“手机图标”即可进入 Chrome 手机模拟器：

![Chrome 手机模拟器](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test2.png)

在 Device 你可以选择预置的设备，快速切换分辨率和屏幕有关参数。此外还可以设置分辨率比率，来模拟 Retina 或者更高级屏幕下的效果，这样可以测试你的响应式图片是否被正确替换等。它甚至提供了网络测试，来测试低网速情况下你的页面加载情况。慢网速的测试，往往需要用抓包工具（Charles 等）来模拟，现在用 Chrome 也可以模拟了。

除此之外，Chrome 的手机模拟器还提供了非常非常多的实用功能，比如模拟 `touch` 事件、捏等手势操作、地理位置、加速计、Retina 等等，详情请见 [官方文档](https://developer.chrome.com/devtools/docs/device-mode)，英文不好的朋友可以看我的 [翻译版本](https://github.com/yujiangshui/CN-Chrome-DevTools/blob/device-mode/md/Use-Tools/device-mode.md)。节约篇幅，这里不再赘述。

这里的方法仅能作为基础的响应式测试，对于中小型、比较简单的项目，完全足够用了，对于稍微复杂的页面，还是需要用虚拟机或者真机测试，这样更加可靠。


## 基于 Android 的移动端前端开发调试

Android 系统是份额最大的移动端设备操作系统。一方面，Android 是 Google 开发的，浏览器等也是基于 Blink 内核（早期版本基于 Webkit ），都是 Google 开发的，所以技术上应该是没有问题的。另一方面，Google 无偿开源 Android 系统，结果导致很多小厂商自己乱改 Android 系统，各种版本遍地生花，各种 BUG 层出不穷。

### Android 虚拟机测试

在电脑上安装 Android 虚拟机，就可以用虚拟机打开进行测试。一般推荐两个：

#### Genymotion

[Genymotion](https://www.genymotion.com/#!/)是一个很棒的 Android 虚拟机。但是首次安装配置需要麻烦一些。由于基于 VirtualBox 内核，所以要先安装 [VirtualBox](https://www.virtualbox.org/wiki/Downloads)，然后需要注册账号 Genymotion，可以免费使用，但是有功能限制。如果遇到重要的项目，临时买一两个月高端账号也是 OK 的。

安装完成，登陆之后，选择 Android 版本和手机型号，即可下载对应的虚拟机包，下载好的虚拟机会显示在列表中，你可以选择开启。

![Genymotion 虚拟机列表](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test3.png)

安装好的虚拟机与你 Host 本机处于一个局域网，这样你就可以用 [BrowserSync](http://www.browsersync.io/) 之类的，开启一个局域网 IP 本地服务器，在移动设备上同步测试了。关于 BrowserSync，如果你没接触过，下面有讲。

比较蛋疼的是，Genymotion 虚拟机里面安装 APP 好像比较麻烦，安装 Chrome 不太方便，这样不方便连接桌面版 Chrome 进行调试，只能使用 Weinre 调试。如果你有 Genymotion 使用这方面的经验欢迎分享。

#### Parallels

[Parallels](https://www.parallels.com/) 是基于 Mac 平台的虚拟机，使用它创建虚拟机的时候，可以直接下载 Android 系统并安装，超级傻瓜的操作，但是超级好用。

![Parallels 安装虚拟机](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test4.png)

没错，它还可以装 Chrome OS，只需要点击一下等待下载即可。

其他虚拟机软件应该也可以实现，不如这两种好用，如果这两种你无法使用，可以自行搜索选择其他方法尝试。Win 系统可以直接安装 Android SDK 也可以通过虚拟机方式，这里不再赘述。

安装完虚拟机，就可以用里面的浏览器打开网页进行测试了，虚拟机与本机处于一个局域网，可以用局域网 IP 来调试本地页面。

虚拟机不是真机，但是要比直接用浏览器测试强一些，在桌面操作比较方便，还可以安装多个版本测试。

### Android 真机调试

桌面端的前端开发调试非常简单，因为有 Firebug、Chrome DevTools 等工具，直接右击打开就可以看到元素的 CSS，并且可以查看各种资源、修改运行调错 JS 等。而移动端浏览器显然没法带有这些功能，于是可以用数据线连接设备，然后用电脑上的 Chrome DevTools 来调试移动设备上的页面。

首先，你的 Chrome 版本必须高于 32。其次你的测试机 Android 系统高于 4.0，测试机安装 Chrome for Android 才可以使用 Chrome 远程调试这项功能。

先用数据线将 Android 测试机连接到电脑上。需要打开测试机上面“开发者选项”中的 “USB 调试”功能。在 Android 4.2+ 系统上“开发者选项”默认是隐藏的，所以你需要先开启“开发者选项”（开启方法：`设置` -》 `关于本机` -》 `猛击版本号（Build number）多次` 即可开启开发者选项）。之后如果没有开启，或者没有反应，可能是你的版本问题或者点击错了，你可以尝试把 `关于本机` 上所有的选项都猛击几次，就会开启。

然后在桌面版 Chrome 打开 `chrome://inspect` 即可查找你的设备，在设备上的 Chrome 打开网页，即可看到，然后就可以在桌面版 Chrome DevTools 调试移动设备上的页面了。

![Chrome 远程调试页面](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test5.jpg)

此外，还可以直接在桌面版 Chrome 输入 URL 在移动设备上打开；在本地用 Nodejs 或者其他功能开启一个本地服务器，用端口转接让移动设备直接访问本机 localhost 上的页面，再配合 LiveReload、BrowserSync 之类的工具，自动刷新，测试简直爽歪歪。

更多细节不再赘述，可以查看 [Remote Debugging 官方文档](https://developer.chrome.com/devtools/docs/remote-debugging) 或者我的 [翻译版本](https://github.com/yujiangshui/CN-Chrome-DevTools/blob/remote-debugging/md/Use-Tools/remote-debugging.md)。


### Android WebView 前端开发调试

现在越来越多的移动端 APP 是 WebView，因为开发方便，更新快捷。那么就会有调试 WebView 的需求，因为他们本身就是网页。

#### 基于 Chrome 的调试

在 Android 4.4（KitKat）或者更新版，你可以使用 DevTools 来调试原生安卓应用中的 WebVies 内容。

不过需要在你开发的应用中，添加有关代码才可以启用 WebView 的调试，这里比较有局限性，有兴趣的朋友可以参照 [官方文档](https://developer.chrome.com/devtools/docs/remote-debugging#debugging-webviews) 或者我的 [翻译版本](https://github.com/yujiangshui/CN-Chrome-DevTools/blob/remote-debugging/md/Use-Tools/remote-debugging.md#%E8%B0%83%E8%AF%95-webviews) 试下，这里不再赘述。

#### 使用 Weinre 调试

Weinre 是一个相当简单好用的调试工具。它会在你本地创建一个监听服务器，并提供一个 JavaScript，你只需要在需要测试的页面中加载这段 JS，就可以被 Weinre 监听到，在 Inspect 面板中调试你这个页面。

目前 Weinre 也发布到 NPM 上了，Mac 下具体使用方法如下（ Win 的同学请参加：[远程调试工具-weinre](http://wyqbailey.diandian.com/post/2011-11-09/20511143)）：

首先安装 Weinre：

	npm install -g weinre
	
安装完成之后，要在本地开启一个监听服务器，需要获取本机的局域网地址：

* Mac 在终端执行 `ipconfig getifaddr en0` 命令。
* Win 在命令行执行 `ipconfig` 命令。

这时候拿到一个 IP，就本例而言，我的 IP 为 `10.189.249.254`，这时候执行：

	weinre --boundHost 10.189.249.254
	
开启本地监听服务器。

![开启 Weinre 监听服务](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test6.png)

这里有一个网址，就是 Weinre 的一些说明，我们可以打开看下：

![Weinre 控制面板](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test7.png)

这里最重要的是箭头所指的 `<script src="http://10.189.249.254:8080/target/target-script-min.js#anonymous"></script>` 这个 JS，我们需要把这个 JS 放到我们要调试的页面中，这样访问页面的时候，加载这个 JS，就会被 Weinre 监听到进行控制。

小提示：这个 JS 后面的 `#anonymous` 起到一个标识作用，为了区别，我们可以将其修改成 `#test` 放到页面中。这时候，我们的 Inspect 面板的地址就不是 `http://10.189.249.254:8080/client/#anonymous` 了，而是 `http://10.189.249.254:8080/client/#test`。

当我们访问页面的时候，就会出现在监听列表中，如果有多个网页，你可以从列表中选择一个。然后就可以使用后面的 Elements、Console 等面板来进行调试操作了：

![使用 Weinre 开发调试](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test8.png)

Weinre 非常灵活，只需要在页面中加载这个 JS，然后访问即可，因此 WebView 可以用这种方法调试，一些低版本的 Android、iOS 也可以支持，Window Phone 也是可以用的。在调试移动设备时你可能需要在本地搭建一个局域网 IP 的服务器，将设备与本机网络连接成一个局域网，用移动设备访问这个网页即可。

当然 Weinre 也不是万能的，相比 Chrome 的调试工具，它缺少 JavaScript debug 以及 Profiles 等常用功能，但是它兼容性强，可以实现基础调试功能。


## 基于 iOS 的移动端前端开发调试

iPhone 等一系列苹果设备对前端还是相当友好的，性能够好，Safari 浏览器也是不错，型号固定统一，问题也比较好解决，此外苹果公司也提供了一系列开发者工具。

Safari 默认是隐藏开发选项的，在第一次使用的时候，需要在 Safari 中选择 “偏好设置”-》“高级”-》“在菜单栏中显示开发选项”：

![开启 Safari 开发功能](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test11.png)

### 使用 iOS Simulator 调试开发

iOS Simulator 是 Xcode 开发工具内置的 iOS 模拟器，因此该功能仅能在 Mac 系统下使用。按照如下方式即可打开：

![打开 Xcode 的 iOS 模拟器](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test9.png)

打开之后，你可以用模拟器里面的 Safari 打开需要调试的网页。它可以直接打开本地 localhost 的页面，无须任何设置。你可以选择上面菜单中的“硬件”来模拟其他 iOS 设备，包括 iPad 等。如果你升级了你的 OS X 系统和 Xcode 6，你还可以模拟 iPhone 6 和 iPhone 6 Plus。

如果需要调试，打开桌面版的 Safari，在“开发”中选择要调试的页面，即可打开 Safari 调试面板：

![Safari 调试 iOS 模拟器](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test10.png)

这样就可以进行调试了。这里提供一个技巧：将 URL 粘贴到模拟器的地址栏时，用 `CMD + V` 是无法粘贴进去的。如果想要粘贴，先摁下 `CMD + V` 然后再用鼠标点击一下地址栏，稍等会出现 `Paste` 按钮，再用鼠标点击一下这个按钮即可粘贴进去。

### iOS 设备真机调试

模拟器已经足够强大方便了，但有些手势操作测试以及最真实的用户体验测试还是需要真机。Safari 调试真机上的网页也是非常简单的。

首先需要在 iPhone 等设备上设置一下 Safari 浏览器，开启调试功能。具体步骤：“设置”-》“Safari”-》“高级”-》“Web 检查器”。使用数据线连接电脑，在设备上用 Safari 浏览器打开需要调试的页面，之后在桌面版的 Safari 开发选项中即可看到进行调试，跟用 iOS Simulator 一样，只不过现在换成了真机。

但是调试本地网站，你可能要将手机与电脑连在一个局域网内，然后开启一个局域网 IP 的服务器进行调试，稍微麻烦。

此外 Safari 还可以调试在 iOS 上面的 WebView，比如用[调试 PhoneGap 打包的 APP](http://phonegap-tips.com/articles/debugging-ios-phonegap-apps-with-safaris-web-inspector.html) 等，方法类似，[这里](https://github.com/paulirish/iOS-WebView-App) 还有个测试用 APP，会 iOS 开发的朋友可以看下。


### 使用 MIHTool 进行远程调试

[MIHTool](http://www.mihtool.com/) 是国人 [听秦](http://weibo.com/unbug/) 开发的，基于 Weinre，用于 iOS 设备的前端开发测试。

上面有提到 Weinre 大体的工作方式，即开启一个服务器，然后将 JS 插入到页面中，访问进行调试。MIHTool 将这个过程简化了，它是一个 APP，可以直接安装到你的 iOS 设备里面，然后内置一个简单的浏览器可以打开你的测试页面，当它开启时，会自动向页面中插入 Weinre 的 JS，并告知 Weinre 控制台 URL 等信息，让你可以访问进行调试。

它还提供了一个公共的 Weinre 调试服务，生成类似 `http://i.mihtool.com/dev/client/#AwAj` 这样的链接，打开即可调试，非常方便，就是有些卡。

除此之外，它还提供了很多方便调试的功能，有兴趣的朋友可以看下 [官方网站的介绍](http://www.mihtool.com/) 和 [Debugging web content on iOS](http://paulbakaus.com/tutorials/performance/mihtool-the-ios-web-debugger/)。感觉就是丑了一些，如果能请设计师或者交互设计一下，会好得多。


## 移动设备在线测试

移动端设备如此之多，小公司或者团队，没有这么多资金和精力购买如此多的测试设备进行测试。于是就有人买了这些设备，连接起来，提供在线调试服务。

例如用不同的设备访问你的网站，并截图：

![使用 BrowserStack 批量截图服务](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test12.png)

甚至可以让你远程控制一台机器，进行测试操作：

![使用 BrowserStack 远程测试](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test13.png)

[BrowserStack](http://www.browserstack.com/) 就提供这种服务，它可以实时在线调试，也可以 [截屏](http://www.browserstack.com/screenshots)、[测试响应式](http://www.browserstack.com/responsive) 等等。

此外 [Keynote](http://www.keynote.com/) 也提供这种服务，当然这里的 Keynote 不是 Mac 上的幻灯片 APP。它提供更加真实的 Mobile 测试，我简单的试了一下，果然比较卡，应该是真机测试：

![使用 Keynote 远程测试](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test14.png)

## 其他移动端调试方法和技巧

### BrowserSync 同步操作

[BrowserSync](http://www.browsersync.io/) 是我最爱的多终端测试工具。在没有使用这个BrowserSync 之前的原始的测试流程一般是这样的：

> 先把本地的网页上传到远程服务器（因为好多设备都要去访问一个固定的地址），然后将网址输入到各个测试机的测试浏览器里面手动打开(或者使用浏览器插件等，生成二维码扫一下）。然后手机开始下载页面，需要等待下载。观看效果进行测试，每个测试机都要操作一遍。测试其他网页的时候，每个测试机重新输入网址、刷新。如果代码有修改，需要重新上传服务器进行刷新。

而 BrowserSync 这个工具，可以用你局域网 IP 创建一个本地服务器，生成一个类似 `http://10.189.249.135:3002` 的 URL，这样所有与你电脑处在一个局域网的设备，都可以访问到你本地的页面。

建议使用无线路由器搭建一个无线局域网，所有设备都连入这个无线局域网。Win 系统电脑用软件开启 Wifi 共享也是可以的，Mac 就比较悲剧了，只有在插网线的时候，可以开启 Wifi 共享功能。

BrowserSync 还会监听文件变动，当监听的文件发生变动，会自动刷新所有连接本地服务器的页面。BrowserSync 最主要的功能是同步，同步一切操作，当你在某个浏览器中触发的操作，会在所有测试浏览器中同步操作，例如在电脑上滚动页面，所有手机都会滚动页面；电脑上更换了 URL 测试另一个页面，所有手机都跳转到另一个页面。

应用 BrowserSync 工具之后的新版测试流程就变成这样了：

> 用 BrowserSync 开启本地服务器，所有测试设备连接到局域网中，依次打开 `http://10.189.249.135:3002/`（BrowserSync 创建的本地服务器地址）。在一台设备操作，观察其他设备的情况，修改了 CSS、HTML 或者 JS 代码，保存一下，自动在所有设备自动刷新。

BrowserSync 的使用非常简单，在要创建服务器的目录下面执行：`browser-sync start --server --files="*"` 命令即可，表示创建一个服务器并监听该目录下的文件变动。它也有提供 Grunt 和 Gulp 插件，更多的用法移步 [BrowserSync 官方文档](http://www.browsersync.io/)，这里不再赘述。

BrowserSync 的原理大体是这样的，它会在 HTML 页面里面插入 JS，然后监听页面操作。所以当你滚动页面或者跳转新页面，BrowserSync 可以捕获到这个操作，通过 Socket.io 向所有 Client 的 JS 发出操作指示，其他设备也会随之 `scroll` 或者 `location.href` 跳转等，实在太巧妙。

此外，两个 BrowserSync 的小提示：

* BrowserSync 默认请求 `index.html`，如果你的目录里面没有这个文件夹，会返回 `Cannot GET /`，这时候你需要指定具体的目录、文件。
* 在开启 BrowserSync 的命令中，`--files="*"` 表示要监听变动的文件。如果你指定了 `--files="css/*.css"` 就表示只监听 `css/` 下的所有 css 文件变动。如果遇到修改代码没有自动刷新的问题，可能是你监听的路径和文件有问题。对于 CSS 的修改，它会采用无刷新注入的方式，JS 和 HTML 的修改，它会采用刷新的方式。

### Charles 代理应用

[Charles](http://www.charlesproxy.com/) 是 Mac 系统下面的抓包、代理工具。如果你电脑是 Win 系统，可以使用 [Fiddler](http://www.telerik.com/fiddler) 实现本节要介绍的技巧。 

使用场景举例：当我们在本地开发时使用内网登陆功能（需要同域），往往需要绑定 Host，比如将本机 `127.0.0.1` 绑定为 `xx.xx.com`。这样我们访问本地服务器时使用 `xx.xx.com`，才可以正常使用 登陆 等等服务（需要用到 Cookie）。

那我们用移动端设备测试这个页面的时候，也需要修改移动端设备上的 Host。因此 Android 需要 root，iPhone 需要越狱，而且每次都要开启，极为不方便。这时候，我们就可以使用 Charles 这里抓包工具做一个代理。

当打开 Charles 时，它会自动在本机开启一个代理服务，默认接口为 `8888`。这时候，我们设置同局域网内的移动设备的代理为本机局域网 IP，即可通过 Charles 转发请求，在移动设备上访问电脑可以访问的内容。基本原理如下图：

![Charles 代理实现原理](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test15.png)

通过这个代理服务，移动设备的请求被转移到到电脑上发送出去，并将电脑得到的响应返回给移动设备。其他同类问题（想用手机访问只有电脑才能访问的内容）均可用这种方式解决。此外，因为经过 Charles 代理，因此可以使用 Charles 的查看有关请求和响应、做本地资源映射等等功能，来简化开发和调试 BUG。

启用方法详情请见：[iOS开发工具——网络封包分析工具Charles](http://www.infoq.com/cn/articles/network-packet-analysis-tool-charles) 中的 截取iPhone上的网络封包 一节，这里不再赘述。

提供一个 Charles 的小技巧：Charles 只提供了全局监听和 Firefox 监听，但我常用的是 Chrome 浏览器，我只想监听 Chrome 浏览器中某个页面的请求信息，也可以通过设置代理来解决。这里使用 SwitchySharp 代理插件（GAE 翻墙必备），增加一个新的情景模式，绑定本地 Charles 代理。

![Charles 监听 Chrome 浏览器](http://jiangshui.b0.upaiyun.com/blog/2014/12/mobile-test16.png)

这样当我们想抓包某个页面时，只需要打开 Charles 并勾掉 `Proxy`-》`Mac OS X Proxy` 和 `Mozilla Firefox Proxy`，之后再在 SwitchySharp 中勾选这个情景模式，即可清爽的只监听 Chrome 浏览器发送的请求了。

关于 Charles 的使用，可以自行搜索教程，Fiddler 同样原理，不再赘述。

## 回顾总结与扩展阅读

### 移动端前端重构项目开发流程最佳实践

新建项目相关文件，然后应用 BrowserSync 等工具（可以配合 [Grunt](http://yujiangshui.com/grunt-basic-tutorial/) 等）启动本地服务器。在 Chrome 中启用 Emulation 来模拟 iPhone 等设备的尺寸，进行编码开发。这样就可以无刷新、比较直观的看到手机上的效果。

开发基本完成，将测试机、虚拟机等打开联入局域网，输入本地服务器地址，开始测试。对文件的修改实时刷新在所有设备中，即时看到效果。

对于有点复杂的 BUG 或者问题，使用 Safari 或者 Chrome 连接虚拟机或者真机进行调试。

### 不同测试场景下需要用到的技术和工具

* 响应式测试：Chrome DevTools 面板右侧拉伸快速查看效果；Firefox 响应式工具进一步调整；Chrome Emulation 精细测试。
* Android 设备测试：使用 Android 虚拟机；高版本 Android 测试机，使用 Chrome 连接调试。Android 4.4+ 的 WebView 修改 APP 源代码，也可以用 Chrome 调试。
* 低版本系统和其他品牌手机以及 WebView：统统可以用 Weinre 来解决。
* iOS 设备测试：使用 Xcode 自带 iOS 模拟器，使用 Safari 调试；WebView 也可以被电脑上 Safari 调试；测试机连接电脑，也可以用 Safari 调试；MIHTool 可以在 iOS 设备上使用，提供类似 Weinre 的调试功能。
* 测试多种设备：BrowserStack 和 Keynote。
* 使用 BrowserSync 可以创建本地局域网 IP 服务器，并同步操作、监听刷新，极大减少测试操作，提高测试效率。
* 当移动端设备无法访问某项资源时，使用 Charles 做代理，通过电脑去访问。

### 扩展阅读与资料参考

* [Remote Debugging on Android with Chrome](https://developer.chrome.com/devtools/docs/remote-debugging#virtual-host-mapping)（[翻译版本](https://github.com/yujiangshui/CN-Chrome-DevTools/blob/remote-debugging/md/Use-Tools/remote-debugging.md)）
* [Device Mode & Mobile Emulation](https://developer.chrome.com/devtools/docs/device-mode)（[翻译版本](https://github.com/yujiangshui/CN-Chrome-DevTools/blob/device-mode/md/Use-Tools/device-mode.md)）
* [About Safari Web Inspector](https://developer.apple.com/library/safari/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/Introduction/Introduction.html)
* [A Concise Guide to Remote Debugging on iOS, Android, and Windows Phone](http://developer.telerik.com/featured/a-concise-guide-to-remote-debugging-on-ios-android-and-windows-phone/)
* [各种 真机远程调试 方法 汇总](https://github.com/jieyou/remote_inspect_web_on_real_device)
* [浏览器远程调试](https://reader.mx/p/1391)
* [weinre - Running](http://people.apache.org/~pmuellr/weinre/docs/latest/Running.html)
* [BrowserSync](http://www.browsersync.io/)
* [Charles](http://www.charlesproxy.com/)

本文不断更新，如有错误、补充，请随时评论或者联系本人。