```
p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。
p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。
:enabled、:disabled 控制表单控件的禁用状态。
:checked，单选框或复选框被选中。

```





##### 重点：

[参考]([https://www.zhangxinxu.com/wordpress/2011/06/css3%E9%80%89%E6%8B%A9%E5%99%A8nth-child%E5%92%8Cnth-of-type%E4%B9%8B%E9%97%B4%E7%9A%84%E5%B7%AE%E5%BC%82/](https://www.zhangxinxu.com/wordpress/2011/06/css3选择器nth-child和nth-of-type之间的差异/))

**伪类和伪元素的区别 **

```
1、伪元素使用 2 个冒号，常见的有：::before，::after，::first-line，::first-letter，::selection、::placeholder 等；
  伪类使用1个冒号，常见的有：:hover，:link，:active，:target，:not()，:focus等。
2、伪元素添加了一个页面中没有的元素（只是从视觉效果上添加了，不是在文档树中添加）；
  伪类是给页面中已经存在的元素添加一个类。
```

**a标签的伪类声明顺序**

```
 L-V-H-A（link,visited,hover,active）
不按照顺序会出现的问题：超链接访问过后 hover 样式就不出现
原因：被点击访问过的超链接样式不在具有 hover 和 active 了
```

**nth-child和nth-of-type区别**

```
p:nth-child(2)  选择属于其父元素的第二个子元素。
p:nth-of-type(2)  选择属于其父元素的第二个段落子元素。

主要区别就是：
nth-child就单单是p的父元素的第二个子元素，可以是任何标签类型。
nth-of-type就必须是父元素中的第二个类型为p的子元素。
例如：
<section>
    <div>我是一个普通的div标签</div>
    <p>我是第1个p标签</p>----nth-child作用标签
    <p>我是第2个p标签</p>----nth-of-type作用标签
</section>
p:nth-of-type(2) { color: red; }
p:nth-child(2) { color: red; }
```

注意：jquery不支持nth-of-type选择器，如果需要则需要引入[插件](https://github.com/keithclark/JQuery-Extended-Selectors)。

**我使用的场景：**让中间元素使用margin值来实现两端对齐的效果时候需要用到。









**CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3 新增伪类有那些？**

答案：

```
        1.id选择器（ # myid）

        2.类选择器（.myclassname）

        3.标签选择器（div, h1, p）

        4.相邻选择器（h1 + p）

        5.子选择器（ul < li）

        6.后代选择器（li a）

        7.通配符选择器（ * ）

        8.属性选择器（a[rel = "external"]）

        9.伪类选择器（a: hover, li: nth - child）

    *   可继承： font-size font-family color, UL LI DL DD DT;

    *   不可继承 ：border padding margin width height ;

    *   优先级就近原则，样式定义最近者为准;

    *   载入样式以最后载入的定位为准;

优先级为:

       !important >  id > class > tag  

       important 比 内联优先级高

CSS3新增伪类举例：

    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。

    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。

    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。

    p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。

    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。

    :enabled、:disabled 控制表单控件的禁用状态。

    :checked，单选框或复选框被选中。
```