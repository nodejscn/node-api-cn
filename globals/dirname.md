<!-- YAML
added: v0.1.27
-->

<!-- type=var -->

* {String}

当前执行脚本所在的目录名称。

例子，从 `/Users/mjr` 运行 `node example.js`：


```js
console.log(__dirname);
// 输出: /Users/mjr
```

`__dirname` 实际上不是一个全局变量，而是每个模块内部的。

例子，给出两个模块：`a` 和 `b`，其中 `b` 是 `a` 的一个依赖，目录结构如下：

* `/Users/mjr/app/a.js`
* `/Users/mjr/app/node_modules/b/b.js`

`b.js` 的 `__dirname` 返回 `/Users/mjr/app/node_modules/b`，而 `a.js` 的 `__dirname` 返回 `/Users/mjr/app`。

