
在 Node.js v6.0.0 之前，`Buffer` 实例是通过 `Buffer` 构造函数创建的，它根据参数返回不同的 `Buffer`：

* 传入数值（如 `new Buffer(10)`），则分配一个指定大小的 `Buffer` 对象。
  在 Node.js v8.0.0 之前，分配给这种 `Buffer` 实例的内存是未初始化的，可能包含旧数据。
  这种 `Buffer` 实例随后必须被初始化，可以使用 [`buf.fill(0)`][`buf.fill()`] 或写满这个 `Buffer`。
  虽然这是为了提高性能而有意为之的，但开发经验表明，创建一个快速但未初始化的 `Buffer` 与创建一个慢点但更安全的 `Buffer` 之间需要有更明确的区分。
  从 Node.js v8.0.0 开始， `Buffer(num)` 与 `new Buffer(num)` 将返回已初始化的 `Buffer`。
* 传入字符串、数组、或 `Buffer`，则将传入的数据拷贝到 `Buffer`。
* 传入 [`ArrayBuffer`] 或 [`SharedArrayBuffer`]，则返回一个与传入的对象共享内存的 `Buffer`。

因为 `new Buffer()` 会根据参数的类型而不同，所以如果没有正确地校验传给 `new Buffer()` 的参数、就可能引起安全性与可靠性问题。

为了使 `Buffer` 实例的创建更可靠，`new Buffer()` 构造函数已被废弃，建议使用 `Buffer.from()`、`Buffer.alloc()`、和 `Buffer.allocUnsafe()`。

* [`Buffer.from(array)`] 返回一个 `Buffer`，包含传入的字节数组的拷贝。
* [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuf)`] 返回一个 `Buffer`，与传入的 `ArrayBuffer` 共享内存。
* [`Buffer.from(buffer)`] 返回一个 `Buffer`，包含传入的 `Buffer` 的内容的拷贝。
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`] 返回一个 `Buffer`，包含传入的字符串的拷贝。
* [`Buffer.alloc(size[, fill[, encoding]])`][`Buffer.alloc()`] 返回一个指定大小且已初始化的 `Buffer`。
  该方法比 `Buffer.allocUnsafe(size)` 慢，但能确保新创建的 `Buffer` 不会包含旧数据。
* [`Buffer.allocUnsafe(size)`][`Buffer.allocUnsafe()`] 与 [`Buffer.allocUnsafeSlow(size)`][`Buffer.allocUnsafeSlow()`] 返回一个指定大小但未初始化的 `Buffer`。
  因为 `Buffer` 是未初始化的，可能包含旧数据。

