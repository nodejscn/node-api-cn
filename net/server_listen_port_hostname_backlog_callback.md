<!-- YAML
added: v0.1.90
-->

在特定的`port`和`hostname`开始接受连接. 如果`hostname`被省略，当IPv6可用的时候，服务器将
接受所有的IPv6地址(`::`)或者所有的 IPv4 地址 (`0.0.0.0`)。省略端口参数，或者用的端口值为`0`，
将被操作系统赋予一个任意的端口，这可以在`'listening'`事件被触发后，用`server.address().port`
来获取。

Backlog 是等待连接的队列长度的最大值。实际的长度在Linux上将由操作系统通过系统设置如
`tcp_max_syn_backlog` 和 `somaxconn` 来确定。默认值为511（而不是512）。

这个函数是异步的。网服务器被绑定时，[`'listening'`][]事件被触发。最后一个参数，
`callback`将被加做[`'listening'`][]事件的监听器。

一些用户运行的一个问题是得到`EADDRINUSE`错误。这意味这另一个服务器已经运行在请求的端口。
处理这个问题的一个方式是等待一秒再次尝试运行：

```js
server.on('error', (e) => {
  if (e.code == 'EADDRINUSE') {
    console.log('Address in use, retrying...');
    setTimeout(() => {
      server.close();
      server.listen(PORT, HOST);
    }, 1000);
  }
});
```

(注意: Node.js中所有的socket都被设置为`SO_REUSEADDR`.)

*注意*: `server.listen()`方法可以被多次调用。每个随后的调用将
用提供的参数*重新打开*服务器.

