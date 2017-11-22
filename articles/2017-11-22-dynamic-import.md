# 动态 import() | Dynamic import()

- 浏览器支持：Chrome 63、 [Safari 24 预览版](https://webkit.org/blog/7423/release-notes-for-safari-technology-preview-24/)
- TC39 proposal：https://github.com/tc39/proposal-dynamic-import
- Stage：3
- 规范：https://tc39.github.io/proposal-dynamic-import/

## Static import

Chrome 61 开始支持 ES2015 的 [modules](https://jakearchibald.com/2017/es-modules-in-browsers/)。

`import` 导入的模块必须是字符串字面量，不能是变量。因为 `import` 是在编译时（pre-runtime）确定的，这要早于运行时。如下代码将报错:

```javascirpt
if (name === 'jjc') {
  import myName from './jjc';
} else {
  import myName from './other';
}
```

下面代码也会报错：

```javascirpt
const name = 'jjc';
import myName from name;
```

静态导入可以在编译阶段对代码进行静态分析、构建、tree-shaking 等。

## Dynamic import()

动态导入可以让我们进行**按需导入**等特性。

语法：

```javascript
import(moduleSpecifier)
```

`import()` 返回一个 Promise

```javascript
<script type="module">
  const moduleSpecifier = './utils.js';
  import(moduleSpecifier)
    .then((module) => {
      // doSth.
    });
</script>
```

**注意**：`import()` 虽然看上去像一个函数调用，但其实 `import` 只是恰好使用了括号语法而已（类似于 `super()`）。
这意味着 `import` 并不是继承自 `Function.prototype`，所以不能使用 `call` 和 `apply`。
使用 `const importAlias = import` 也是不行的。甚至，`import` 根本就不是一个对象！

## 建议

"静态 import" 和"动态 import()" 都同样重要。使用静态导入可以在运行之前构建模块的依赖关系，而动态导入可以在运行时按需加载模块。

-----------

> 阅读原文：[Dynamic import()](https://developers.google.com/web/updates/2017/11/dynamic-import)
>
> 讨论地址：[动态 import()](https://github.com/dev-reading/fe/issues/10)
> 
> 如果你想参与讨论，请[点击这里](https://github.com/dev-reading/fe)
