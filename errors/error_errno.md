
* {number}

`error.errno` 属性是一个负数，对应 [`libuv 错误处理`][`libuv Error handling`] 中定义的错误码。

在 Windows 上，系统提供的错误码由 libuv 进行规范化。

要获取错误码的字符串表示形式，则使用 [`util.getSystemErrorName(error.errno)`]。


