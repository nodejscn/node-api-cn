<!-- YAML
added: v0.1.27
-->

* {string}
<!-- type=var -->
当前模块的文件夹名称。等同于 [`__filename`][] 的 [`path.dirname()`][] 的值。

<!--
The directory name of the current module. This the same as the
[`path.dirname()`][] of the [`__filename`][].
-->
示例：运行位于 `/Users/mjr`目录下的example.js文件：`node example.js`
<!--Example: running `node example.js` from `/Users/mjr`-->

```js
console.log(__dirname);
// Prints: /Users/mjr
console.log(path.dirname(__filename));
// Prints: /Users/mjr
```

