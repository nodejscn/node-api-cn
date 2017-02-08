<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {String}

所执行的代码的文件名。
这是代码文件的解析后的绝对路径。
对于主程序而言，无需与在命令行中使用的文件名相同。
在模块中此变量的值是模块文件的路径。

例子，从 `/Users/mjr` 运行 `node example.js`：

```js
console.log(__filename);
// 输出: /Users/mjr/example.js
```

`__filename` 实际上不是一个全局变量，而是每个模块内部的。

