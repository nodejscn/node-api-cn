<!-- YAML
added: v0.3.1
changes:
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4777
    description: The `cachedData` and `produceCachedData` options are
                 supported now.
-->

* `code` {string} The JavaScript code to compile.JavaScript要解析的代码。
* `options`
  * `filename` {string} Specifies the filename used in stack traces produced
    by this script.
    定义脚本生成的堆栈跟踪使用的文件名
  * `lineOffset` {number} Specifies the line number offset that is displayed
    in stack traces produced by this script.
    定义脚本生成的堆栈跟踪显示的行号偏移
  * `columnOffset` {number} Specifies the column number offset that is displayed
    in stack traces produced by this script.
    定义脚本生成的堆栈跟踪显示的列号偏移
  * `displayErrors` {boolean} When `true`, if an [`Error`][] error occurs
    while compiling the `code`, the line of code causing the error is attached
    to the stack trace.
    当为真的时候，假如在解析代码的时候发生错误，引起错误的行将会加入堆栈跟踪
  * `timeout` {number} Specifies the number of milliseconds to execute `code`
    before terminating execution. If execution is terminated, an [`Error`][]
    will be thrown.
    定义在终止执行之前执行代码的毫秒数。假如执行终止，将会抛出一个错误。
  * `cachedData` {Buffer} Provides an optional `Buffer` with V8's code cache
    data for the supplied source. When supplied, the `cachedDataRejected` value
    will be set to either `true` or `false` depending on acceptance of the data
    by V8.
    提供一个可选的v8的代码缓存数据Buffer。一旦选择，cachedDataRejected值将会被设为要么
    真要么为假取决于v8接受的数据。
  * `produceCachedData` {boolean} When `true` and no `cachedData` is present, V8
    will attempt to produce code cache data for `code`. Upon success, a
    `Buffer` with V8's code cache data will be produced and stored in the
    `cachedData` property of the returned `vm.Script` instance.
    The `cachedDataProduced` value will be set to either `true` or `false`
    depending on whether code cache data is produced successfully.
    当为真且cachedData存在的时候，v8将会试图去产生代码缓存数据。一旦成功，一个有V8代码
    缓存数据的Buffer将会生成和储存在vm.Script返回的实例的cachedData属性里。
    

Creating a new `vm.Script` object compiles `code` but does not run it. The
compiled `vm.Script` can be run later multiple times. It is important to note
that the `code` is not bound to any global object; rather, it is bound before
each run, just for that run.
创建一个新的vm.Script对象编译代码但是不执行它，编译的vm.Script能够在之后跑几次，很重要代码
不是绑到任何全局对象；相反

