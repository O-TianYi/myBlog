**.去除数组重复成员的方法**

答案：

方法 1 扩展运算符和 Set 结构相结合，就可以去除数组的重复成员

```
// 去除数组的重复成员
[...new Set([1, 2, 2, 3, 4, 5, 5])];
// [1, 2, 3, 4, 5]
```

方法 2

```
function dedupe(array) {
  return Array.from(new Set(array));
}
dedupe([1, 1, 2, 3]); // [1, 2, 3]
```

方法 3（ES5）

```
function unique(arry) {
  const temp = [];
  arry.forEach(e => {
    if (temp.indexOf(e) == -1) {
      temp.push(e);
    }
  });

  return temp;
}
```









**去除字符串里面的重复字符**

答案：

最简单的方式

```
[...new Set("ababbc")].join(""); // "abc"
```



