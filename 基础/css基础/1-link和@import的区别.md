[参考](https://juejin.im/post/6844903796686979086)



#### 区别

**1.从属关系区别**

@import是 CSS 提供的语法规则，只有导入样式表的作用；link是HTML提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。rel属性表示加载的资源和文档的关系，例如rel="stylesheet"/rel="ion"分别代表加载的资源是样式和标题图标，还有media属性作用于媒体查询，即符合某种条件才会把该资源加载下来。（[rel参考](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link)）

**2.加载顺序区别**

加载页面时，link标签引入的 CSS 被同时加载；@import引入的 CSS 将在页面加载完毕后被加载。

**3.兼容性区别**

@import是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link标签作为 HTML 元素，不存在兼容性问题。

**4.DOM可控性区别**

可以通过 JS 操作 DOM ，插入link标签来改变样式；由于 DOM 方法是基于文档的，无法使用@import的方式插入样式。

**5.权重区别**

link引入的样式权重大于@import引入的样式。

同等权重CSS样式的优先级由高到低的排序是：行内样式、内联样式、外联样式、导入样式 。如果外联样式和导入样式都有一个div{color:XX},最终的div样式是外联样式中所定义div样式 。







#### 引入方式

```
<link  rel="stylesheet"  href="../css/123.css" />

<style type="text/css">   

    @import url("css/green.css");

</style>
```







#### 应用场景

总的来说，最好不要使用improt导入式，如果import加载的样式比较大，容易出现加载延迟，甚至有闪屏的情况。就目前来看，小型的网站还是推荐使用link导入，当然如果将来我们需要把CSS进行模块化管理，那会用到@import，这个还需要看情况的。

