<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {string}

当前模块的文件名称。
这是当前的模块文件的符号链接已被解析的绝对路径。

对于一个主程序，这不需要与被用于命令行中的文件名称相同。

查看 [`__dirname`] 获取当前模块的目录名称。

示例：

从 `/Users/mjr` 运行 `node example.js`

```js
console.log(__filename);
// 打印: /Users/mjr/example.js
console.log(__dirname);
// 打印: /Users/mjr
```

给定两个模块：`a` 和 `b`，其中 `b` 是 `a` 的一个依赖，并且有一个如下的目录结构：

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

`b.js` 中的 `__filename` 的引用会返回 `/Users/mjr/app/node_modules/b/b.js`，而 `a.js` 中的 `__filename` 的引用会返回 `/Users/mjr/app/a.js`。


