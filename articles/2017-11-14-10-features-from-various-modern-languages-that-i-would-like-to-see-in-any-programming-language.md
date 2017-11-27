# 现代编程语言最有趣的 10 大特性

[Ten interesting features from various modern languages](https://medium.com/@kasperpeulen/10-features-from-various-modern-languages-that-i-would-like-to-see-in-any-programming-language-f2a4a8ee6727)

阅读时间大概 2 分钟

-------------

如今大多数“现代”语言都依然使用老旧的 C-style 语法。

我们看一下编程语言的年代：Lisp (1958)、Smalltalk (1972)、Objective-C (1984)、Haskell (1990)、OCaml (1996)、等等。这些都是上个世纪的语言了。

本文作者选择了几个最新的语言：Reason、Swift、Kotlin、Dart 作为研究对象，总结了 10 个特性：

## 1 管道操作符 Pipeline operator

Reason 语法

```reason
let newScore = me.score
  |> double
  |> (it) => add(7, it)
  |> (it) => boundScore(0, 100, it);
```

对应的 JavaScript 写法：

```javascript
boundScore(0, 100, add(7, double(me.score)));
```

而 es 也已经有了对应的提案：[tc39/proposal-pipeline-operator](https://github.com/tc39/proposal-pipeline-operator)

## 2 模式匹配 Pattern matching 

Kotlin 语法

```kotlin
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
```

## 3 Reactive (Rx) programming build in the language

Dart 语法

```dart
input.onKeyDown                                              
  .where((e) => e.ctrlKey && e.code == 'Enter')              
  .forEach((e) => dispatch(addTodoAction(e.target.value)));
```

### 4 lambda 函数的默认参数

Kotlin 语法（使用 `it` 作为默认参数）

```kotlin
strings
  .filter{ it.length == 5 }
  .map{ it.toUpperCase() }
```

对比 JavaScript 

```js
strings
  .filter{ it => it.length === 5 }
  .map{ it => it.toUpperCase() }
```

## 5 解构 Destructuring

Reason 语法：

```reason
let someInts = (10, 20);
let (ten, twenty) = someInts;

type person = {name: string, age: int};
let somePerson = {name: "Guy", age: 30};
let {name, age} = somePerson;
```

Kotlin 语法

```kotlin
data class Person(val name: String, val age: Int)
val(name, age) = Person("Guy", 20)
```

es6 已经有了数组解构，es8 增加了对象解构

## 6 操作符级联 Cascade operator

Dart 语法

```dart
querySelector('#button') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => dispatch(confirmedAction()));
```

对应的 JavaScript 写法

```js
var button = querySelector('#button');
button.text = 'Confirm';
button.classed.add('important');
button.onClick.listen((e) => dispatch(confirmedAction()));
```

如果使用 jQuery 基本在**写法上**就和 dart 一致了，但是两者有本质的不同

## 7 if 表达式 If expressions

Kotlin 语法

```kotlin
val result = if (param == 1) {
    "one"
} else if (param == 2) {
    "two"
} else {
    "three"
}
```

对于 if 表达式有人喜欢，有人讨厌，有人觉得无所谓；我是非常喜欢的，我之前在知乎有个回答：https://www.zhihu.com/question/55866176/answer/149009695

## 8 Try expressions

Kotlin 语法

```kotlin
val result = try {
    count()
} catch (e: ArithmeticException) {
    throw IllegalStateException(e)
}
```
## 9 自动科里化 Automatic currying

Reason 语法：

```reason
let add = (x, y) => x + y;   /* same as (x) => (y) => x + y; */
let five = add(2,3);         /* 5 */
let alsoFive = add(2)(3);    /* 5 */
let addFive = add(5);        /* y => 5 + y; */
let eleven = addFive(6);     /* 11 */
let twelve = addFive(7);     /* 12 */
```

## 10 方法扩展 Method extensions

Swift 语法：

```swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}

3.repetitions({
    print("Hello!")
})
// Hello!
// Hello!
// Hello!
```

JavaScript 可以在原型上扩展。

我觉得还有要给非常有用的特性，[optional-chaining](https://github.com/tc39/proposal-optional-chaining)。之所以没有提到，是因为大多数语言都已经有这个特性了吧，看来 JavaScript 还是发展太慢啊。。。

-----------

> 阅读原文：[Ten interesting features from various modern languages](https://medium.com/@kasperpeulen/10-features-from-various-modern-languages-that-i-would-like-to-see-in-any-programming-language-f2a4a8ee6727)
>
> 讨论地址：[现代编程语言最有趣的 10 大特性](https://github.com/dev-reading/fe/issues/8)
> 
> 如果你想参与讨论，请[点击这里](https://github.com/dev-reading/fe)
