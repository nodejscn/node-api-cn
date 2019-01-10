<!-- YAML
added: v0.8.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/16393
    description: Deprecation warnings are only emitted once for each code.
-->

* `fn` {Function} The function that is being deprecated.
* `msg` {string} A warning message to display when the deprecated function is
  invoked.
* `code` {string} A deprecation code. See the [list of deprecated APIs][] for a
  list of codes.
* Returns: {Function} The deprecated function wrapped to emit a warning.

`util.deprecate()` 方法会包装给定的 `function` 或类，并标记为废弃的。


```js
const util = require('util');

exports.obsoleteFunction = util.deprecate(() => {
  // Do something here.
}, 'obsoleteFunction() is deprecated. Use newShinyFunction() instead.');
```

当被调用时，`util.deprecate()` 会返回一个函数，这个函数会使用 `process.on('warning')` 事件触发一个 `DeprecationWarning`。
默认情况下，警告只在首次被调用时才会被触发并打印到 `stderr`。
警告被触发之后，被包装的 `function` 会被调用。


```js
const util = require('util');

const fn1 = util.deprecate(someFunction, someMessage, 'DEP0001');
const fn2 = util.deprecate(someOtherFunction, someOtherMessage, 'DEP0001');
fn1(); // emits a deprecation warning with code DEP0001
fn2(); // does not emit a deprecation warning because it has the same code
```

如果使用了 `--no-deprecation` 或 `--no-warnings` 命令行标记，或 `process.noDeprecation` 属性在首次废弃警告之前被设为 `true`，则 `util.deprecate()` 方法什么也不做。

如果设置了 `--trace-deprecation` 或 `--trace-warnings` 命令行标记，或 `process.traceDeprecation` 属性被设为 `true`，则废弃的函数首次被调用时会把警告与堆栈追踪打印到 `stderr`。

如果设置了 `--throw-deprecation` 命令行标记，或 `process.throwDeprecation` 属性被设为 `true`，则当废弃的函数被调用时会抛出一个异常。

`--throw-deprecation` 命令行标记和 `process.throwDeprecation` 属性优先于 `--trace-deprecation` 和 `process.traceDeprecation`。
