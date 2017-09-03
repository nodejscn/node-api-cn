<!-- YAML
added: v0.0.1
-->

<!-- type=var -->

* {string}

当前模块的文件名称---解析后的绝对路径。

在主程序中这不一定要跟命令行中使用的名称一致。

参阅 [`__dirname`][] 以获取当前模块的目录名称。

例如：

在 `/Users/mjr` 目录下执行 `node example.js` 

```js
console.log(__filename);
// Prints: /Users/mjr/example.js
console.log(__dirname);
// Prints: /Users/mjr
```

给定两个模块： `a` 和 `b`, 其中 `b` 是 `a` 的一个依赖。

文件目录结构如下：

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

`b.js` 中对 `__filename` 的引用将会返回 `/Users/mjr/app/node_modules/b/b.js`
`a.js` 中对 `__filename` 的引用将会返回 `/Users/mjr/app/a.js`
