**script标签的 defer 和 asnyc 属性的作用以及二者的区别？**

答案：

- 1、defer 和 async 的网络加载过程是一致的，都是异步执行。
- 2、区别在于加载完成之后什么时候执行，可以看出 defer 是文档所有元素解析完成之后才执行的。
- 3、如果存在多个 defer 脚本，那么它们是按照顺序执行脚本的，而 async，无论声明顺序如何，只要加载完成就立刻执行

解析：

无论`<script>`标签是嵌入代码还是引用外部文件，只要不包含 defer 属性和 async 属性（这两个属性只对外部文件有效），浏览器会按照`<script>`的出现顺序对他们依次进行解析，也就是说，只有在第一个`<script>`中的代码执行完成之后，浏览器才会执行第二个`<script>`中的代码，并且在解析时，页面的处理会暂时停止。

嵌入代码的解析=执行 外部文件的解析=下载+执行

script 标签存在两个属性，defer 和 async，这两个属性只对外部文件有效

## 只有一个脚本的情况

```
<script src="a.js" />
```

没有 defer 或 async 属性，浏览器会立即下载并执行相应的脚本，并且在下载和执行时页面的处理会停止。

```
<script defer src="a.js" />
```

有了 defer 属性，浏览器会立即下载相应的脚本，在下载的过程中页面的处理不会停止，等到文档解析完成脚本才会执行。

```
<script async src="a.js" />
```

有了 async 属性，浏览器会立即下载相应的脚本，在下载的过程中页面的处理不会停止，下载完成后立即执行，执行过程中页面处理会停止。

```
<script defer async src="a.js" />
```

如果同时指定了两个属性,则会遵从 async 属性而忽略 defer 属性。

下图可以直观的看出三者之间的区别:

[![js_002](https://github.com/O-TianYi/web-interview/raw/master/images/js_002.png)](https://github.com/O-TianYi/web-interview/blob/master/images/js_002.png)

其中蓝色代表 js 脚本网络下载时间，红色代表 js 脚本执行，绿色代表 html 解析。

## 多个脚本的情况

这里只列举两个脚本的情况：

```
<script src="a.js"></script>
<script src="b.js"></script>
```

没有 defer 或 async 属性，浏览器会立即下载并执行脚本 a.js，在 a.js 脚本执行完成后才会下载并执行脚本 b.js，在脚本下载和执行时页面的处理会停止。

```
<script defer src="a.js"></script>
<script defer src="b.js"></script>
```

有了 defer 属性，浏览器会立即下载相应的脚本 a.js 和 b.js，在下载的过程中页面的处理不会停止，等到文档解析完成才会执行这两个脚本。HTML5 规范要求脚本按照它们出现的先后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于 DOMContentLoaded 事件执行。 在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发前执行，因此最好只包含一个延迟脚本。

```
<script async src="a.js"></script>
<script async src="b.js"></script>
```

有了 async 属性，浏览器会立即下载相应的脚本 a.js 和 b.js，在下载的过程中页面的处理不会停止，a.js 和 b.js 哪个先下载完成哪个就立即执行，执行过程中页面处理会停止，但是其他脚本的下载不会停止。标记为 async 的脚本并不保证按照制定它们的先后顺序执行。异步脚本一定会在页面的 load 事件前执行，但可能会在 DOMContentLoaded 事件触发之前或之后执行。