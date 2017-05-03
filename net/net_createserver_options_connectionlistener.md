<!-- YAML
added: v0.5.0
-->

创建一个新的服务器。`connectionListener` 参数将一次被用作监听器来监听[`'connection'`][]事件。

`options` 是一个对象，有以下默认属性:

```js
{
  allowHalfOpen: false,
  pauseOnConnect: false
}
```

如果 `allowHalfOpen` 是 `true`, 那么socket不会自动的发送一个FIN包，即使socket的另一端
发送了FIN包。socket变成不可读但是可写的。你应该显式地调用 [`end()`][] 方法。
查看 [`'end'`][]事件获取更多信息。

如果 `pauseOnConnect` 是 `true`, 那么与每个连入的连接的socket将会暂停，
并且不能从其中读取任何数据。这允许将在进程中传递的连接不会被原始进程读取数据。 
为了从暂停的socket中开始读取数据，调用[`resume()`][].

下面有关于响应服务器的一个例子，监听连接的8124端口。

```js
const net = require('net');
const server = net.createServer((c) => {
  // 'connection' listener
  console.log('client connected');
  c.on('end', () => {
    console.log('client disconnected');
  });
  c.write('hello\r\n');
  c.pipe(c);
});
server.on('error', (err) => {
  throw err;
});
server.listen(8124, () => {
  console.log('server bound');
});
```

通过`telnet`来进行测试:

```console
$ telnet localhost 8124
```

为了监听 `/tmp/echo.sock`socket，从倒数第三行起，应改为

```js
server.listen('/tmp/echo.sock', () => {
  console.log('server bound');
});
```

用`nc` 来连接UNIX域socket服务器:

```console
$ nc -U /tmp/echo.sock
```

