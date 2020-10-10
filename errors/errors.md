
<!--introduced_in=v4.0.0-->
<!--type=misc-->

Node.js 应用程序一般会遇到以下四类错误：

- 标准的 JavaScript 错误，例如 {EvalError}、{SyntaxError}、{RangeError}、{ReferenceError}、{TypeError} 或 {URIError}。
- 由底层操作系触发的系统错误，例如试图打开不存在的文件、或试图使用已关闭的 socket 发送数据。
- 由应用程序代码触发的用户自定义的错误。
- `AssertionError` 错误，当 Node.js 检测到不应该发生的异常逻辑时触发。这类错误通常来自 `assert` 模块。

所有由 Node.js 引起的 JavaScript 错误与系统错误都继承自或实例化自标准的 JavaScript {Error} 类，且保证至少提供类中的属性。

