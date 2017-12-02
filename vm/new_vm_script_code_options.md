<!-- YAML
added: v0.3.1
changes:
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4777
    description: 新增对`cachedData`和`produceCachedData`选项的支持

-->

* `code` {string} 需要被解析的JavaScript代码
* `options`
  * `filename` {string} 定义供脚本生成的堆栈跟踪信息所使用的文件名
  * `lineOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的行号偏移
  * `columnOffset` {number} 定义脚本生成的堆栈跟踪信息所显示的列号偏移
  * `displayErrors` {boolean} 当值为真的时候，假如在解析代码的时候发生错误[`Error`][]，引起错误的行将会被加入堆栈跟踪信息
  * `timeout` {number} 定义在被终止执行之前此code被允许执行的最大毫秒数。假如执行被终止，将会抛出一个错误[Error][]。
  * `cachedData` {Buffer} 为源码提供一个可选的存有v8代码缓存数据的Buffer。一旦提供了此Buffer，取决于v8引擎对Buffer中数据的接受状况，cachedDataRejected值将会被设为要么
    真要么为假。
  * `produceCachedData` {boolean} 当值为真且cachedData不存在的时候，v8将会试图为code生成代码缓存数据。一旦成功，一个有V8代码缓存数据的Buffer将会被生成和储存在vm.Script返回的实例的cachedData属性里。
    取决于代码缓存数据是否被成功生成，cachedDataProduced的值会被设置为true或者false。
    
创建一个新的vm.Script对象只编译代码但不会执行它。编译过的vm.Script此后可以被多次执行。值得注意的是，code是不绑定于任何全局对象的，相反，它仅仅绑定于每次执行它的对象。

