<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {String}

当前模块的文件名。
这是当前模块文件的解析后的绝对路径。

对于主程序而言，无需与在命令行中使用的文件名相同。

查看 [`__dirname`] 了解当前模块的目录名。

`__filename` 实际上不是一个全局变量，而是每个模块内部的。

例子：

从 `/Users/mjr` 运行 `node example.js`：

```js
console.log(__filename);
// 输出: /Users/mjr/example.js
console.log(__dirname);
// 输出: /Users/mjr
```

给出两个模块：`a` 和 `b`，其中 `b` 是 `a` 的一个依赖，目录结构如下：

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

`b.js` 的 `__filename` 返回 `/Users/mjr/app/node_modules/b/b.js`，`a.js` 的 `__filename` 返回 `/Users/mjr/app/a.js`。

