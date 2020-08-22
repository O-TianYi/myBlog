[参考](https://blog.rxliuli.com/p/acfc2875/)



var中：

```
for (var i = 0; i < 3; i++) {
  var k = 10 - i
}
console.log(`i: ${i}, k: ${k}`)

// 结果：
// i: 3, k: 8Copy
```

相当于

```
var i = 0
var k
for (; i < 3; ) {
  k = 10 - i
  i++
}
```





let则有新的作用域：

```
for (var i = 0; i < 3; i++) {
  ;(_i => {
    setTimeout(() => console.log(_i), 0)
    i = _i
  })(i)
}Copy
```

> 附：这里吾辈是根据 babel 编译的结果修改而来。而且 babel 真的很聪明，当迭代变量 i 没有更新时，就不会使用 `_i` 进行区分呢！









#### 面试题：

### let + for

再看下面这段代码，可以对其进行分解

```
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0)
}Copy
```

1. 创建 for 循环，表达式中存在 let 变量，for 将会创建一个块级作用域（ES6 let 专用）
2. 每次迭代时，会创建一个子块级作用域，迭代变量 i 也会重新生成
3. 对 i 的任何操作，都会被记住并赋值给下一次的迭代

> 块级作用域只对 let 有效，var 声明的变量仍然能在 for 循环外使用，证明 for 循环并不是像函数作用域那样是连 var 都能封闭的作用域。

图解如下

[![let + for 图解](https://img.rxliuli.com/20181227212650.png)](https://img.rxliuli.com/20181227212650.png)

### var + for

分析一下

```
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0)
}Copy
```

1. 进入 for 循环
2. 在这里创建了迭代变量 i，因为是函数作用域变量所以在 for 循环外可以访问，被提升到了函数作用域顶部声明
3. setTimeout 函数执行，闭包绑定函数作用域外部变量 i，在循环结束输出 i 的值 3
4. 继续迭代

[![var + for 图解](https://img.rxliuli.com/20181227213014.png)](https://img.rxliuli.com/20181227213014.png)

------

所以以后如果可能，还是要拥抱这些新特性呢！那么，关于 `let/var` 在 `for` 循环中的区别就到这里啦