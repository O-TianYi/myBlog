插槽的作用：动态的在某些位置插入不同的标签元素

例如：

```
<navigation-link url="/profile">
  Your Profile,也可以为其他元素标签
</navigation-link>


//navigation-link组件的内容
<a
  v-bind:href="url"
  class="nav-link"
>
  <slot></slot>
</a>


//渲染后
<slot></slot> 将会被替换为“Your Profile”
```

若组件中没有slot元素，则引用该组件的起始标签和结束标签之间的任何内容都会被抛弃。





#### 后备内容

```
<button type="submit">
  <slot>Submit</slot>//即引用的时候没有取代该位置的内容就显示submit
</button>
```

使用：

```
<submit-button></submit-button>

//会不被渲染为：
<button type="submit">
  Submit
</button>
```

```
<submit-button>
  Save
</submit-button>

//渲染
<button type="submit">
  Save
</button>
```







#### 具名插槽（name属性）

```
<slot name="header"></slot>
<slot></slot>//隐含的名字“default"

//使用
<base-layout>
//template的所有内容都会传入对应的插槽
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>
  
  //任何没有被包裹template都会视为默认插槽内容
  <p>A paragraph for the main content.</p>
  <p>And another one.</p>
  
  //默认的准确写法也可以为
   <template v-slot:default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>
  
  
</base-layout>
```

**注意：v-slot只能添加在template上**







#### 作用域插槽

父组件中的插槽内容需要访问子组件中的数据。

```
//组件
<span>
  <slot v-bind:user="user">
    {{ user.lastName }}
  </slot>
</span>


//父组件使用,slotProps为自定义名称，该slotProps为一个对象，是名称为默认的插槽的v-bind的所有数据，
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```



**上面也可以使用解构插槽的方式来**

```
<current-user v-slot="{ user }">
  {{ user.firstName }}
</current-user>

//重命名
<current-user v-slot="{ user: person }">
  {{ person.firstName }}
</current-user>

//带默认值
<current-user v-slot="{ user = { firstName: 'Guest' } }">
  {{ user.firstName }}
</current-user>
```



