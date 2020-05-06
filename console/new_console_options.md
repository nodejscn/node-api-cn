<!-- YAML
changes:
  - version: v14.2.0
    pr-url: https://github.com/nodejs/node/pull/32964
    description: The `groupIndentation` option was introduced.
  - version: v11.7.0
    pr-url: https://github.com/nodejs/node/pull/24978
    description: The `inspectOptions` option is introduced.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19372
    description: The `Console` constructor now supports an `options` argument,
                 and the `colorMode` option was introduced.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: The `ignoreErrors` option was introduced.
-->

* `options` {Object}
  * `stdout` {stream.Writable}
  * `stderr` {stream.Writable}
  * `ignoreErrors` {boolean} 在写入底层流时忽略错误。**默认值:** `true`。
  * `colorMode` {boolean|string} 此 `Console` 实例设置颜色支持。
    设置为 `true` 会在检查值时启用着色。
    设置为 `false` 会在检查值时禁用着色。
    设置为 `'auto'` 会使颜色支持取决 `isTTY` 属性的值和 `getColorDepth()` 在相应流上返回的值。
    如果设置了 `inspectOptions.colors`，则不能使用此选项。
    **默认值:** `'auto'`。
  * `inspectOptions` {Object} 指定传给 [`util.inspect()`] 的选项。
  * `groupIndentation` {number} Set group indentation.
    **Default:** `2`.
    
创建具有一个或两个可写流实例的新 `Console`。
`stdout` 是一个可写流，用于打印日志或信息输出。 
`stderr` 用于警告或错误输出。
如果未提供 `stderr`，则 `stdout` 用于 `stderr`。

```js
const output = fs.createWriteStream('./stdout.log');
const errorOutput = fs.createWriteStream('./stderr.log');
// 自定义的简单记录器。
const logger = new Console({ stdout: output, stderr: errorOutput });
// 像控制台一样使用它。
const count = 5;
logger.log('count: %d', count);
// 在 stdout.log 中: count 5
```

全局的 `console` 是一个特殊的 `Console`，其输出发送到 [`process.stdout`] 和 [`process.stderr`]。
相当于调用：


```js
new Console({ stdout: process.stdout, stderr: process.stderr });
```

