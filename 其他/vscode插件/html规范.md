[参考](https://juejin.im/post/6844903870571282445)



#### 注解部分

- 注释内容前后各一个空格字符
- `<!-- S Comment Text -->`表示模块开始
- `<!-- E Comment Text -->`表示模块结束，模块与模块之间相隔一行
- 模块注释内部嵌套模块注释，`<!-- /Comment Text -->`

```
<!-- S Comment Text A -->
<div class="mod_a">

    <div class="mod_b">
        ...
    </div>
    <!-- /mod_b -->

    <div class="mod_c">
    	...
    </div>
    <!-- /mod_c -->

</div>
<!-- E Comment Text A -->

<!-- S Comment Text D -->
<div class="mod_d">
    ...
</div>
<!-- E Comment Text D -->
```

