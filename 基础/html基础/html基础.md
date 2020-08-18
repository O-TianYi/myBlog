**1.简述一下你对 HTML 语义化的理解？**

正确的标签做正确的事情、内容结构化、结构清晰、利于SEO、便于阅读维护理解。



**2.Label 的作用是什么？是怎么用的？**

答案：label 标签来定义表单控制间的关系,**当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上**。

解析：两种用法：**一种是 id 绑定，一种是嵌套**

```
<label for="Name">Number:</label>

<input type=“text“name="Name" id="Name"/>

<label>Date:<input type="text" name="B"/></label>
```







**DOM 和 BOM 有什么区别**

答案：

- DOM

Document Object Model，文档对象模型

DOM 是为了操作文档出现的 API，document 是其的一个对象

DOM 和文档有关，这里的文档指的是网页，也就是 html 文档。DOM 和浏览器无关，他关注的是网页本身的内容。

- BOM

Browser Object Model，浏览器对象模型

BOM 是为了操作浏览器出现的 API，window 是其的一个对象

window 对象既为 javascript 访问浏览器提供 API，同时在 ECMAScript 中充当 Global 对象![BOM结构图](../../../../../../Documents/%E7%AC%94%E8%AE%B0%E5%9B%BE/%E5%9B%BE/BOM%E7%BB%93%E6%9E%84%E5%9B%BE.png)





**DOM Tree是如何构建的？**

答案：

1. HTML 解释器

HTML 解释器的工作就是将网络或者本地磁盘获取的 HTML 网页和资源从字节流解释成 DOM 树结构。

1. JavaScript 的执行

在 HTML 解释器的工作过程中，可能会有 JavaScript 代码需要执行，它发生在将字符串解释成词语之后、创建各种节点的时候。这也是为什么全局执行的 JavaScript 代码不能访问 DOM 的原因——因为 DOM 树还没有被创建完呢。

![浏览器渲染引擎流程](../../../../../../Documents/%E7%AC%94%E8%AE%B0%E5%9B%BE/%E5%9B%BE/%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93%E5%BC%95%E6%93%8E%E6%B5%81%E7%A8%8B.png)![js阻塞和css阻塞](../../../../../../Documents/%E7%AC%94%E8%AE%B0%E5%9B%BE/%E5%9B%BE/js%E9%98%BB%E5%A1%9E%E5%92%8Ccss%E9%98%BB%E5%A1%9E.png)





**meta viewport 原理是什么？**

答案：

meta viewport 标签的作用是让当前 viewport 的宽度等于设备的宽度，同时不允许用户进行手动缩放

viewport的原理：移动端浏览器通常都会在一个比移动端屏幕更宽的虚拟窗口中渲染页面，这个虚拟窗口就是 viewport; 目的是正常展示没有做移动端适配的网页，让他们完整的展示给用户；

解析：

Viewport ：字面意思为视图窗口，在移动 web 开发中使用。表示将设备浏览器宽度虚拟成一个特定的值（或计算得出），这样利于移动 web 站点跨设备显示效果基本一致。移动版的 Safari 浏览器最新引进了 viewport 这个 meta tag，让网页开发者来控制 viewport 的大小和缩放，其他手机浏览器也基本支持。

在移动端浏览器当中，存在着两种视口，一种是可见视口（也就是我们说的设备大小），另一种是视窗视口（网页的宽度是多少）。 举个例子：如果我们的屏幕是 320 像素 * 480 像素的大小（iPhone4），假设在浏览器中，320 像素的屏幕宽度能够展示 980 像素宽度的内容。那么 320 像素的宽度就是可见视口的宽度，而能够显示的 980 像素的宽度就是视窗视口的宽度。

为了显示更多的内容，大多数的浏览器会把自己的视窗视口扩大，简易的理解，就是让原本 320 像素的屏幕宽度能够容下 980 像素甚至更宽的内容（将网页等比例缩小）。![viewport参数](https://raw.githubusercontent.com/O-TianYi/picture/master/img/20200818103831.png)







**Canvas 和 SVG 有什么区别？**

答案：Canvas 和 SVG 都允许您在浏览器中创建图形，但是它们在根本上是不同的。

## Canvas

描述：

通过 Javascript 来绘制 2D 图形。 是逐像素进行渲染的。 其位置发生改变，会重新进行绘制。

## SVG

描述：

一种使用 XML 描述的 2D 图形的语言 SVG 基于 XML 意味着，SVG DOM 中的每个元素都是可用的，可以为某个元素附加 Javascript 事件处理器。 在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

## 比较

Canvas

- 依赖分辨率
- 不支持事件处理器
- 弱的文本渲染能力
- 能够以 .png 或 .jpg 格式保存结果图像
- 最适合图像密集型的游戏，其中的许多对象会被频繁重绘

SVG

- 不依赖分辨率
- 支持事件处理器
- 最适合带有大型渲染区域的应用程序（比如谷歌地图）
- 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）
- 不适合游戏应用









**html5 有哪些新特性、移除了那些元素？**

答案：

新特性：

1. 拖拽释放(Drag and drop) API
2. 语义化更好的内容标签（header,nav,footer,aside,article,section）
3. 音频、视频 API(audio,video)
4. 画布(Canvas) API
5. 地理(Geolocation) API
6. 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
7. sessionStorage 的数据在浏览器关闭后自动删除
8. 表单控件，calendar、date、time、email、url、search
9. 新的技术 webworker, websocket, Geolocation

移除的元素：

1. 纯表现的元素：basefont，big，center，font, s，strike，tt，u；
2. 对可用性产生负面影响的元素：frame，frameset，noframes；

支持 HTML5 新标签：

- IE8/IE7/IE6 支持通过 document.createElement 方法产生的标签， 可以利用这一特性让这些浏览器支持 HTML5 新标签， 浏览器支持新标签后，还需要添加标签默认的样式：
- 当然最好的方式是直接使用成熟的框架、使用最多的是 html5shim 框架

```
<!--[if lt IE 9]>
  <script>
    src = "http://html5shim.googlecode.com/svn/trunk/html5.js";
  </script>
<![endif]-->
```







**前端需要注意哪些 SEO**

答案：

1. 合理的 title、description、keywords：搜索对着三项的权重逐个减小，title 值强调重点即可，重要关键词出现不要超过 2 次，而且要靠前，不同页面 title 要有所不同；description 把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面 description 有所不同；keywords 列举出重要关键词即可
2. 语义化的 HTML 代码，符合 W3C 规范：语义化代码让搜索引擎容易理解网页
3. 重要内容 HTML 代码放在最前：搜索引擎抓取 HTML 顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
4. 重要内容不要用 js 输出：爬虫不会执行 js 获取内容
5. 少用 iframe：搜索引擎不会抓取 iframe 中的内容
6. 非装饰性图片必须加 alt
7. 提高网站速度：网站速度是搜索引擎排序的一个重要指标

解析：[参考](https://www.cnblogs.com/passkey/p/10081589.html)









**title 与 h1 的区别、b 与 strong 的区别、i 与 em 的区别？**

答案：

```
①title用于网站信息标题，突出网站标题或关键字，一个网站可以有多个title，seo权重高于H1；H1概括的是文章主题，一个页面最好只用一个H1，seo权重低于title。


解析：

A.从网站角度而言，title则重于网站信息标题，突出网站标题或关键字用title，一篇文章，一个页面最好只

用一个H1，H1用得太多，会稀释主题；一个网站可以有多个title，最好一个单页用一个title以便突出网站页面

主题信息。

B.从文章角度而言，H1则概括的是文章主题，突出文章主题，用H1，面对的用户，要突出其视觉效果。

C.从SEO角度而言，title的权重高于H1，其适用性要比H1广。


②b为了加粗而加粗，strong为了标明重点而加粗


解析：

A.b这个标签对应 bold，即文本加粗，其目的仅仅是为了加粗显示文本，是一种样式／风格需求；

B.strong这个标签意思是加强字符的语气，表示该文本比较重要，提醒读者／终端注意。为了达到这个目的，浏览器等终端将其加粗显示；


③ 同②i为了斜体而斜体，em为了标明重点而斜体，且对于搜索引擎来说strong和em比b和i要重视的多
```