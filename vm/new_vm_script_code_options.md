<!-- YAML
added: v0.3.1
changes:
  - version: v10.6.0
    pr-url: https://github.com/nodejs/node/pull/20300
    description: The `produceCachedData` is deprecated in favour of
                 `script.createCachedData()`.
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4777
    description: The `cachedData` and `produceCachedData` options are
                 supported now.
-->

* `code` {string} 需要被解析的 JavaScript 代码。
* `options` {Object|string}
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名。**默认值:** `'evalmachine.<anonymous>'`。
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移。**默认值:** `0`。
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移。**默认值:** `0`。
  * `cachedData` {Buffer|TypedArray|DataView} 为源码提供一个可选的存有 V8 代码缓存数据的 `Buffer`、`TypedArray` 或 `TypedArray`。
    如果提供了，则 `cachedDataRejected` 的值将会被设为要么为 `true` 要么为 `false`，这取决于 v8 引擎对数据的接受状况。
  * `produceCachedData` {boolean} 当值为 `true` 且 `cachedData` 不存在的时候，V8 将会试图为 `code` 生成代码缓存数据。
    一旦成功，则一个有 V8 代码缓存数据的 `Buffer` 将会被生成和储存在返回的 `vm.Script` 实例的 `cachedData` 属性里。
    `cachedDataProduced` 的值会被设置为 `true` 或者 `false`，这取决于代码缓存数据是否被成功生成。
    不推荐使用此选项，而应该使用 `script.createCachedData()`。**默认值:** `false`。
  * `importModuleDynamically` {Function} 在调用 `import()` 时评估此模块期间调用。 
    如果未指定此选项，则对 `import()` 的调用将拒绝 [`ERR_VM_DYNAMIC_IMPORT_CALLBACK_MISSING`]。 
    此选项是实验的模块的 API 的一部分，不应被视为稳定。
     * `specifier` {string} 传给 `import()` 的说明符。
     * `module` {vm.Module}
     * 返回: {Module Namespace Object|vm.Module} 返回 `vm.Module` 以利用错误跟踪，并避免出现包含 `then` 函数导出的命名空间问题。
    
如果 `options` 是字符串，则它指定文件名。

创建一个新的 `vm.Script` 对象只编译 `code` 但不会执行它。
编译过的 `vm.Script` 此后可以被多次执行。
`code` 是不绑定于任何全局对象的，相反，它仅仅绑定于每次执行它的对象。

