<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: The `ignoreErrors` option was introduced.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19372
    description: The `Console` constructor now supports an `options` argument,
                 and the `colorMode` option was introduced.
-->

* `options` {Object}
  * `stdout` {stream.Writable}
  * `stderr` {stream.Writable}
  * `ignoreErrors` {boolean} 是否在向输出流写数据时忽略错误， **默认为** `true`.
  * `colorMode` {boolean|string} 配置该 `Console` 实例的颜色支持。
    设为 `true` 将会使控制台在检查数据时为其上色，设为 `auto` 会使是否启用颜色取决于 `isTTY` 属性的值和对应的数据流的 `getColorDepth()` 返回的值。**默认为** `auto`。

用一个或两个输出流实例创建一个新的 `Console`。 输出流 `stdout` 用来记录日志和信息；`stderr` 用来记录警告和错误。如果不提供 `stderr`，则 `stdout` 会被用作 `stderr`。

```js
const output = fs.createWriteStream('./stdout.log');
const errorOutput = fs.createWriteStream('./stderr.log');
// custom simple logger
const logger = new Console({ stdout: output, stderr: errorOutput });
// use it like console
const count = 5;
logger.log('count: %d', count);
// in stdout.log: count 5
```

全局符号 `console` 是一个特殊的 `Console` 实例，其输出会被送往 [`process.stdout`][] 和 [`process.stderr`][]。它等价于调用：

```js
new Console({ stdout: process.stdout, stderr: process.stderr });
```

