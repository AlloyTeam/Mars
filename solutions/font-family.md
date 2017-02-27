## 字体设置

```css
body {
    font-family: -apple-system, BlinkMacSystemFont, "PingFang SC","Helvetica Neue",STHeiti,"Microsoft Yahei",Tahoma,Simsun,sans-serif;

}
```

iOS 4.0+ （iOS 9以下系统已经非常少） 使用英文字体 Helvetica Neue，之前的iOS版本降级使用 Helvetica。
中文字体设置为华文黑体STHeiTi。

iOS 9+ Safari开始支持 -apple-system 参数， Chrome 使用 BlinkMacSystemFont ，兼容 iOS ／ MacOS     

`微软雅黑`是为了兼容Win系统，毕竟视网膜分辨率的win系统用`Simsun`是非常丑陋的，可以用4K屏 windows 去看 JD 淘宝，你能忍的话我就没话说

`PingFang SC` 是简体苹方，看需要 如果要命中对应 苹方字体的话 直接写  PingFang 不带引号。


需补充说明，华文黑体并不存在iOS的字体库中(http://support.apple.com/kb/HT5484?viewlocale=en_US)，
但系统会自动将华文黑体STHeiTi兼容命中系统默认中文字体黑体-简或黑体-繁：

```
Heiti SC Light 黑体-简 细体
Heiti SC Medium 黑体-简 中黑
Heiti TC Light 黑体-繁 细体
Heiti TC Medium 黑体-繁 中黑
```

原生Android下中文字体与英文字体都选择默认的无衬线字体。

4.0之前版本英文字体原生Android使用的是Droid Sans，中文字体原生Android会命中Droid Sans Fallback。

4.0+ 中英文字体都会使用原生Android新的Roboto字体。

其他第三方Android系统也一致选择默认的无衬线字体。

Android 就直接让它命中系统字体吧，因为你无法预知发行厂商会去内置什么字体，或者人家root去修改什么字体。

## 参考阅读
* [Droid, the default font for older versions of Android](http://en.wikipedia.org/wiki/Droid_fonts)
* [Roboto, the default font for newer versions of Android](http://en.wikipedia.org/wiki/Roboto)

