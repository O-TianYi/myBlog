![vue生命周期](https://raw.githubusercontent.com/O-TianYi/picture/master/img/20200816151840.jpg)

（1） beforeCreate 初始化实例后 数据观测和事件配置之前调用，相关的render函数被首次调用，插件的混入，响应式数据的绑定(初始化界面前)

（2） created 实例创建完成后调用，初始化data,props,methods,computed和watch（初始化界面后）

（3） beforeMount 挂载开始前被用（渲染dom前）

（4） mounted el 被新建 vm.$el 替换并挂在到实例上之后调用，实例化wathcer，渲染dom（渲染dom后）

（5） beforeUpdate 数据更新时调用（更新数据前）

（6） updated 数据更改导致的 DOM 重新渲染后调用，检查当前的watcher列表中，是否存在当前要更新数据的watcher，存在则执行该生命周期（更新数据后）

（7） beforeDestory 实例被销毁前调用（卸载组件前）

（8） destroyed 实例销毁后调用（卸载组件后）







注意点：

+ 只有vm.$mount("#app")执行了才会有真实的dom，而render执行的时候只是返回一个VNode，只有$mount方法执行了，才会有真实的dom，才会在vm上挂载真实的dom,即vm.$el。即没有挂载#app这个div就不会有beforeMounted和该钩子函数后的生命周期函数。
+ new Vue的时候会优先使用template属性的div，没有才会使用el上的div。并且render函数的优先级最高，即三者同时存在的时候，render函数>template属性>外部html（el属性定义的）

+ vue的所有生命周期函数都是自动绑定在this的上下文中，所以不能使用箭头函数，即钩子函数不能写为`create:()=>{}`形式。

+ 不要在钩子函数使用箭头函数`created: () => console.log(this.a)`，因为箭头函数没有this，会作为变量一直向上级词法作用域查找，经常会导致出现``Uncaught TypeError: Cannot read property of undefined` 或 `Uncaught TypeError: this.myMethod is not a function` 之类的错误。`正确写法有：

  ```
  created: function () {
      // `this` 指向 vm 实例
      console.log('a is: ' + this.a)
  }
  
  create(){
  ..
  }
  ```

  

