
在 6.0.0 之前的 Node.js 版本中，`Buffer` 实例是使用 `Buffer` 构造函数创建的，该函数根据提供的参数以不同方式分配返回的 `Buffer`：

* 将数字作为第一个参数传给 `Buffer()`（例如 `new Buffer(10)`）会分配一个指定大小的新建的 `Buffer` 对象。
  在 Node.js 8.0.0 之前，为此类 `Buffer` 实例分配的内存是未初始化的，并且可能包含敏感数据。
  此类 `Buffer` 实例随后必须被初始化，可以使用 [`buf.fill(0)`][`buf.fill()`] 或写满整个 `Buffer`。
  虽然这种行为是为了提高性能，但开发经验表明，创建一个快速但未初始化的 `Buffer` 与创建一个速度更慢但更安全的 `Buffer` 之间需要有更明确的区分。
  从 Node.js 8.0.0 开始，`Buffer(num)` 和 `new Buffer(num)` 将返回已初始化内存的 `Buffer`。
* 传入字符串、数组、或 `Buffer` 作为第一个参数，则会将传入的对象的数据拷贝到 `Buffer` 中。
* 传入 [`ArrayBuffer`] 或 [`SharedArrayBuffer`]，则返回一个与给定的数组 buffer 共享已分配内存的 `Buffer`。

由于 `new Buffer()` 的行为因第一个参数的类型而异，因此当未执行参数验证或 `Buffer` 初始化时，可能会无意中将安全性和可靠性问题引入应用程序。

例如，如果攻击者可以使应用程序接收到数字（实际期望的是字符串），则应用程序可能调用 `new Buffer(100)` 而不是 `new Buffer("100")`，它将分配一个 100 个字节的 buffer 而不是分配一个内容为 `“100”` 的 3 个字节的 buffer。 
这通常可以使用 JSON API 调用。 
由于 JSON 区分数字和字符串类型，因此它允许在天真的应用程序可能期望始终接收字符串的情况下注入数字。 
在 Node.js 8.0.0 之前，100 个字节的 buffer 可能包含任意预先存在的内存数据，因此可能会用于向远程攻击者暴露内存中的机密。 
从 Node.js 8.0.0 开始，由于数据会用零填充，因此不会发生内存暴露。 
但是，其他攻击仍然存在，例如导致服务器分配非常大的 buffer，导致性能下降或内存耗尽崩溃。

为了使 `Buffer` 实例的创建更可靠且更不容易出错，各种形式的 `new Buffer()` 构造函数都已被弃用，且改为单独的 `Buffer.from()`，[`Buffer.alloc()`] 和 [`Buffer.allocUnsafe()`] 方法。

开发者应将 `new Buffer()` 构造函数的所有现有用法迁移到这些新的 API。

* [`Buffer.from(array)`] 返回一个新的 `Buffer`，其中包含提供的八位字节数组的副本。
* [`Buffer.from(arrayBuffer[, byteOffset [, length]])`][`Buffer.from(arrayBuf)`] 返回一个新的 `Buffer`，它与给定的 [`ArrayBuffer`] 共享相同的已分配内存。
* [`Buffer.from(buffer)`] 返回一个新的 `Buffer`，其中包含给定 `Buffer` 的内容的副本。
* [`Buffer.from(string[, encoding])`][`Buffer.from(string)`] 返回一个新的 `Buffer`，其中包含提供的字符串的副本。
* [`Buffer.alloc(size[, fill[, encoding]])`][`Buffer.alloc()`] 返回一个指定大小的新建的的已初始化的 `Buffer`。
  此方法比 [`Buffer.allocUnsafe(size)`][`Buffer.allocUnsafe()`] 慢，但能确保新创建的 `Buffer` 实例永远不会包含可能敏感的旧数据。
  如果 `size` 不是数字，则将会抛出 `TypeError`。
* [`Buffer.allocUnsafe(size)`][`Buffer.allocUnsafe()`] 和 [`Buffer.allocUnsafeSlow(size)`][`Buffer.allocUnsafeSlow()`] 分别返回一个指定大小的新建的未初始化的 `Buffer`。
  由于 `Buffer` 是未初始化的，因此分配的内存片段可能包含敏感的旧数据。
  
如果 `size` 小于或等于 [`Buffer.poolSize`] 的一半，则 [`Buffer.allocUnsafe()`] 返回的 `Buffer` 实例可能是从共享的内部内存池中分配。 
[`Buffer.allocUnsafeSlow()`] 返回的实例则从不使用共享的内部内存池。
  
  
  
  
  

