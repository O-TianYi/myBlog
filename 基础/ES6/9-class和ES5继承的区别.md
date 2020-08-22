[参考](https://juejin.im/post/6844903895362338824)



1、class 声明会提升，但不会初始化赋值。Foo进入暂时性死区，类似let、const声明变量

2、class 声明内部会启用严格模式

3、class 的所有方法（包括静态方法和实例方法）都是不可枚举的。

4、calss 所有方法（包括静态方法和实例方法）都没有原型对象prototype，所以也没有[[construct]]，不能使用new来调用。

5、必须使用new调用class。

6、class 内部无法重写类名。