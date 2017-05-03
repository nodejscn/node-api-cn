<!-- YAML
added: v0.1.90
-->

* `path` {String}
* `backlog` {Number}
* `callback` {Function}

在给定的`path`路径上，开启一个监听连接的本地socket服务器。


这个函数是异步的. 当服务器被已经绑定时[`'listening'`][] 事件将被触发。最后一个参数
`callback` 将被添加为[`'listening'`][]事件的监听器.

在UNIX上, 本地域通常被称为UNIX域. 路径是文件系统路径名。
它被截断至`sizeof(sockaddr_un.sun_path)`个字节，减去一。
它根据操作系统的不同，在91和107个字节之间变动。典型的值为在Linux上
为107，在OS X上为103.路径遵循相同的命名规则和权限检查，这会在文件生成的时候进行，
可以在文件系统中可视，并且*直到不连接的时候才被允许*。

在Windows系统上，本地域用具名管道实现。路径*必须*是`\\?\pipe\`或`\\.\pipe\`的入口。
任何字符都是允许的，但是有一些处理可能会影响管道的名字，例如解析`..`序列。
无论表现如何，管道命名空间是平的。管道*不允许*被移除，当他们的最后一个引用被关闭的时候。
不要忘记JavaScript字符串转义需要路径用双斜线，例如

```js
net.createServer().listen(
    path.join('\\\\?\\pipe', process.cwd(), 'myctl'));
```

`backlog`参数表现地跟
[`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host, backlog, callback)`]一样。

*注意*: `server.listen()`方法可以被多次调用。每个随后的调用将
用提供的参数*重新打开*服务器.

