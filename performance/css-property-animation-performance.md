# CSS动画属性性能

* CSS动画属性会触发整个页面的重排relayout、重绘repaint、重组recomposite
* Paint通常是其中最花费性能的，尽可能避免使用触发paint的CSS动画属性，这也是为什么我们推荐在CSS动画中使用`webkit-transform: translateX(3em)`的方案代替使用`left: 3em`，因为`left`会额外触发layout与paint，而`webkit-transform`只触发整个页面composite

```css
div {
  -webkit-animation-duration: 5s;
  -webkit-animation-name: move;
  -webkit-animation-iteration-count: infinite;
  -webkit-animation-direction: alternate;
  width: 200px;
  height: 200px;
  margin: 100px;
  background-color: #808080;
  position: absolute;
}
```

```css
@-webkit-keyframes move{
	from {
		left: 100px;
	}
	to {
		left: 200px;
	}
}
```

如下图使用`left`将持续触发页面重绘，表现为红色边框：

![move](https://f.cloud.github.com/assets/677114/1755561/a8fb9c94-6666-11e3-8788-ac5b5ef4ef24.gif)


```css
@-webkit-keyframes move{
	from {
		-webkit-transform: translateX(100px);
	}
	to {
		-webkit-transform: translateX(200px);
	}
}
```

如下图使用`-webkit-transform`页面只发生重组，表现为橙色边框：

![move2](https://f.cloud.github.com/assets/677114/1755562/aaef262e-6666-11e3-8e83-3e770f269af0.gif)

* CSS属性在CSS动画中行为表

![CSS Property Animation on the Web](https://f.cloud.github.com/assets/677114/1752383/1f8c5e8e-661c-11e3-9725-306f7e5c73f5.png)



## 参考
* [#perfmatters: 60fps layout and rendering](https://docs.google.com/presentation/d/1CH8ifryioHDLT1Oryyy8amusUmq2FytpCPCpk0G3E4o/edit#slide=id.p)
