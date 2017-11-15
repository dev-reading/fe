# 使用 CSS overscroll-behavior 控制滚动行为：自定义下拉刷新和溢出效果

CSS 的新属性 [overscroll-behavior](https://wicg.github.io/overscroll-behavior/) 允许开发者覆盖默认的浏览器**滚动**行为，一般用在滚动到顶部或者底部。

## 背景

### 滚动边界和滚动链接（boundary & chaining）

在 APP 中经常使用的抽屉导航(drawer)中，我们期望的效果是：滚动到底部时，滚动停止，因为我们到达了"滚动边界"。

但是在 Web 页面中滚动并不会停止，而是**继续滚动抽屉后面的内容**。效果如下：

<video src="../assets/drawer-scroll.mp4" autoplay="" loop="" alt="Drawer demo" height="300"></video>

我们称这种行为叫滚动链接（**scroll chaining**）。

### 下拉刷新 pull-to-refresh

下拉刷新是一个在移动端经常使用的操作，Chrome 移动版也增加了下拉刷新的支持。

Twitter PWA 版本的自定义下拉刷新：

<video src="../assets/twitter.mp4" autoplay="" loop="" height="350"></video>

Chrome Android 版的原生下拉刷新（刷新整个页面）：

<video src="../assets/mobilep2r.mp4" autoplay="" loop="" height="350"></video>

很多时候我们需要**禁用原生的 pull-to-refresh 行为**。

以前我们想出各种方式来处理滚动，比如：不让页面滚动，而是使用 touch 事件处理滚动行为，使用 `100vw/vh` 设置页面高度禁止内容溢出或滚动，等等。。。

现在我们可以使用 `overscroll-behavior`。

## 介绍 overscroll-behavior

`overscroll-behavior` 属性有 3 个值：

1. `auto` - 默认。元素的滚动会传播给祖先元素。

2. `contain` - 阻止滚动链接。滚动不会传播给祖先，但会显示元素内的原生效果。例如，Android 上的炫光效果或 iOS 上的回弹效果，当用户触摸滚动边界时会通知用户。注意：`overscroll-behavior: contain` 在 `html` 元素上使用**可防止滚动导航操作**。

3. `none` - 和 `contain` 一样，但它也可以防止节点本身的滚动效果（例如 Android 炫光或 iOS 回弹）。

## 阻止 fixed 定位元素的滚动传播

当一个 `fixed` 定位元素滚动到边界时，会滚动元素后面的内容。如下：

<video src="../assets/chatbox-chaining.mp4" autoplay="" loop="" alt="Chatbox demo" height="350"></video>

我们可以使用 `overscroll-behavior: contain` 阻止这种行为。

如果我们有一个 `fixed` 定位的弹出层需要滚动时，默认是这样的，如下：

<video src="../assets/modal-off.mp4" autoplay="" loop="" height="290"></video>

使用 `overscroll-behavior: contain` 可以阻止滚动传播给父元素，如下：

<video src="../assets/modal-on.mp4" autoplay="" loop="" height="290"></video>

## 禁用下拉刷新 pull-to-refresh

禁用原生的下拉刷新效果，只需要在 `body` 或 `html` 元素添加：

```css
body {
  /* Disables pull-to-refresh but allows overscroll glow effects. */
  overscroll-behavior-y: contain;
}
```

当我们阻止了原生的下拉刷新后，就可以实现自己定义的下拉刷新。否则会出现两个下拉刷新：

之前：

<video src="../assets/chatbox-double-refresh.mp4" autoplay="" loop="" height="225"></video>

之后：

<video src="../assets/chatbox-double-refresh-fix.mp4" autoplay="" loop="" height="225"></video>

## 禁用炫光和回弹效果

将属性制定为 `none`，可以禁用默认的滚动边界效果。

```css
body {
  /* 禁用默认的下拉刷新和边界效果
     但是依然可以进行滑动导航 */
  overscroll-behavior-y: none;
}
```

之前:

<video src="../assets/drawer-glow.mp4" autoplay="" loop="" height="300"></video>

之后：

<video src="../assets/drawer-noglow.mp4" autoplay="" loop="" height="300"></video>

如果想禁用左右滑动的手势导航，可以使用 `overscroll-behavior-x: none`。

## 完整的 demo

Demo 地址：https://ebidel.github.io/demos/chatbox.html

源码：https://github.com/ebidel/demos/blob/master/chatbox.html

最终效果：

<video src="../assets/chatbox-fixed.mp4" autoplay="" loop="" alt="Chatbox demo" height="600"></video>

-----------

> 阅读原文：[Take control of your scroll: customizing pull-to-refresh and overflow effects](https://developers.google.com/web/updates/2017/11/overscroll-behavior)
>
> 讨论地址：[使用 CSS overscroll-behavior 控制滚动行为：自定义下拉刷新和溢出效果](https://github.com/dev-reading/fe/issues/9)
> 
> 如果你想参与讨论，请[点击这里](https://github.com/dev-reading/fe)
