<!-- YAML
added: v10.10.0
-->
* `code` {string} 需要编译的函数体。
* `params` {string[]} 包含所有函数参数的字符串数组。
* `options` {Object}
  * `filename` {string} 定义此脚本生成的堆栈跟踪信息中使用的文件名。 **默认:** `''`。
  * `lineOffset` {number} 定义此脚本生成的堆栈跟踪信息中显示的行号偏移量。**默认:** `0`。
  * `columnOffset` {number} 定义此脚本生成的堆栈跟踪中显示的列偏移量。 **默认:** `0`。
  * `cachedData` {Buffer|TypedArray|DataView} 为源码提供一个 `Buffer`、`TypedArray` 或 `DataView` 格式的 V8 代码缓存。
  * `produceCachedData` {boolean} 定义是否需要生成新的缓存数据。**默认:** `false`。
  * `parsingContext` {Object} 编译函数的 [contextified][] (上下文隔离) 的沙箱。
  * `contextExtensions` {Object[]}  包含要在编译时应用的上下文扩展（包装当前范围的对象）的集合的数组。**默认:** `[]`.


将给定的代码编译到提供的上下文/沙箱中（如果没有提供上下文，则使用当前上下文），并返回包装了给定参数的函数。
