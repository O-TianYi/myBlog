#### mixin

#### 含义

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。





##### 应用场景

在不同的组件中经常会需要用到一些相同或者相似的代码，这些代码的功能相对独立。这时，可以通过vue的mixin功能将相同或者相似的代码提取，这样既方便复用也方便维护。

在vue中使用就是提取一些钩子函数的公共方法，或者data上的公共数据。也可以将功能相对独立的代码提取出来，进行单独的维护，多处复用。





##### 基础使用方法

+ src/mixin/demo.js定义混入对象：（一般为方法的复用，即create，method等）

  ```
  export default {
      data(){
        return {
          msg:"这是mixin的数据",
          mixinMsg:"这是mixin的数据",
        }
      },
      created(){
        console.log(123)
      },
      methods:{
        onClick(){
          console.log('触发了mixin中的onClick')
        }
      }
  }
  ```

+ 在组件中引入并使用，组件中只使用mixin

  ```
  <template>
    <div class='container'>
      <div>{{msg}}</div>
      <div>{{mixinMsg}}</div>
      <div @click="onClick"> 点一下 </div>
    </div>
  </template>
  
  <script>
  import mixin from '@/mixin/demo.js';
  export default {
    mixins:[mixin],//直接当做data挂载的数据和方法使用
  }
  </script>
  ```

+ 当组件中定义的内容和mixin对象的内容发生冲突的时候，

  ```
  <template>
    <div class='container'>
      <div>{{msg}}</div>
      <div>{{mixinMsg}}</div>
      <div @click="onClick"> 点一下 </div>
    </div>
  </template>
  
  <script>
  import mixin from '@/mixin/demo.js';
  export default {
    mixins:[mixin],
    data () {
      return {
        msg: '组件中的数据'//和mixin冲突的数据----组件属性有效
      }
    },
    created(){//冲突的生命周期函数-----先触发mixin后触发组件
      console.log('组件内的created')
    },
    methods: {
      onClick(){//冲突的方法----组件中有效
        console.log('触发了组件中的onClick')
      }
    },
  }
  </script>
  ```

  结果：

  + data上的属性（data上的属性或者methods等属性）发生冲突的时候，会以组件中的数据优先，类似java的重写某方法那样。
  + 同名钩子会被合并为一个数组，会依次调用，混合对象的钩子函数将在组件滋生钩子函数之前调用，例如先执行混入的create方法后执行对应组件中的create方法。
  + 值为对象的选项，例如methods，components等将被合并为同一个对象。即methods等方法和mixin冲突会优先为组件中的方法。



##### 全局混入

在初始化vue之前调用vue.mixin()进行全局混入，需要格外小心，一旦使用全局混入，它将影响每一个之后创建的vue实例。

```
Vue.mixin({
  data(){
    return {
      $_globalMsg:"全局mixin数据"
    }
  },
  created(){
    console.log('触发全局mixin的Created')
  },
  methods:{
    $_globalMixin(){
      console.log('$_globalMixin')
    }
  }
})
```

注意：全局混入会影响每个vue的实例（(包括第三方组件）。即全局混入会导致你不想混入的实例也会被混入。局部混入的时候也需要注意定义的变量名不要重复，经常使用特殊符号作为开头，例如$_。



##### 优先级

当全局mixin，局部mixin和组件实例中存在冲突： **组件 > 局部mixin > 全局mixin**







##### 官网分析混入

混入是一种分发Vue组件中的可复用功能的方式。一个混入对象可以包含任意组件选项。当组件使用混入对象时候，所有混入对象的选项将被“混合“进入该组件本身的选项。



