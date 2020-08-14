

### 高级API

#### 实现内容折叠效果：

实现：

````
<details>
<summary>展开查看</summary>
<pre><code>
System.out.println("Hello to see U!");
</code></pre>
</details>
````

预览效果：
<details>
<summary>展开查看</summary>
<pre><code>
System.out.println("Hello to see U!");
</code></pre>
</details>



#### 设置字体、字号与颜色：

代码

```
<font color=#00ffff size=72>color=#00ffff</font>
```

预览效果：

<font color=#00ffff size=72>color=#00ffff</font>





#### 设置背景颜色

代码：需要借助table，tr,td等表格标签的bgcolor属性实现背景颜色功能。

```
<table><tr><td bgcolor=orange>背景色是：orange</td></tr></table>
```

效果：

<table><tr><td bgcolor=orange>背景色是：orange</td></tr></table>





#### 设置分割线，缩紧，换行

代码：分割线一行中使用三个以上的星号、减号都可以；首行缩进两个字符可以使用`&ensp;/&ensp`，一个是半角的空格和全角的空格；换行使用两个以上空格加回车或者使用`<br>`

```
+++/---：分割线
&ensp;/&ensp：缩进
<br>：换行
```

效果：

+++





#### <font color="red">设置链接和图片链接</font>

代码：链接文字使用"[]"来标记，后面紧跟就是该文字的真实链接网址。图片链接就在“[]”前面多一个感叹号。

```
[链接文字](http://example.net/) 点击上面的文字可以跳转某地址.
![图片](图片地址)
```

效果：

[百度](https://baidu.com)啥都不是。

![我是一张图片](https://raw.githubusercontent.com/O-TianYi/picture/master/img/20200813161024.png)