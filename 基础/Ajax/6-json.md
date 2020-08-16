**什么是 json，优缺点**

答案：

JSON (JavaScript Object Notation)

优点:

1. 数据格式比较简单, 易于读写, 格式都是压缩的, 占用带宽小
2. 易于解析这种语言, 客户端 javascript 可以简单的通过 eval()进行 JSON 数据的读取搜索
3. 支持多种语言, 包括 ActionScript, C, C#, ColdFusion, Java, JavaScript, Perl, php, Python, Ruby 等语言服务器端语言, 便于服务器端的解析
4. 在 PHP 世界, 已经有 PHP-JSON 和 JSON-PHP 出现了, 便于 PHP 序列化后的程序直接调用. PHP 服务器端的对象、数组等能够直接生 JSON 格式, 便于客户端的访问提取. 另外 PHP 的 PEAR 类已经提出了支持 (http://pear.php.net/pepr/pepr-proposal-show.php?id=198)
5. 因为 JSON 格式能够直接为服务器端代码使用, 大大简化了服务器端和客户端的代码开发量, 但是完成的任务不变, 且易于维护

缺点:

1. 没有 XML 格式这么推广的深入人心和使用广泛, 没有 XML 那么通用性
2. JSON 格式目前在 Web Service 中推广还属于初级阶段 PS: 据说 Google 的 Ajax 是使用 JSON+模板 做的