**Vue 中如何实现 proxy 代理？**

答案：

webpack 自带的 devServer 中集成了 http-proxy-middleware。配置 devServer 的 proxy 选项即可

```
proxyTable: {
   '/api': {
    target: 'http://192.168.149.90:8080/', // 设置你调用的接口域名和端口号
    changeOrigin: true,   // 跨域
    pathRewrite: {
     '^/api': '/'
    }
   }
  }
```