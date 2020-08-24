![vue生命周期](https://raw.githubusercontent.com/O-TianYi/picture/master/img/20200816151840.jpg)

1） beforeCreate 初始化实例后 数据观测和事件配置之前调用

（2） created 实例创建完成后调用

（3） beforeMount 挂载开始前被用

（4） mounted el 被新建 vm.$el 替换并挂在到实例上之后调用

（5） beforeUpdate 数据更新时调用

（6） updated 数据更改导致的 DOM 重新渲染后调用

（7） beforeDestory 实例被销毁前调用

（8） destroyed 实例销毁后调用







注意点：

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

  

