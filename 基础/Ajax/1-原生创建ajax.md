**Ajax 是什么?如何创建一个 Ajax？**

答案：Ajax 全称是 asychronous javascript and xml，可以说是已有技术的组合，主要用来实现客户端与服务器端的异步交互，实现页面的局部刷新。

基本步骤 4 步走：（创建对象、建立连接、发送数据、接收数据）

解析：

```
    1：我要创建一个XMLHttpRequest 对象。
    var xhr=new XMLHttpRequest() 创建对象

    2：我要发送请求，我要跟服务器建立一个连接。

    xhr.open("type 提交方式", "url  提交的地址")

    2.1:如果是post请求，需要设置请求头

    xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");

    3：我要发送数据给服务器。

    如果说是get 请求，请求的数据在地址的后面。
    xhr.send() 发送数据，这一步不能省略

    4：接收服务器的数据。
        服务端返回数据会调用一个回调函数。
        通过回调函数去接收数据.
    xhr.onreadystatechange=function(){
            if(xhr.readyState==4){ 响应完成了
                    if(xhr.status==200){ //响应成功了
                          responseText 属性接收服务端返回的数据.
                    }
            }
    }
```







**创建 ajax 过程**

答案：

1. 创建 XMLHttpRequest 对象,也就是创建一个异步调用对象
2. 创建一个新的 HTTP 请求,并指定该 HTTP 请求的方法、URL 及验证信息
3. 设置响应 HTTP 请求状态变化的函数
4. 发送 HTTP 请求
5. 获取异步调用返回的数据
6. 使用 JavaScript 和 DOM 实现局部刷新