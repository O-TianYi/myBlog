

## position:sticky

[参考](https://juejin.im/post/6844904087486464007)

**什么是sticky**

+ 在目标区域以内，它的行为就像 position:relative;在滑动过程中，某个元素距离其父元素的距离达到sticky粘性定位的要求时(比如top：100px)；position:sticky这时的效果相当于fixed定位，固定到适当位置。

+ 可以说是相对定位relative和固定定位fixed的结合

+ 元素固定的相对偏移是相对于离它最近的具有滚动框的祖先元素，如果祖先元素都不可以滚动，那么是相对于viewport来计算元素的偏移量。



**使用条件**

1.父元素不能overflow:hidden或者overflow:auto属性。
2.必须指定top、bottom、left、right4个值之一，否则只会处于相对定位
3.父元素的高度不能低于sticky元素的高度
4、sticky元素仅在其父元素内生效



**例子：**

- css代码

```
.tab-control{
  position: sticky;
  top: 44px;
}
复制代码
```

- html区域

```
<tab-control class="tab-control" :titles="['流行','新款','精选']"></tab-control>
```

当鼠标下滑到一定高度时，触发position:sticky定位的要求，让“流行，新款，精选”固定为距离顶部44px的地方



**注意的坑**

1.sticky不会触发BFC，

2.z-index无效，

3.当父元素的height：100%时，页面滑动到一定高度之后sticky属性会失效。

4.IE低版本不支持sticky的使用






