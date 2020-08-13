#### 父子间传值

##### bus事件总线的应用场景

+ 适合两个组件之间通信（非父子关系）

```
//main.js
Vue.prototype.$bus = new Vue()


//触发组件A中的事件
methods: {
  todo: function () {
    this.$bus.$emit('todoSth', params);  //params是传递的参数
    //...
  }
}

//在组件B创建的钩子中监听事件---一般在create生命周期获取,最好在组件销毁前清除beforeDestory
created() {//mounted生命周期调用也是可以的
  this.$bus.$on('data', (id) => {  //获取传递的参数并进行操作
      //to do something
  })
},
// 最好在组件销毁前
// 清除事件监听
beforeDestroy () {
  this.$bus.$off('todoSth');
},


$emit， $on， $off 分别来分发、监听、取消监听事件：
然后经常会配合父组件调用子组件的方法来触发：
  mounted(){
     // 1.图片加载完成后的事件监听
     this.$bus.$on('homeitemimagesload',()=>{
     this.$refs.scroll.scroll.refresh()
     })
   },
```

注意：多个组件使用$on接收的时候

```
//c页面
this.$bus.$emit(event)

//b页面
this.$bus.$on(event, () => {
    this.status = 'reserve'
})

//a页面
this.$bus.$on(event, () => {
     this.status = 'buying'
})

这时候this.status是reserve而不是我们想要的buying


正确写法：
this.$bus.$off(event).$on(event, () => {
    this.status = 'reserve'
})

this.$bus.$off(event).$on(event, () => {
    this.status = 'buying'
})
```

