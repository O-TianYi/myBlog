先本地查看自己的vue-cli版本



参考官方文档[[https://cli.vuejs.org/zh/guide/creating-a-project.html#%E4%BD%BF%E7%94%A8%E5%9B%BE%E5%BD%A2%E5%8C%96%E7%95%8C%E9%9D%A2](https://cli.vuejs.org/zh/guide/creating-a-project.html#使用图形化界面)]





##### cmd窗口键入：

```
vue -V----查看本地脚手架版本号（我的旧版本为2.9.6）

vue uninstall vue-cli -g---卸装旧版本的vue-cli

vue install -g @vue/cli

vue -V----再次查看为4版本即说明安装成功
```



##### 2.9.6版本的会出现的问题：

安装插件时候会出现的问题：（目前遇到的问题）

+ 初始化项目的不同

  ```
  vue init webpack demo----以前版本
  //如果你本地的脚手架为大于等于3版本的时候使用以上命令会提示安装一个桥接工具
  npm install -g @vue/cli-init
  # `vue init` 的运行效果将会跟 `vue-cli@2.x` 相同
  vue init webpack my-project
  
  
  vue create demo1----最新安装方式
  ```

  生成的项目的文件夹会不同：

  ![image-20200808174527458](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808174527458.png)

+ 如果是脚手架版本为2.9.6的时候，你安装的less-loader和sass-loader的版本必须为低版本，否则会报错。例如报错原因：this.getResolve is not a function，解决就需要安装低版本的加载器，npm install sass-loader@7.3.1 -D

  



##### 图形化界面安装插件

新版本的vue脚手架可以在命令窗口使用`vue ui`启动图形化界面来安装自己需要的插件：

![image-20200808175433706](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808175433706.png)

然后就会自动浏览器显示下面所示图形化界面，可以在该界面进行项目的创建，导入（安装插件）

![image-20200808175457886](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808175457886.png)

+ **项目创建：**（效果和`vue create demo`一致）

  ![](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808175830059.png)

![image-20200808180023043](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808180023043.png)

![image-20200808180109587](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808180109587.png)

创建成功自动进入进入项目界面。

+ **导入插件：**（直接搜索安装）

  ![image-20200808180244554](C:\Users\OTY\AppData\Roaming\Typora\typora-user-images\image-20200808180244554.png)





#### vue-cli2.x和3.x的区别和不同

+ 打包方式

  ```
  2.0：npm run dev
  3.0: npm run serve
  ```

+ 文件夹目录

  ```
  3.0取消了config目录、build目录、static目录，最重要一点的是，3.0的安装项目时自动下载node-model，3.0的vue.config.js文件需要自己创建，需要在vue.confog.js进行跨域等配置。
  3.0的public变成2.0的static文件夹，不需要解压的文件可以放入该文件夹中
  ```

+ 创建方式

  ```
  2.0: vue init webpack demo 
  3.0: vue create demo
  ```

  

+ 安装插件方式

  ```
  2.0: npm i element-ui -S
  3.0: vue add element-ui(推荐，也可以使用npm)
  ```

  