
在 Node.js v6 之前的版本中，`Buffer` 实例是通过 `Buffer` 构造函数创建的，它根据提供的参数返回不同的 `Buffer`：

* 传一个数值作为第一个参数给 `Buffer()`（如 `new Buffer(10)`），则分配一个指定大小的新建的 `Buffer` 对象。
  在 Node.js 8.0.0 之前，分配给这种 `Buffer` 实例的内存是**没有**初始化的，且**可能包含敏感数据**。
  这种 `Buffer` 实例随后必须被初始化，可以使用 [`buf.fill(0)`] 或写满这个 `Buffer`。
  虽然这种行为是为了提高性能而**有意为之的**，但开发经验表明，创建一个快速但未初始化的 `Buffer` 与创建一个慢点但更安全的 `Buffer` 之间需要有更明确的区分。从 Node.js 8.0.0 开始， `Buffer(num)` 和 `new Buffer(num)` 将返回一个初始化内存之后的 `Buffer`。
* 传一个字符串、数组、或 `Buffer` 作为第一个参数，则将所传对象的数据拷贝到 `Buffer` 中。
* 传入一个 [`ArrayBuffer`]，则返回一个与给定的 [`ArrayBuffer`] 共享所分配内存的 `Buffer`。

因为 `new Buffer()` 的行为会根据所传入的第一个参数的值的数据类型而明显地改变，所以如果应用程序没有正确地校验传给 `new Buffer()` 的参数、或未能正确地初始化新分配的 `Buffer` 的内容，就有可能在无意中为他们的代码引入安全性与可靠性问题。

为了使 `Buffer` 实例的创建更可靠、更不容易出错，各种 `new Buffer()` 构造函数已被 **废弃**，并由 `Buffer.from()`、[`Buffer.alloc()`]、和 [`Buffer.allocUnsafe()`] 方法替代。

**开发者们应当把所有正在使用的 `new Buffer()` 构造函数迁移到这些新的 API 上。**

* [`Buffer.from(array)`] 返回一个新建的包含所提供的字节数组的副本的 `Buffer`。
* [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuffer)`] 返回一个新建的与给定的 [`ArrayBuffer`] 共享同一内存的 `Buffer`。
* [`Buffer.from(buffer)`] 返回一个新建的包含所提供的 `Buffer` 的内容的副本的 `Buffer`。
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`] 返回一个新建的包含所提供的字符串的副本的 `Buffer`。
* [`Buffer.alloc(size[, fill[, encoding]])`][`Buffer.alloc()`] 返回一个指定大小的被填满的 `Buffer` 实例。
  这个方法会明显地比 [`Buffer.allocUnsafe(size)`] 慢，但可确保新创建的 `Buffer` 实例绝不会包含旧的和潜在的敏感数据。
* [`Buffer.allocUnsafe(size)`] 与 [`Buffer.allocUnsafeSlow(size)`] 返回一个新建的指定 `size` 的 `Buffer`，但它的内容**必须**被初始化，可以使用 [`buf.fill(0)`] 或完全写满。

如果 `size` 小于或等于 [`Buffer.poolSize`] 的一半，则 [`Buffer.allocUnsafe()`] 返回的 `Buffer` 实例**可能**会被分配进一个共享的内部内存池。
