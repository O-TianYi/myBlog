**li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？**

答案：浏览器的默认行为是把 inline 元素（即display：inline-blacok）间的空白字符（空格换行 tab）渲染成一个空格，也就是我们上面的代码

换行后会产生换行字符，而它会变成一个空格，当然空格就占用一个字符的宽度。



解决方案：[参考](https://blog.csdn.net/sjinsa/article/details/70919546)

+ 最简单就是写代码的时候把所有的li都写在一行，不进行换行。

+ 既然是空格占一个字符的宽度，那我们索性就将`<ul>`内的字符尺寸直接设为 0，将下面样式放入样式表，问题解决

```
.wrap ul {
  font-size: 0px;
  li{
  font-size: 12px;
  }
}
```

+ 但是li父级标签字符设置为0在Safari浏览器依然出现空白；

```
.wrap ul {
  letter-spacing: -5px;
}
```

之后记得设置 li 内字符间隔

```
.wrap ul li {
  letter-spacing: normal;//按照当前字体的正常间距确认
}
```

补充：letter-spacing属性为设置恩本字符的间距。



#### 其他类似问题

**display:inline-block 什么时候会显示间隙？**

答案：间隙产生的原因是因为，代码li之间换行或空格会占据一定的位置

推荐解决方法：

父元素中设置 font-size:0或者letter-spaceing:-4px;



**display:inline-block 什么时候不会显示间隙？(携程)**

答案：inline-block 布局的元素在编辑器里写在同一行



**去除 inline-block 元素间间距的方法**

答案：

- 移除空格
- 使用 margin 负值（不推荐）
- 使用 font-size:0
- letter-spacing（推荐）
- word-spacing

 [具体参考]([https://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-%E5%8E%BB%E9%99%A4%E9%97%B4%E8%B7%9D/](https://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-去除间距/))

