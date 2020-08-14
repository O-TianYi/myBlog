**css3 有哪些新特性**

答案：

1. 选择器

- E:last-child 匹配父元素的最后一个子元素 E。

- E:nth-child(n)匹配父元素的第 n 个子元素 E。

- E:nth-last-child(n) CSS3 匹配父元素的倒数第 n 个子元素 E。

  

1. RGBA

回答此问题，面试官很可能继续问：rgba()和 opacity 的透明效果有什么不同？rgba()和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有内容的透明度，

而 rgba()只作用于元素的颜色或其背景色。（设置 rgba 透明的元素的子元素不会继承透明效果！）



1. 多栏布局

```
<div class="mul-col">
  <div>
    <h3>新手上路</h3>
    <p>新手专区 消费警示 交易安全 24小时在线帮助 免费开店</p>
  </div>
  <div>
    <h3>付款方式</h3>
    <p>快捷支付 信用卡 余额宝 蚂蚁花呗 货到付款</p>
  </div>
  <div>
    <h3>淘宝特色</h3>
    <p>手机淘宝 旺信 大众评审 B格指南</p>
  </div>
</div>
.mul-col {
  column-count: 3;
  column-gap: 5px;
  column-rule: 1px solid gray;
  border-radius: 5px;
  border: 1px solid gray;
  padding: 10px;
}
```

1. 多背景图

```
/* backgroundimage:url('1.jpg),url('2.jpg') */
```

1. CSS3 word-wrap 属性

```
p.test {
  word-wrap: break-word;
}
```

1. 文字阴影

```
text-shadow: 5px 2px 6px rgba(64, 64, 64, 0.5);
```

1. @font-face 属性

Font-face 可以用来加载字体样式，而且它还能够加载服务器端的字体文件，让客户端显示客户端所没有安装的字体。

```
@font-face {
  font-family: BorderWeb;
  src: url(BORDERW0.eot);
}
@font-face {
  font-family: Runic;
  src: url(RUNICMT0.eot);
}
.border {
  font-size: 35px;
  color: black;
  font-family: "BorderWeb";
}
.event {
  font-size: 110px;
  color: black;
  font-family: "Runic";
}

/* 淘宝网字体使用 */

@font-face {
  font-family: iconfont;
  src: url(//at.alicdn.com/t/font_1465189805_4518812.eot);
}
```

1. 圆角

```
border-radius: 15px;
```

1. 边框图片

CSS3 border-image 属性

1. 盒阴影

```
/* box-shadow: 水平方向的偏移量 垂直方向的偏移量 模糊程度 扩展程度 颜色 是否具有内阴影 */
```

1. 盒子大小

CSS3 box-sizing 属性

1. 媒体查询

CSS3 @media 查询

1. CSS3 动画

@keyframes

```
@keyframes abc {
  from {
    transform: rotate(0);
  }
  50% {
    transform: rotate(90deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

animation 属性

```
/* animation ： name duration timing-function delay interation-count direction play-state */
```

1. 渐变效果

```
background-image: -webkit-gradient(
  linear,
  0% 0%,
  100% 0%,
  from(#2a8bbe),
  to(#fe280e)
);
```

1. CSS3 弹性盒子模型

- 弹性盒子是 CSS3 的一种新的布局模式。
- CSS3 弹性盒（ Flexible Box 或 flexbox），是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。
- 引入弹性盒布局模型的目的是提供一种更加有效的方式来对一个容器中的子元素进行排列、对齐和分配空白空间。

1. CSS3 过渡

```
div {
  transition: width 2s;
  -moz-transition: width 2s; /* Firefox 4 */
  -webkit-transition: width 2s; /* Safari 和 Chrome */
  -o-transition: width 2s; /* Opera */
}
```

1. CSS3 变换

- rotate()旋转
- translate()平移
- scale( )缩放
- skew()扭曲/倾斜
- 变换基点
- 3d 转换