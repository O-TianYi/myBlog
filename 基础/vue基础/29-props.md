## [Prop 的大小写 (camelCase vs kebab-case)](https://cn.vuejs.org/v2/guide/components-props.html#Prop-的大小写-camelCase-vs-kebab-case)

HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名：

```
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

重申一次，如果你使用字符串模板，那么这个限制就不存在了。

**注意：**

+ 字符串模板就是在js中写的<template>那些，而平常的.vue文件中写的是非字符串模板。





##### prop类型

```
//一般使用字符串数组形式列出
props: ['title', 'likes', 'isPublished', 'commentIds', 'author']

//指定每个prop的类型的时候，prop就需要以对象的形式显示
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```





#### 静态和动态值的传递

两种方式传入的值都是字符串类型，但实际上任何类型的值都可以传给一个prop

```
//静态值传递---仅仅当传递的数据是字符串的时候不需要v-bind来静态传递值
<blog-post title="My journey with Vue"></blog-post>

<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>
```

**其他特点的传递**

+ 传入一个数字

```

<!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:likes="42"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:likes="post.likes"></blog-post>
```

+ 传入一个布尔值

  ```
  <!-- 包含该 prop 没有值的情况在内，都意味着 `true`。-->
  <blog-post is-published></blog-post>
  
  <!-- 即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post v-bind:is-published="false"></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:is-published="post.isPublished"></blog-post>
  ```

+ 传入一个数组

  ```
  <!-- 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:comment-ids="post.commentIds"></blog-post>
  ```

  

+ 传入一个对象

  ```
  <!-- 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
  <!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
  <blog-post
    v-bind:author="{
      name: 'Veronica',
      company: 'Veridian Dynamics'
    }"
  ></blog-post>
  
  <!-- 用一个变量进行动态赋值。-->
  <blog-post v-bind:author="post.author"></blog-post>
  ```

  

+ 传入一个对象的所有属性

  如果你想要将一个对象的所有 property 都作为 prop 传入，你可以使用不带参数的 `v-bind` (取代 `v-bind:prop-name`)。例如，对于一个给定的对象 `post`：

  ```
  post: {
    id: 1,
    title: 'My Journey with Vue'
  }
  
  <blog-post v-bind="post"></blog-post>
  //该模板等价于
  <blog-post
    v-bind:id="post.id"
    v-bind:title="post.title"
  ></blog-post>
  ```

  



#### prop的类型检查可取值

```
String
Number
Boolean
Array
Object
Date
Function
Symbol
```







**其他注意点**

+ prop为单向数据流，由父组件流向子组件，即父组件的数据变化了，子组件的prop也会跟随变化，反过来则不行

+ 子组件不能修改prop的属性，如果需要修改则子组件重新在data上定义一个属性，然后把prop属性赋给自定义的属性上修改，或者使用computed钩子来修改。但是注意**父组件传递的数组和对象是引用类型的传入给子组件，如果子组件修改，对应的父组件的状态也会发生修改**。因此需要避免修改传递的引用类型的值。

+ prop验证，可以方便知道传递的值的类型，在合作开发的时候，你组件给别人使用的时候就会显得很重要。验证失败控制台会发出警告。**注意prop会在一个组件实例创建之前进行验证，所以实例的属性（例如data、computed等）在default或者validator函数中是不可用的**

  ```
  props: {
      // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
      propA: Number,
      // 多个可能的类型
      propB: [String, Number],
      // 必填的字符串
      propC: {
        type: String,
        required: true
      },
      // 带有默认值的数字
      propD: {
        type: Number,
        default: 100
      },
      // 带有默认值的对象
      propE: {
        type: Object,
        // 对象或数组默认值必须从一个工厂函数获取
        default: function () {//注意--这时候组件实例没有被创建，即data等都不可使用
          return { message: 'hello' }
        }
      },
  ```

  