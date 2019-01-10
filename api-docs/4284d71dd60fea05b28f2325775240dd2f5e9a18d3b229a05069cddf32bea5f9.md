
`SystemError` 实例可能附有一个 `info` 属性，其值是一个对象，记录了关于错误情况的更多细节。

`SystemError` 实例提供以下属性：

* `code` {string} 错误代码字符串
* `errno` {number} 系统提供的错误代号
* `message` {string} 系统提供的常人能理解的错误描述
* `syscall` {string} 触发了错误的系统调用的名称
* `path` {Buffer} 当汇报文件系统的错误时，`path` 包含与之有关的文件的路径
* `dest` {Buffer} 当汇报文件系统的错误时，`dest` 包含与之有关的文件目的地的路径（如果存在）

