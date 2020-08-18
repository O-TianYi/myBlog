**rgba()和 opacity 的透明效果有什么不同？**

答案：

rgba()和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有内容的透明度，

而 rgba()只作用于元素的颜色或其背景色。（设置 rgba 透明的元素的子元素不会继承透明效果！），一般color设置的字体颜色是可以被子元素实现继承，而使用rgba来设置的color是不会被子元素继承该透明效果的。







**CSS 隐藏元素的几种方法（至少说出三种）**

答案：

Opacity:元素本身依然占据它自己的位置并对网页的布局起作用。它也将响应用户交互;

Visibility:与 opacity 唯一不同的是它不会响应任何用户交互。此外，元素在读屏软件中也会被隐藏;

Display:display 设为 none 任何对该元素直接打用户交互操作都不可能生效。此外，读屏软件也不会读到元素的内容。这种方式产生的效果就像元素完全不存在;

Position:不会影响布局，能让元素保持可以操作;

Clip-path:clip-path 属性还没有在 IE 或者 Edge 下被完全支持。如果要在你的 clip-path 中使用外部的 SVG 文件，浏览器支持度还要低;







**display:none 与 visibility:hidden 的区别是什么？**

答案：

display : 隐藏对应的元素但不挤占该元素原来的空间。

visibility: 隐藏对应的元素并且挤占该元素原来的空间。

即是，使用 CSS display:none 属性后，HTML 元素（对象）的宽度、高度等各种属性值都将“丢失”;而使用 visibility:hidden 属性后，HTML 元素（对象）仅仅是在视觉上看不见（完全透明），而它所占据的空间位置仍然存在。

更深入的回答：

display:none是底层原理是：会在dom树生成dom节点，只是会在render tree不会生成渲染节点，回触发回流。

v-if：是动态删除和增加dom树的元素

