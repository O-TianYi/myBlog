

##### src和href的区别

src会用引入资源替换当前元素，href是在当前页面和引用资源之间建立联系。

+ href一般在link和a标签上使用。当文档中解析到href的时候，不会暂停对当前文档的处理，而是并行把引用资源下载。这就是为什么使用link引入比@import引入的好处。
+ src一般在img，script，iframe等标签元素上，当文档解析到src（除了图片不会暂停其他资源下载和处理）的时候，会暂停其他资源的下载和处理，直到该资源加载、编辑、执行完成。这就是为什么建议把js脚本放在底部而不是头部的原因。



**12.列举 IE 与其他浏览器不一样的特性？**

a. IE 的排版引擎是 Trident （又称为 MSHTML）

b. Trident 内核曾经几乎与 W3C 标准脱节（2005 年）

c. Trident 内核的大量 Bug 等安全性问题没有得到及时解决

d. JS 方面，有很多独立的方法，例如绑定事件的 attachEvent、创建事件的 createEventObject 等

e. CSS 方面，也有自己独有的处理方式，例如设置透明，低版本 IE 中使用滤镜的方式

区别：

总体会有布局、样式解析和脚本执行三个方面的区别。

盒模型：在 W3C 标准中，如果设置一个元素的宽度和高度，指的是元素内容的宽度和高度，而在 Quirks 模式下，IE 的宽度和高度还包含了 padding 和 border。

设置行内元素的高宽：在 Standards 模式下，给`<span>`等行内元素设置 wdith 和 height 都不会生效，而在 quirks 模式下，则会生效。

设置百分比的高度：在 standards 模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置百分比的高度，子元素设置一个百分比的高度是无效的

用 margin:0 auto 设置水平居中：使用 margin:0 auto 在 standards 模式下可以使元素水平居中，但在 quirks 模式下却会失效。



**19. 你能描述一下渐进增强和优雅降级之间的不同吗?**



答案：

渐进增强  progressive enhancement：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

（一开始保证最基本的功能，再改进和追加功能）

优雅降级  graceful degradation：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

（一开始就构建完整的功能，再针对低版本浏览器进行兼容。）

区别：优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要。降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带。





**22. html 常见兼容性问题？**

答案：

1.双边距 BUG float 引起的，解决办法: 使用 display解决

2.3 像素问题 使用 float 引起的，解决办法: 使用 dislpay:inline -3px

3.超链接 hover 点击后失效，解决办法: 使用正确的书写顺序 link visited hover active

4.Ie z-index 问题，解决办法: 给父级添加 position:relative

5.Png 透明 ，解决办法: 使用 js 代码

6.Min-height 最小高度 ，解决办法: ！Important 解决

7.select 在 ie6 下遮盖，解决办法: 使用 iframe 嵌套

8.为什么没有办法定义 1px 左右的宽度容器，解决办法: （IE6 默认的行高造成的，使用 over:hidden,zoom:0.08 line-height:1px）

9.IE5-8 不支持 opacity，解决办法：

```
.opacity {
  opacity: 0.4;
  filter: alpha(opacity=60); /_ for IE5-7 _/
  -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=60)"; /_ for IE 8_/
}
```

10.IE6 不支持 PNG 透明背景，解决办法: IE6 下使用 gif 图片



**25.前端需要注意哪些 SEO**



答案：

1. 合理的 title、description、keywords：搜索对着三项的权重逐个减小，title 值强调重点即可，重要关键词出现不要超过 2 次，而且要靠前，不同页面 title 要有所不同；description 把页面内容高度概括，长度合适，不可过分堆砌关键词，不同页面 description 有所不同；keywords 列举出重要关键词即可
2. 语义化的 HTML 代码，符合 W3C 规范：语义化代码让搜索引擎容易理解网页
3. 重要内容 HTML 代码放在最前：搜索引擎抓取 HTML 顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取
4. 重要内容不要用 js 输出：爬虫不会执行 js 获取内容
5. 少用 iframe：搜索引擎不会抓取 iframe 中的内容
6. 非装饰性图片必须加 alt
7. 提高网站速度：网站速度是搜索引擎排序的一个重要指标