<!-- YAML
added: v0.1.27
-->

<!-- type=var -->
当前模块的文件夹名称. 等同于当前打开文件 [`__filename`][]
的所在文件夹名称[`path.dirname()`][] .
* {string}
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

