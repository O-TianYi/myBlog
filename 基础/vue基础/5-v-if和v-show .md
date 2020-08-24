**为什么避免 v-if 和 v-for 用在一起**

答案：

当 Vue 处理指令时，v-for 比 v-if 具有更高的优先级（官网说的），这意味着 v-if 将分别重复运行于每个 v-for 循环中。通过 v-if 移动到容器元素，不会再重复遍历列表中的每个值。取而代之的是，我们只检查它一次，且不会在 v-if 为否的时候运算 v-for。







##### v-for维护状态，即添加key的意义

当vue更新使用v-for渲染的元素列表时候，它默认使用“就地更新”策略。如果数据项的顺序被改变，vue将不会移动DOM元素来匹配数据项的顺序，而是就地更新每个元素，并且确保他们在每个索引位置正确渲染。该默认的模式的高效的，但是只适用于不依赖子组件状态或临时DOM状态（例如表单输入值）的列表渲染输出。

因此不采用默认的就地复用模式就需要给每一项提供一个唯一的key来跟踪每个节点的身份，从而重用和重新排序现有元素。







#### 使用v-if控制多个组件显示：

使用v-else-if

```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```







##### key在v-if的作用

没有使用key的时候会复用组件：

```
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address">
</template>

//切换的时候input和label都会被复用，即切换的时候将不会清除用户已经输入的内容，两个模板使用了相同的元素，仅仅是替换了它的placeholder
```

带key则会对相同的key的元素才会进行复用：（独立元素，不复用）

```
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>

//label属性没有key会继续复用，，而每次切换的时候，输入框将被重新渲染
```







### v-show和v-if区别

+ 带有 `v-show` 的元素始终会被渲染并保留在 DOM 中。`v-show` 只是简单地切换元素的 CSS property `display`。注意：`v-show` 不支持 `<template>` 元素
+ `v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建
+ `v-if` 也是**惰性的**：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块
+ `v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换
+ `v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好





