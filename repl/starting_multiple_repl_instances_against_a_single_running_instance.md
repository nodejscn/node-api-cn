可以在一个Node.js中创建并运行多个REPL的实例。它们共享一个`global`对象但是有独立的
I/O端口。
接下来的一个例子中，给每个独立的REPL提供`stdin`，Unix socket和一个TCP socket。

```js
const net = require('net');
const repl = require('repl');
var connections = 0;

repl.start({
  prompt: 'Node.js via stdin> ',
  input: process.stdin,
  output: process.stdout
});

net.createServer((socket) => {
  connections += 1;
  repl.start({
    prompt: 'Node.js via Unix socket> ',
    input: socket,
    output: socket
  }).on('exit', () => {
    socket.end();
  });
}).listen('/tmp/node-repl-sock');

net.createServer((socket) => {
  connections += 1;
  repl.start({
    prompt: 'Node.js via TCP socket> ',
    input: socket,
    output: socket
  }).on('exit', () => {
    socket.end();
  });
}).listen(5001);
```

从命令行运行这个程序将启动一个stdin REPL。其他REPL客户端将连接到Unix socket和TCP socket。
举个例子，TCP sockets的连接使用`terminal`非常方便，而Unix和TCP sockets的连接使用`socat`非常好。

通过从Unix的socket服务器启动一个REPL而不是从stdin，可以这样连接到一个长期运行的Node.js进程，避免重启。

例程：运行“完整特性”（`terminal`）REPL，从`net.Server`和`net.Socket`的实例，参见：https://gist.github.com/2209310

例程：运行REPL的实例，从curl(1)，参见：https://gist.github.com/2053342

[stream]: stream.html
[`util.inspect()`]: util.html#util_util_inspect_object_options
[`readline.Interface`]: readline.html#readline_class_interface
[`readline.InterfaceCompleter`]: readline.html#readline_use_of_the_completer_function
