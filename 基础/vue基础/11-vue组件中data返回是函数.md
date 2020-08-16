**Vue 组件中 data 为什么必须是函数**

答案：

在 new Vue() 中，data 是可以作为一个对象进行操作的，然而在 component 中，data 只能以函数的形式存在，不能直接将对象赋值给它，这并非是 Vue 自身如此设计，而是跟 JavaScript 特性相关，我们来回顾下 JavaScript 的原型链

```
var Component = function() {};
Component.prototype.data = {
  message: "Love"
};
var component1 = new Component(),
  component2 = new Component();
component1.data.message = "Peace";
console.log(component2.data.message); // Peace
```

以上**两个实例都引用同一个原型对象，当其中一个实例属性改变时，另一个实例属性也随之改变，只有当两个实例拥有自己的作用域时，才不会互相干扰** ！！！！！这句是重点！！！！！

```
var Component = function() {
  this.data = this.data();
};
Component.prototype.data = function() {
  return {
    message: "Love"
  };
};
var component1 = new Component(),
  component2 = new Component();
component1.data.message = "Peace";
console.log(component2.data.message); // Love
```