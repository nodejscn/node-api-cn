<!-- YAML
added: v0.3.1
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19016
    description: The `contextCodeGeneration` option is supported now.
  - version: v6.3.0
    pr-url: https://github.com/nodejs/node/pull/6635
    description: The `breakOnSigint` option is supported now.
-->

* `code` {string} 将被编译和运行的 JavaScript 代码。
* `sandbox` {Object} 一个将会被[上下文隔离化][contextified]的对象。如果是 `undefined`, 则会生成一个新的对象。
* `options` {Object|string}
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名。**默认值:** `'evalmachine.<anonymous>'`。
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移。**默认值:** `0`。
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移。**默认值:** `0`。
  * `displayErrors` {boolean} 当值为 `true` 的时候，假如在解析代码的时候发生错误 [`Error`][]，引起错误的行将会被加入堆栈跟踪信息。**默认值:** `true`。
  * `timeout` {integer} 定义在被终止执行之前此 `code` 被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误 [`Error`][]。该值必须是严格正整数。
  * `breakOnSigint` {boolean} 若值为 `true`，当收到 `SIGINT` (Ctrl+C)事件时，代码会被终止执行。
     此外，通过 `process.on('SIGINT')` 方法所设置的消息响应机制在代码被执行时会被屏蔽，但代码被终止后会被恢复。如果执行被终止，一个错误 [`Error`][] 会被抛出。**默认值:** `false`。
  * `contextName` {string} 新创建的上下文的人类可读名称。 **默认值:** `'VM Context i'`，其中 `i` 是创建的上下文的升序数字索引。
  * `contextOrigin` {string} 对应于新创建用于显示目的的上下文的[原点][origin]。 
    原点应格式化为类似一个 URL，但只包含协议，主机和端口（如果需要），例如 [`URL`] 对象的 [`url.origin`] 属性的值。 最值得注意的是，此字符串应省略尾部斜杠，因为它表示路径。 **默认值:** `''`。
  * `contextCodeGeneration` {Object}
    * `strings` {boolean} 如果设置为 `false`，则对 `eval` 或函数构造函数（`Function`、`GeneratorFunction` 等）的任何调用都将抛出 `EvalError`。**默认值:** `true`。
    * `wasm` {boolean} 如果设置为 `false`，则任何编译 WebAssembly 模块的尝试都将抛出 `WebAssembly.CompileError`。**默认值:** `true`。
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
     * `module` {vm.SourceTextModule}
     * 返回: {Module Namespace Object|vm.SourceTextModule} 返回 `vm.SourceTextModule` 以利用错误跟踪，并避免出现包含 `then` 函数导出的命名空间问题。
* 返回: {any} 脚本中执行的最后一个语句的结果。

`vm.runInNewContext()` 首先给指定的 `sandbox`（若为 `undefined`，则会新建一个` sandbox`）提供一个隔离的上下文, 再在此上下文中执行编译的 `code`，最后返回结果。
运行中的代码无法获取本地作用域。

如果 `options` 是字符串，则它指定文件名。

以下的例子会编译一段代码，该代码会递增一个全局变量，给另外一个全局变量赋值。同时该代码被编译后会被多次执行。全局变量会被置于 `sandbox` 对象内。

```js
const util = require('util');
const vm = require('vm');

const sandbox = {
  animal: 'cat',
  count: 2
};

vm.runInNewContext('count += 1; name = "kitty"', sandbox);
console.log(util.inspect(sandbox));

// { animal: 'cat', count: 3, name: 'kitty' }
```

