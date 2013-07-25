## 字体设置

```css
body {
    font-family: HelveticaNeue, Helvetica, STHeiTi, sans-serif;
}
```

iOS 4.0+ 使用英文字体 Helvetica Neue，之前的iOS版本降级使用 Helvetica。

中文字体设置为华文黑体STHeiTi。

需补充说明，华文黑体并不存在iOS的字体库中(http://support.apple.com/kb/HT5484?viewlocale=en_US)，
但系统会自动将华文黑体STHeiTi兼容命中系统默认中文字体黑体-简或黑体-繁：

```
Heiti SC Light 黑体-简 细体
Heiti SC Medium 黑体-简 中黑
Heiti TC Light 黑体-繁 细体
Heiti TC Medium 黑体-繁 中黑
```

Android下中文字体与英文字体都选择默认的无衬线字体。

4.0之前版本英文字体Android使用的是Droid Sans，中文字体Android会命中Droid Sans FallBack。

4.0+ 中英文字体都会使用Android新的Roboto字体。




