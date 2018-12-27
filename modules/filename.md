<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {string}

当前模块的文件名（处理后的绝对路径）。

不一定与命令行中使用的名称一致。

当前模块的目录名可以使用 [`__dirname`] 获取。

例子：

在 `/Users/mjr` 目录下运行 `node example.js`：

```js
console.log(__filename);
// 输出: /Users/mjr/example.js
console.log(__dirname);
// 输出: /Users/mjr
```

假设两个模块 `a` 和 `b`, 其中 `b` 是 `a` 的依赖文件，且目录结构如下：

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

则 `b.js` 中的 `__filename` 会返回 `/Users/mjr/app/node_modules/b/b.js`，`a.js` 中的 `__filename` 会返回 `/Users/mjr/app/a.js`。

