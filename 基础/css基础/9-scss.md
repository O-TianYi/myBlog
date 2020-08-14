#### scss安装

**预处理器的优缺点：**

**优点**

+ 提高css可维护性
+ 易于编写嵌套选择器
+ 引入变量，增添主题功能
+ 通过混合（Mixins）生成重复的css

**缺点**

+ 需要预处理loader

+ 重新编译的时间可能会很慢

+ less的变量名称以@作为前缀，容易与css关键字混淆，如@media、@import

  



 ##### 准备工作

```
npm install css-loader style-loader --save-dev
npm install node-sass sass-loader --save-dev
```

webpack.config.js添加loader：

```
const path = require("path");
const {VueLoaderPlugin} = require('vue-loader');
module.exports = {
    entry: './webapp/App.js',
    output: {
        filename: 'App.js',
        path: path.resolve(__dirname, './dist')
    },
	module: {
		rules: [
            {
                test: /\.scss/,
                use: ['style-loader', 'css-loader','sass-loader']
            },
			{
				test: /\.vue$/,
				use: 'vue-loader'
			}
		]
	},
	plugins: [
		new VueLoaderPlugin()
	],
	mode: "production"
}
```



##### 正式开始

+ 使用变量

  ```
  $border-color:#aaa; //声明变量
  .container {
  $border-width:1px;
      border:$border-width solid $border-color; //使用变量
  }
  
  //编译后就是：
  .container {
      border:1px solid #aaa; //使用变量
  }
  
  又或者
  $border-color:#aaa; //声明变量
  $border_color:#ccc;
  .container {
      $border-width:1px;
      border:$border-width solid $border-color; //使用变量
  }
  编译后的CSS
  .container {
      border:1px solid #ccc; //使用变量
  }
  ```

+ 嵌套规则

  ```
  /*scss*/
  .container ul {
      border:1px solid #aaa;
      list-style:none;
      
      li {
          float:left;
      }
      
      li>a {
          display:inline-block;
          padding:6px 12px;
      }
      
      &:after {
          display:block;
          content:"";
          clear:both;
      }
  }
  
  或者更简单的：
  li {
      float:left;
  
      >a {
          display:inline-block;
          padding:6px 12px;
      }
  }
  
  又或者：
  li >{ 
      a {
          display:inline-block;
          padding:6px 12px;
      }
  }
  ```

+ 混合器（相当于公共代码的提取）

  + 定义(@mixin)

  ```
  //重复代码片段提取复用
  @mixin border-radius{
      -moz-border-radius: 5px;
      -webkit-border-radius: 5px;
      border-radius: 5px;
      color:red;
  }
  
  //以函数的形式传递参数
  @mixin get-border-radius($border-radius,$color){
      -moz-border-radius: $border-radius;
      -webkit-border-radius: $border-radius;
      border-radius: $border-radius;
      color:$color;
  }
  
  //设置默认值
  @mixin get-border-radius($border-radius:5px,$color:red){
      -moz-border-radius: $border-radius;
      -webkit-border-radius: $border-radius;
      border-radius: $border-radius;
      color:$color;
  }
  ```

  + 使用(@include)

    ```
    .container {
        border:1px solid #aaa;
        @include get-border-radius;         //不传参则为默认值5px
        @include get-border-radius(10px,blue);   //传参
    }
    /*多个参数时，传参指定参数的名字，可以不用考虑传入的顺序*/
    .container {
        border:1px solid #aaa;
        @include get-border-radius;         //不传参则为默认值5px
        @include get-border-radius($color:blue,$border-radius:10px);   //传参
    }
    ```

  + 使用混合器定义和直接使用class来定义的异同：class定义的样式需要在html文件中使用，而混合器就不需要在html文件中使用class就可以达到复用的效果。
  + 混合器中可以使用一切scss代码。

+ 继承

  + 定义（%）

  ```
  %border-style {
    border:1px solid #aaa;
    -moz-border-radius: 5px;
    -webkit-border-radius: 5px;
    border-radius: 5px;
  }
  ```

  注意：使用%定义一个被继承的样式，本事不起作用，只用于被人继承，类似于抽象类。

  + 继承使用（@extend）

  ```
  container {
  	@extend %border-style;
  	color:red;
  }
  .container1 {   //继承另一个选择器
  	@extend .container;
  }
  ```

  

+ 导入scss文件

  ```
  /*App1.scss*/
  $border-color:#aaa; //声明变量
  @import App2.scss;  //引入另一个SCSS文件
  .container {
      border:1px solid $border-color; //使用变量
  }
  /*App2.scss*/
  $border-color:#ccc !default; //声明变量
  
  /*生成的css文件*/
  .container {
      border:1px solid #aaa; //使用变量
  }
  
  导入的文件App2.scss只在文件中不存在$border-color时起作用，若App1.scss中已经存在了$border-color变量，则App2.scss中的$border-color不生效
  !default只能使用与变量中。
  ```

  

  