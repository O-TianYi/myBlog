**CSS 清除浮动的几种方法（至少两种）**

[更加详细参考](https://juejin.im/post/6844903504545316877)

答案：

```
清除浮动： 核心：clear:both;

1.使用额外标签法（不推荐使用）

在浮动的盒子下面再放一个标签，使用 clear:both;来清除浮动

a 内部标签：会将父盒子的高度重新撑开

b 外部标签：只能将浮动盒子的影响清除，但是不会撑开盒子

2.使用 overflow 清除浮动（不推荐使用）

先找到浮动盒子的父元素，给父元素添加一个属性：overflow:hidden;就会清除子元素对页面的影响

3.使用伪元素清除浮动(用的最多)

伪元素：在页面上不存在的元素，但是可以通过 css 添加上去

种类：
      :after(在。。。之后)
      :before(在。。。之前)

注意：每个元素都有自己的伪元素
在父元素中添加该类，后者直接在父元素的类上使用伪元素来实现。
.clearfix:after {
    content:"";
    height:0;
    line-height:0;
    display:block;
    clear:both;
    visibility:hidden;  /_将元素隐藏起来_/ 
      在页面的 clearfix 元素后面添加了一个空的块级元素
     （这个元素的高为 0 行高也为 0   并且这个元素清除了浮动）
}
.clearfix {
  zoom:1;/_为了兼容 IE6_/
}
```

方法三例子：（其实就是第一种方法的变形，原理都是一样）

```
HTML结构如下，为了惯例相符，在.topDiv的div上再添加一个clearfix类：
<div class="topDiv clearfix">
    <div class="textDiv">...</div>
    <div class="floatDiv">float left</div>
</div>
<div class="bottomDiv">...</div>复制代码样式应用如下：
// 省略基本的样式
// 区别在这里
.clearfix:after {
    content: '.';
    height: 0;
    display: block;//和方法一一样必须为块级元素
    clear: both;
}

复制代码该样式在clearfix，即父级元素的最后，添加了一个:after伪元素，通过清除伪元素的浮动，达到撑起父元素高度的目的。注意到该伪元素的display值为block，即，它是一个不可见的块级元素（有的地方使用table，因为table也是一个块级元素）。你可能已经意识到，这也只不过是前一种清除浮动方法（添加空白div）的另一种变形，其底层逻辑也是完全一样的。前面的三种方法，其本质上是一样的。
```







**BFC**

答案：

- 什么是 BFC

  BFC（Block Formatting Context）格式化上下文，是 Web 页面中盒模型布局的 CSS 渲染模式，指一个独立的渲染区域或者说是一个隔离的独立容器。

- 形成 BFC 的条件

  - 浮动元素，float 除 none 以外的值
  - 定位元素，position（absolute，fixed）
  - display 为以下其中之一的值 inline-block，table-cell，table-caption
  - overflow 除了 visible 以外的值（hidden，auto，scroll）

- BFC 的特性

  - 内部的 Box 会在垂直方向上一个接一个的放置。
  - 垂直方向上的距离由 margin 决定
  - bfc 的区域不会与 float 的元素区域重叠。
  - 计算 bfc 的高度时，浮动元素也参与计算
  - bfc 就是页面上的一个独立容器，容器里面的子元素不会影响外面元素。







##### 补充

**设置元素浮动后，浮动元素的display为block，测试显示的是block。更准确的说像inline-block，因为设置成类似`float：left`的元素会同时拥有行内和块级的特性，最明显的不同是它的默认宽度不是 100%，行内元素默认 100%宽度占据一行，并且设置 的padding-top 和 padding-bottom 或者 width、height 都是有效果的。**

line元素设置的padding-top和padding-bottom，margin-top和margin-bottom都是不起作用的。

