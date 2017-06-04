
* {string|number}

`error.errno` 属性是一个数值或字符串。
如果返回一个数值，则数值是一个负数，对应 [`libuv 错误处理`] 中定义的错误码。
详见 uv-errno.h 头文件（Node.js 源代码中的 `deps/uv/include/uv-errno.h`）。
如果返回一个字符串，则同 `error.code`。

