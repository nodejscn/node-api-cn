<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {string}

当前模块的文件名。
这是当前的模块文件的绝对路径（符号链接会被解析）。

对于主程序，这不一定与命令行中使用的文件名相同。

有关当前模块的目录名，参阅 [`__dirname`]。

示例：

从 `/Users/mjr` 运行 `node example.js`：

```js
console.log(__filename);
// 打印: /Users/mjr/example.js
console.log(__dirname);
// 打印: /Users/mjr
```

给定两个模块：`a` 和 `b`，其中 `b` 是 `a` 的依赖文件，且目录结构如下：

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

`b.js` 中的 `__filename` 的引用会返回 `/Users/mjr/app/node_modules/b/b.js`，而 `a.js` 中的 `__filename` 的引用会返回 `/Users/mjr/app/a.js`。


