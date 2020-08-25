vue的**渲染函数**中使用的render，返回的就是VNode

```
render: function (createElement) {
  return createElement('h1', this.blogTitle)
}
```

createElement更准确说是createNodeDescription，主要高速vue页面上需要渲染什么样的节点，包括及其子节点的描述信息。这些节点就是虚拟节点（VNode）





