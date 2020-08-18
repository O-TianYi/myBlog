[参考](https://juejin.im/post/6844903700733886477)

```
:link {
    color: blue;
}
:visited {
 color: purple;
}
:hover {
    color: red;
}
:active {
    color: orange;
}
```

根据之前的介绍，以上这些选择器的特殊性都是一样的：0,0,1,0。因此他们有相同的权重、来源和特殊性，因此与元素匹配的最后一个选择器才会胜出。

正在 *“点击”* 的 *未访问* 链接可以与其中3个规则匹配 —— `:link`、`:hover`、`:active`，所以按照上面的声明顺序，`:active`将胜出，这可能就是我们所期望的。

假设我们忽略这种常用的顺序，而是按字母顺序排列链接样式，声明样式如下:

```
    :active {
        color: orange;
    }
    :hover {
        color: red;
    }
    :link {
        color: blue;
    }
    :visited {
     color: purple;
    }
复制代码
```

按照这种顺序，任何链接都不会显示 `:hover` 或者 `:active`，因为 `:link` 和 `:visited` 规则后出现。所有链接都必须要么是已访问（`:visited`），要么是未访问（`:link`），所以 `:link` 和 `:visited` 样式总是会覆盖 `:hover` 或者 `:active`。

当然链接样式也可以根据自己的实际需要设定某一种顺序，比如 *link-hover-visited-active* 这样的一个顺序，起到的效果是 **只有未访问的链接会有悬停样式，已访问的链接没有悬停样式**。