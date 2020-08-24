#### 需求：动态改变class和style的属性



##### 绑定class

**对象语法**

对象形式绑定：可以与普通的class共存，变量true和false控制显示某个class

```
<div v-bind:class="{ active: isActive }"></div>//isActive的true和false来决定显示active这个class

//可以与class共存
<div
  class="static"
  v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>
//渲染的结果为：
<div class="static active"></div>

data: {
  isActive: true,
  hasError: false
}
```

也可以绑定计算属性使用，绑定的是一个对象的时候：(这是一个常用且强大的模式)

```
<div v-bind:class="classObject"></div>

data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```

**数组语法**

```
<div v-bind:class="[activeClass, errorClass]"></div>

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

//渲染为：
<div class="active text-danger"></div>

//三元表达式
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>

//结合对象语法使用
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```

**组件中使用**

```
Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})

<my-component v-bind:class="{ active: isActive }"></my-component>
//渲染为：<p class="foo bar active">Hi</p>

<my-component class="baz boo"></my-component>
//渲染为：<p class="foo bar baz boo">Hi</p>
```





#### 绑定内联样式

**对象语法**

CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

data: {
  activeColor: 'red',
  fontSize: 30
}

//直接绑定对象--常常结合计算属性使用
<div v-bind:style="styleObject"></div>
data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```



**数组语法**

```
<div v-bind:style="[baseStyles, overridingStyles]"></div>
```





**注意点：**

+ ：style使用需要添加浏览器前缀的css的时候，例如tranform。vuejs会自动侦测并添加相应的前缀。