
<!--type=class-->

一个通用的 JavaScript `Error` 对象，它不表示错误发生的具体情况。
`Error` 对象会捕捉一个“堆栈跟踪”，详细说明被实例化的 `Error` 对象在代码中的位置，并可能提供错误的文字描述。

只对于加密，如果在抛出错误时可以使用 `Error` 对象，则会将OpenSSL错误堆栈放入到名为 `opensslErrorStack` 的单独属性中。

所有由 Node.js 产生的错误，包括所有系统的和 JavaScript 的错误都实例化自或继承自 `Error` 类。

