<!-- YAML
added: v0.3.1
changes:
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/6635
    description: The `breakOnSigint` option is supported now.
-->

* `code` {string} 将被编译和运行的 JavaScript 代码。
* `contextifiedObject` {Object} 一个被[上下文隔离化][contextified]过的对象，会在 `code` 被编译和执行之后充当 `global` 对象。
* `options` {Object|string}
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名。**默认值:** `'evalmachine.<anonymous>'`。
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移。**默认值:** `0`。
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移。**默认值:** `0`。
  * `displayErrors` {boolean} 当值为 `true` 的时候，假如在解析代码的时候发生错误 [`Error`][]，引起错误的行将会被加入堆栈跟踪信息。**默认值:** `true`。
  * `timeout` {integer} 定义在被终止执行之前此 `code` 被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误 [`Error`][]。该值必须是严格正整数。
  * `breakOnSigint` {boolean} 若值为 `true`，当收到 `SIGINT` (Ctrl+C)事件时，代码会被终止执行。
     此外，通过 `process.on('SIGINT')` 方法所设置的消息响应机制在代码被执行时会被屏蔽，但代码被终止后会被恢复。如果执行被终止，一个错误 [`Error`][] 会被抛出。**默认值:** `false`。
  * `cachedData` {Buffer|TypedArray|DataView} 为源码提供一个可选的存有 V8 代码缓存数据的 `Buffer`、`TypedArray` 或 `TypedArray`。
    如果提供了，则 `cachedDataRejected` 的值将会被设为要么为 `true` 要么为 `false`，这取决于 v8 引擎对数据的接受状况。
  * `produceCachedData` {boolean} 当值为 `true` 且 `cachedData` 不存在的时候，V8 将会试图为 `code` 生成代码缓存数据。
    一旦成功，则一个有 V8 代码缓存数据的 `Buffer` 将会被生成和储存在返回的 `vm.Script` 实例的 `cachedData` 属性里。
    `cachedDataProduced` 的值会被设置为 `true` 或者 `false`，这取决于代码缓存数据是否被成功生成。
    不推荐使用此选项，而应该使用 `script.createCachedData()`。**默认值:** `false`。
  * `importModuleDynamically` {Function} 在调用 `import()` 时评估此模块期间调用。 
    如果未指定此选项，则对 `import()` 的调用将拒绝 [`ERR_VM_DYNAMIC_IMPORT_CALLBACK_MISSING`]。 
    此选项是 `--experimental-modules` 标志的实验 API 的一部分，不应被视为稳定。
     * `specifier` {string} 传给 `import()` 的说明符。
     * `module` {vm.Module}
     * 返回: {Module Namespace Object|vm.Module} 返回 `vm.Module` 以利用错误跟踪，并避免出现包含 `then` 函数导出的命名空间问题。
* 返回: {any} 脚本中执行的最后一个语句的结果。

`vm.runInContext()` 方法会编译 `code`，然后在指定的 `contextifiedObject` 的上下文里执行它并返回其结果。
被执行的代码无法获取本地作用域。
`contextifiedObject` 必须是事先被 [`vm.createContext()`] 方法[上下文隔离化][contextified]过的对象。

如果 `options` 是字符串，则它指定文件名。

以下例子使用一个单独的[上下文隔离化][contextified]过的对象来编译并运行几个不同的脚本：

```js
const util = require('util');
const vm = require('vm');

const contextObject = { globalVar: 1 };
vm.createContext(contextObject);

for (let i = 0; i < 10; ++i) {
  vm.runInContext('globalVar *= 2;', contextObject);
}
console.log(util.inspect(contextObject));

// { globalVar: 1024 }
```

