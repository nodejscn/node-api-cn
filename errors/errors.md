
<!--type=misc-->

Node.js 中运行的应用程序一般会遇到以下四类错误：

- 标准的 JavaScript 错误：
  - {EvalError} : 当调用 `eval()` 失败时抛出。
  - {SyntaxError} : 当 JavaScript 语法错误时抛出。
  - {RangeError} : 当值不在预期范围内时抛出。
  - {ReferenceError} : 当使用未定义的变量时抛出。
  - {TypeError} : 当传入错误类型的参数时抛出。
  - {URIError} : 当全局的 URI 处理函数被误用时抛出。
- 由底层操作系触发的系统错误，例如试图打开一个不存在的文件、试图通过一个已关闭的 socket 发送数据等。
- 由应用程序代码触发的用户自定义的错误。
- 断言错误是错误的一个特殊类别，每当 Node.js 检测到一个不应该发生的异常逻辑时触发。
  这类错误通常由 `assert` 模块引起。

所有由 Node.js 引起的 JavaScript 错误与系统错误都继承自或实例化自标准的 JavaScript {Error} 类，且保证至少提供类中的属性。

