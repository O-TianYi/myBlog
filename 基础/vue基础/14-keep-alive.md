**vue 中 keep-alive 组件的作用**

答案：keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，或避免重新渲染。

解析：

用法也很简单：

```
<keep-alive>
  <component>
    <!-- 该组件将被缓存！ -->
  </component>
</keep-alive>
```

props属性有：

include - 字符串或正则表达，只有匹配的组件会被缓存 

exclude - 字符串或正则表达式，任何匹配的组件都不会被缓存

```
// 组件 a
export default {
  name: "a",
  data() {
    return {};
  }
};
<keep-alive include="a">
  <component>
    <!-- name 为 a 的组件将被缓存！ -->
  </component> </keep-alive
>可以保留它的状态或避免重新渲染
<keep-alive exclude="a">
  <component>
    <!-- 除了 name 为 a 的组件都将被缓存！ -->
  </component> </keep-alive
>可以保留它的状态或避免重新渲染
```

但实际项目中,需要配合 vue-router 共同使用.

router-view 也是一个组件，如果直接被包在 keep-alive 里面，所有路径匹配到的视图组件都会被缓存：

```
<keep-alive>
  <router-view>
    <!-- 所有路径匹配到的视图组件都会被缓存！ -->
  </router-view>
</keep-alive>
```

如果只想 router-view 里面某个组件被缓存，怎么办？

增加 router.meta 属性

```
// routes 配置
export default [
  {
    path: "/",
    name: "home",
    component: Home,
    meta: {
      keepAlive: true // 需要被缓存
    }
  },
  {
    path: "/:id",
    name: "edit",
    component: Edit,
    meta: {
      keepAlive: false // 不需要被缓存
    }
  }
];
<keep-alive>
    <router-view v-if="$route.meta.keepAlive">
        <!-- 这里是会被缓存的视图组件，比如 Home！ -->
    </router-view>
</keep-alive>

<router-view v-if="!$route.meta.keepAlive">
    <!-- 这里是不被缓存的视图组件，比如 Edit！ -->
</router-view>
```







#### 官网重新学习的解析

作用：组件之间切换的时候，有时想保持这些组件的状态，以避免反复渲染导致的性能问题。

使用：

```
<!-- 失活的组件将会被缓存！-->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>
```

注意：keep-alive要求被切换到的组件都有自己的名字，不论是通过组件的name选项还是局部、全局注册。

