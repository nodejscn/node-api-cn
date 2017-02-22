<!-- YAML
added: v0.1.27
-->

<!-- type=var -->

* {String}

当前模块的目录名。
等同于 [`__filename`] 的 [`path.dirname()`]。

`__dirname` 实际上不是一个全局变量，而是每个模块内部的。

例子，从 `/Users/mjr` 运行 `node example.js`：


```js
console.log(__dirname);
// 输出: /Users/mjr
console.log(path.dirname(__filename));
// 输出: /Users/mjr
```

