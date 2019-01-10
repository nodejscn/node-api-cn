<!-- YAML
added: v0.1.27
-->

<!-- type=var -->

* {string}

当前模块的目录名。相当于 [`__filename`] 的 [`path.dirname()`]。

例子，在 `/Users/mjr` 目录下运行 `node example.js`：

```js
console.log(__dirname);
// 输出: /Users/mjr
console.log(path.dirname(__filename));
// 输出: /Users/mjr
```

