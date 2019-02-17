<!-- YAML
added: v0.1.27
-->

<!-- type=var -->

* {string}

当前模块的目录名。
与 [`__filename`] 的 [`path.dirname()`] 相同。

示例，从 `/Users/mjr` 运行 `node example.js`：

```js
console.log(__dirname);
// 打印: /Users/mjr
console.log(path.dirname(__filename));
// 打印: /Users/mjr
```

