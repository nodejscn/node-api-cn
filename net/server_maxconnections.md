<!-- YAML
added: v0.2.0
-->

Set this property to reject connections when the server's connection count gets
high.

设置该属性使得当 server 连接数过多时拒绝连接

It is not recommended to use this option once a socket has been sent to a child
with [`child_process.fork()`][].

一旦将一个套接字发送给[`child process.fork()`][]生成的子进程, 不推荐使用该选项.


