<!-- YAML
added: v10.0.0
-->

`FileHandle` 对象是数字文件描述符的包装器。 
`FileHandle` 的实例与数字文件描述符的不同之处在于它们提供了一个面向对象的 API 来处理文件。

如果没有使用 `filehandle.close()` 方法关闭 `FileHandle`，则它可能会自动关闭文件描述符并触发进程警告，从而有助于防止内存泄漏。 
请不要在代码中依赖此行为，因为它不可靠，且该文件可能无法关闭。 
相反，应该始终显式的关闭 `FileHandles`。 
Node.js 将来可能会改变这种行为。

`FileHandle` 对象的实例由 `fsPromises.open()` 方法在内部创建。

与基于回调的 API（如 `fs.fstat()`、`fs.fchown()`、`fs.fchmod()` 等）不同，基于 promise 的 API 不使用数字文件描述符。 
而是，基于 promise 的 API 使用 `FileHandle` 类，以帮助避免在解决或拒绝 `Promise` 后意外泄漏未关闭的文件描述符。

