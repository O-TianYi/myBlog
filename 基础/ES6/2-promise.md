**说说你对 promise 的了解**

答案：Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件监听——更合理和更强大。

所谓 Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

Promise 对象有以下两个特点:

1. 对象的状态不受外界影响，Promise 对象代表一个异步操作，有三种状态：Pending（进行中）、Resolved（已完成，又称 Fulfilled）和 Rejected（已失败）
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果let







**Promise.all并发限制**,**介绍下 Promise.all 使用、原理实现及错误处理**

[参考](https://juejin.im/post/6844903761505173512)

`Promise.all` 接收一个 `promise` 对象的数组作为参数，当这个数组里的所有 `promise` 对象全部变为`resolve`或 有 `reject` 状态出现的时候，它才会去调用 `.then` 方法,它们是并发执行的。(总结就是参数中的promise实例数组都是resolve的时候才会执行then，否则进入catch方法)

```
var p1 = Promise.resolve(1),
    p2 = Promise.resolve(2),
    p3 = Promise.resolve(3);
Promise.all([p1, p2, p3]).then(function (results) {
    console.log(results);  // [1, 2, 3]
});

var p1 = Promise.resolve(1),
    p2 = Promise.reject(2),
    p3 = Promise.resolve(3);
Promise.all([p1, p2, p3]).then(function (results) {
    //then方法不会被执行
    console.log(results);
}).catch(function (e){
    //catch方法将会被执行，输出结果为：2
    console.log(2);
});
```

### 总结 promise.all 的特点

1、接收一个 `Promise` 实例的数组或具有 `Iterator` 接口的对象，

2、如果元素不是 `Promise` 对象，则使用 `Promise.resolve` 转成 `Promise` 对象

3、如果全部成功，状态变为 `resolved`，返回值将组成一个数组传给回调

4、只要有一个失败，状态就变为 `rejected`，返回值将直接传递给回调
`all()` 的返回值也是新的 `Promise` 对象




















**设计并实现 Promise.race()**

