#### 兼容性(Can I use)

(参考)[http://www.wzsky.net/Website/css/140565.html]

- -moz代表firefox浏览器私有属性
- -ms代表IE浏览器私有属性
- -webkit代表chrome、safari私有属性
- -o代表opera私有属性

**书写顺序：**

 对于私有属性的顺序要注意，把标准写法放到最后，兼容性写法放到前面 

```
 -webkit-transform:rotate(-3deg); /*为Chrome/Safari*/ 
 -moz-transform:rotate(-3deg); /*为Firefox*/ 
 -ms-transform:rotate(-3deg); /*为IE*/ 
 -o-transform:rotate(-3deg); /*为Opera*/ 
 transform:rotate(-3deg);
```

##### 简化浪费生命的兼容性写法：（自动化插件 Autoprefixer ）

 把Autoprefixer添加到资源构建工具（例如Grunt, webpack ）后，可以完全忘记有关CSS前缀的东西，只需按照最新的W3C规范来正常书写CSS即可 。

例子：

```
//我们编写的代码 
div { 
 transform: rotate(30deg); 
} 
 
// 自动补全的代码，具体补全哪些由要兼容的浏览器版本决定，可以自行设置 
div { 
 -ms-transform: rotate(30deg); 
 -webkit-transform: rotate(30deg); 
 -o-transform: rotate(30deg); 
 -moz-transform: rotate(30deg); 
 transform: rotate(30deg); 
}
```





#### Jquery解决的兼容性问题

解决的兼容性问题为各个浏览器触发的不一样问题

