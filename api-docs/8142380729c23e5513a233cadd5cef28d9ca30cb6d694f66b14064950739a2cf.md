
像 open(2) 和 read(2) 这样的系统调用定义了用户程序和底层操作系统之间的接口。 
Node.js 函数简单地封装了系统调用，例如 [`fs.open()`]。 
相应的帮助文档描述了系统调用的工作方式。

大多数 Unix 系统调用都有 Windows 等价物，但 Windows 相对于 Linux 和 macOS 的行为可能不同。 
有关在 Windows 上有时无法替换 Unix 系统调用语义的微妙方法的示例，请参阅 Node.js 的[讨论贴](https://github.com/nodejs/node/issues/4760)。

