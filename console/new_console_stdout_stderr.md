
* `stdout` {Writable}
* `stderr` {Writable}

使用可写流实例来创建新的 `Console` 对象。
`stdout` 是一个可写流，用于打印日志或输出信息。
`stderr` 用于输出警告或错误。
如果没有提供 `stderr`，则 `stdout` 会被用于 `stderr`。


```js
const output = fs.createWriteStream('./stdout.log');
const errorOutput = fs.createWriteStream('./stderr.log');
// 自定义的简单记录器
const logger = new Console(output, errorOutput);
// 像 console 一样使用
const count = 5;
logger.log('count: %d', count);
// stdout.log 中打印: count 5
```

全局的 `console` 是一个特殊的 `Console` 实例，它的输出会发送到 [`process.stdout`] 和 [`process.stderr`]。
相当于调用：

```js
new Console(process.stdout, process.stderr);
```

