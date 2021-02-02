#### 正式环境去除console等打印内容

1、vue.config.js配置

[参考](https://www.jianshu.com/p/96353576a621)

```
const TerserPlugin = require('terser-webpack-plugin')//vue-cli自带，不需要安装
config.optimization.minimizer([new TerserPlugin({
    terserOptions: {
        mangle: true, // 混淆，默认也是开的，mangle也是可以配置很多选项的，具体看后面的链接
        compress: {
            drop_console: true，//传true就是干掉所有的console.*这些函数的调用.
            drop_debugger: true, //干掉那些debugger;
            pure_funcs: ['console.log'] // 如果你要干掉特定的函数比如console.info ，又想删掉后保留其参数中的副作用，那用pure_funcs来处理
        }
    }
})])
```







2、其他方法

(1)使用babel-plugin-transform-remove-console

```
//安装插件
npm install babel-plugin-transform-remove-console --save-dev
```

.babelrc里面配置

```
{
  "plugins": ["transform-remove-console"]
}
```

(2)简单方法-把正式环境的console.log直接换成空函数

```
if(process.env.ENV_NAME ==='prod') {
	if(window){
		window.console.log =function(){};
  	}
}
```

