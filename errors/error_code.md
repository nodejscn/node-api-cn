
* {string}

`error.code` 属性是标识错误类别的字符标签。
`error.code` 是识别错误的最稳定方法。 
它只会在 Node.js 的主要版本之间更改。 
相反，`error.message` 字符串可能会在 Node.js 的任何版本之间发生变化。
详见 [Node.js 错误码][Node.js Error Codes]关于特定的错误码。
