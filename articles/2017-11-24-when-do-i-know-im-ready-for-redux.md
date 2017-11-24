# 4 张动图解释为什么（什么时候）使用 Redux

> 过早优化是万恶之源 —— Donald Knuth

本文描述了**什么时候**开始使用 Redux。作者描述了在构建一个真实 React APP 时，从没有使用 Redux 到使用 Redux 的过程以及收获。

首先，**并不是所有的 React 应用程序都需要使用 Redux**。事实上，大多数非常简单的 React 应用程序根本不能从 Redux 中受益。

## 第 1 天

使用 React 本地组件状态

React 使用[单向数据流](https://reactjs.org/docs/state-and-lifecycle.html#the-data-flows-down)，这意味着父组件把自身的状态作为属性传递给子组件。

![](../assets/when-do-i-know-im-ready-for-redux-1.gif)

## 第 5 天

随着添加更多的功能，**非父子**组件之间需要**共享**一些状态。

我们通过[提升状态](https://reactjs.org/docs/lifting-state-up.html)来解决这个问题。

这意味着我们将状态（和改变这个状态的函数）**提升到最接近的祖先**（Container Component）。我们将这些函数绑定到容器组件，并将它们作为属性向下传递。这意味着子组件可以触发其父组件中的状态更改，这将**更新树中的所有其他组件**。

![](../assets/when-do-i-know-im-ready-for-redux-2.gif)

## 第 20 天

随着添加了更多的功能和组件，我们的应用程序状态流程开始看起来像这样...

![](../assets/when-do-i-know-im-ready-for-redux-3.gif)

## 第 n 天

如果您开始遇到上述某些问题，则可能意味着您应该使用 Redux 了。

## Redux

当我们使用 Redux 后，状态变成了这样：

![](../assets/when-do-i-know-im-ready-for-redux-4.gif)

如果您的应用符合以下某些条件，那么我认为应该立即使用 Redux。

- UI 可以根据应用程序状态显着变化
- 并不总是以一种线性的，单向的方式流动
- 许多不相关的组件以相同的方式更新状态
- 状态树并不简单
- 状态以许多不同的方式更新
- 您需要能够撤消以前的用户操作

-----------

> 阅读原文：[When do I know I’m ready for Redux?](https://medium.com/dailyjs/when-do-i-know-im-ready-for-redux-f34da253c85f)
>
> 讨论地址：[4 张动图解释为什么（什么时候）使用 Redux #11](https://github.com/dev-reading/fe/issues/11)
> 
> 如果你想参与讨论，请[点击这里](https://github.com/dev-reading/fe)
