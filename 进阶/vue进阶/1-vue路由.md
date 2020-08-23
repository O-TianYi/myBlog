[参考](https://juejin.im/post/6844903647806128135)



vue-router模式：hash、history

vue-router嵌套：父级元素必须有<router-view/>>才能在指定位置显示

<router-link/>和<router-view/>的区别和应用场景：

这两者都是通过引入vuerouter引入的组件。....

路由守卫：作用控制不同用户显示不同的页面，一般使用在判断用户是否登录，登录可以显示某些页面。

+ 全局路由守卫：beforeEach
+ 独自路由守卫：beforeEnter

路由配置：base来决定上下文目录，可以根据该base来控制生产和开发环境





![image-20200823102852832](../../../../../../AppData/Roaming/Typora/typora-user-images/image-20200823102852832.png)







动态路由，后台存储对应的权限

![image-20200823103333605](../../../../../../AppData/Roaming/Typora/typora-user-images/image-20200823103333605.png)









路由源码：[参考](https://juejin.im/post/6844903629804011533)

通过改变current的值来触发render来实现路由的显示。

+ 绑定 `hashchange` 事件，实现前端路由；

+ 将传入的路由和组件做一个路由映射，切换哪个路由即可找到对应的组件显示；

+ 需要 new 一个 Vue 实例还做响应式通信，当路由改变的时候，`router-view` 会响应更新；

+ 注册 `router-link` 和 `router-view` 组件。

```
class VueRouter {
  constructor (Vue, options) {
    this.$options = options;//传递的就是{routes},routes为[]规则
    this.routeMap = {};//映射，根据window.location.hash的路径变化来选择不同的路由组件修改响应式中的current的值
    this.app = new Vue({//实现响应式
      data: {
        current: '#/'//根据current的值来实现对应的组件的render，render的h函数就可以实现对应的节点操作
      }
    });

    this.init();//对hashchange，load进行监听，监听window.location.hash是否 发生改变
    this.createRouteMap(this.$options);//建立映射表
    this.initComponent(Vue);//注册router-link和router-view两个组件
  }

  // 绑定事件
  init () {
    window.addEventListener('load', this.onHashChange.bind(this), false);
    window.addEventListener('hashchange', this.onHashChange.bind(this), false);
  }

  // 路由映射表
  createRouteMap (options) {
    options.routes.forEach(item => {
      this.routeMap[item.path] = item.component;
    });
  }

  // 注册组件
  initComponent (Vue) {
    Vue.component('router-link', {
      props: {
        to: String
      },
      template: '<a :href="to"><slot></slot></a>'
    });

    const _this = this;
    Vue.component('router-view', {
      render (h) {
        var component = _this.routeMap[_this.app.current];
        return h(component);
      }
    });
  }

  // 获取当前 hash 串
  getHash () {
    return window.location.hash.slice(1) || '/';
  }

  // 设置当前路径
  onHashChange () {
    this.app.current = this.getHash();
  }
}

```

将 Vue 与 Hash 路由结合，监听了 `hashchange` 事件，再通过 Vue 的 `响应机制` 和 `组件`，便有了上面实现好了一个 vue-router。





































