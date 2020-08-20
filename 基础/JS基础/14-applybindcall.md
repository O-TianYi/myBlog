**bind、call、apply 的区别**

答案：

call 和 apply 其实是一样的，区别就在于传参时参数是一个一个传或者是以一个数组的方式来传。
call 和 apply 都是在调用时生效，改变调用者的 this 指向。

```
let name = 'Jack'
const obj = {name: 'Tom'}
function sayHi() {console.log('Hi! ' + this.name)}

sayHi() // Hi! Jack
sayHi.call(obj) // Hi! Tom
```

bind 也是改变 this 指向，不过不是在调用时生效，而是返回一个新函数。

```
const newFunc = sayHi.bind(obj)
newFunc() // Hi! Tom
```







**call() 和 apply() 的含义和区别？**

答案：

首先说明两个方法的含义：

- call：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.call(A, args1,args2);即 A 对象调用 B 对象的方法。
- apply：调用一个对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即 A 对象应用 B 对象的方法。

call 与 apply 的相同点：

- 方法的含义是一样的，即方法功能是一样的；
- 第一个参数的作用是一样的；

call 与 apply 的不同点：两者传入的列表形式不一样

- call 可以传入多个参数；
- apply 只能传入两个参数，所以其第二个参数往往是作为数组形式传入



补充：

call的性能要比apply要好。在jquery源码的时候有看到在源码的注释中有标注过call性能比apply要好。个人理解是内部少了一次将apply第二个参数解构的操作



[实现原理参考](https://juejin.im/post/6844903782803832845#heading-12)







#### 重要补充

**一旦函数通过bind绑定了有效的this指向，那么在函数执行过程中this会指向该对象，即使在使用call，bind也不能改变this的指向。**

原因：在bind调用的时候this，在内部把对象指向了函数的this，然后在return的方法中使用闭包的形式来调用该this，所以不能改变bind绑定的this。即如下bind 的简单实现原理：

```
Function.prototype.bind = function(context) {
   let _me = this
    return function() {
        return _me.apply(context)
    }
}
```

