<!-- YAML
added: v0.8.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/16393
    description: Deprecation warnings are only emitted once for each code.
-->

* `fn` {Function} 要被废弃的函数。
* `msg` {string} 当调用废弃的函数时显示的警告消息。
* `code` {string} 废弃码。 有关代码列表，请参阅[废弃的 API 列][list of deprecated APIs]。
* 返回: {Function} 废弃的函数被包装以发出警告。

`util.deprecate()` 方法以一种标记为已废弃的方式包装 `fn`（可以是函数或类）。


```js
const util = require('util');

exports.obsoleteFunction = util.deprecate(() => {
  // 一些操作。
}, 'obsoleteFunction() 已废弃，使用 newShinyFunction() 代替');
```

当被调用时，`util.deprecate()` 会返回一个函数，这个函数会使用 [`'warning'`] 事件触发一个 `DeprecationWarning`。
默认情况下，警告只在首次被调用时才会被触发并打印到 `stderr`。
警告被触发之后，被包装的函数会被调用。

如果在对 `util.deprecate()` 的多次调用中提供了相同的可选 `code`，则该 `code` 仅触发一次警告。


```js
const util = require('util');

const fn1 = util.deprecate(someFunction, someMessage, 'DEP0001');
const fn2 = util.deprecate(someOtherFunction, someOtherMessage, 'DEP0001');
fn1(); // 使用代码 DEP0001 触发废弃警告。
fn2(); // 不会触发废弃警告，因为它具有相同的代码。
```

如果使用了 `--no-deprecation` 或 `--no-warnings` 命令行标记，或 `process.noDeprecation` 属性在首次废弃警告之前被设为 `true`，则 `util.deprecate()` 方法什么也不做。

如果设置了 `--trace-deprecation` 或 `--trace-warnings` 命令行标记，或 `process.traceDeprecation` 属性被设为 `true`，则废弃的函数首次被调用时会把警告与堆栈追踪打印到 `stderr`。

如果设置了 `--throw-deprecation` 命令行标记，或 `process.throwDeprecation` 属性被设为 `true`，则当废弃的函数被调用时会抛出一个异常。

`--throw-deprecation` 命令行标记和 `process.throwDeprecation` 属性优先于 `--trace-deprecation` 和 `process.traceDeprecation`。
