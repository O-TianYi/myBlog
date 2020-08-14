**1.简述一下你对 HTML 语义化的理解？**

正确的标签做正确的事情、内容结构化、结构清晰、利于SEO、便于阅读维护理解。



**2.Label 的作用是什么？是怎么用的？**

答案：label 标签来定义表单控制间的关系,**当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上**。

解析：两种用法：**一种是 id 绑定，一种是嵌套**

```
<label for="Name">Number:</label>

<input type=“text“name="Name" id="Name"/>

<label>Date:<input type="text" name="B"/></label>
```

