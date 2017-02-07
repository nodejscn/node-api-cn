
<!--type=misc-->

Node.js 有些模块会被编译成二进制。
这些模块别的地方有更详细的描述。

核心模块定义在 Node.js 源代码的 `lib/` 目录下。

`require()` 总是会优先加载核心模块。
例如，`require('http')` 始终返回内置的 HTTP 模块，即使有同名文件。

