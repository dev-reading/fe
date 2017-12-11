# await、return 和 return await 的陷阱

[await vs return vs return await](https://jakearchibald.com/2017/await-vs-return-vs-return-await/)

阅读时间大概 2 分钟

-------------

`await`、`return` 和 `return await` 有很多容易被忽视的不同之处。

首先定义一个异步函数：

```javascript
async function waitAndMaybeReject() {
  // 等待1秒
  await new Promise(r => setTimeout(r, 1000));

  const isHeads = Boolean(Math.round(Math.random()));

  if (isHeads) {
    return 'yay';
  } else {
    throw Error('Boo!');
  }
}
```

函数等待 1 秒钟，然后有一半的概率返回 `"yay"`，一半的概率抛出异常。


## 1 直接调用 Just calling

```javascript
async function foo() {
  try {
    waitAndMaybeReject();
  }
  catch (e) {
    return 'caught';
  }
}
```

直接调用 `foo`，函数总是返回 Promise **fulfill with undefined, without waiting**。

![](https://user-images.githubusercontent.com/359395/33812969-e650b798-de5b-11e7-82d5-e1551d332045.png)

永远不会返回 `"yay"`。

## 2 Awaiting

```javascript
async function foo() {
  try {
    await waitAndMaybeReject();
  }
  catch (e) {
    return 'caught';
  }
}
```

调用 `foo`，函数返回的 Promise **等待 1 秒**，然后 **fulfill with `undefined`, or fulfill with `"caught"`**。

因为我们 await `waitAndMaybeReject()` 的结果，如果 rejected，我们的 catch 块捕获了异常，然后 `"caught"`，如果 fulfilled，我们的函数并没有返回 Promise 的值。

## 3 Returning

```javascript
async function foo() {
  try {
    return waitAndMaybeReject();
  }
  catch (e) {
    return 'caught';
  }
}
```

调用 `foo`，函数返回的 Promise **等待 1 秒**，然后 **fulfill with `"yay"`, or fulfill with `"caught"`**。

这个是最符合我们预期的写法。

我们可以把它拆分一下：

```javascript
async function foo() {
  try {
    // 等待 waitAndMaybeReject() 函数的结果
    // 把 fulfilled value 赋值给 fulfilledValue:
    const fulfilledValue = await waitAndMaybeReject();
    // 如果 waitAndMaybeReject() 失败，抛出异常:
    return fulfilledValue;
  }
  catch (e) {
    return 'caught';
  }
}
```

-----------

> 阅读原文：[await vs return vs return await](https://jakearchibald.com/2017/await-vs-return-vs-return-await/)
>
> 讨论地址：[await、return 和 return await 的陷阱](https://github.com/dev-reading/fe/issues/9)
> 
> 如果你想参与讨论，请[点击这里](https://github.com/dev-reading/fe)
