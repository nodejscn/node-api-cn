
It is possible to create and run multiple REPL instances against a single
running instance of Node.js that share a single `global` object but have
separate I/O interfaces.

The following example, for instance, provides separate REPLs on `stdin`, a Unix
socket, and a TCP socket:

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

Running this application from the command line will start a REPL on stdin.
Other REPL clients may connect through the Unix socket or TCP socket. `telnet`,
for instance, is useful for connecting to TCP sockets, while `socat` can be used
to connect to both Unix and TCP sockets.

By starting a REPL from a Unix socket-based server instead of stdin, it is
possible to connect to a long-running Node.js process without restarting it.

For an example of running a "full-featured" (`terminal`) REPL over
a `net.Server` and `net.Socket` instance, see: https://gist.github.com/2209310

For an example of running a REPL instance over curl(1),
see: https://gist.github.com/2053342

[stream]: stream.html
[`util.inspect()`]: util.html#util_util_inspect_object_options
[`readline.Interface`]: readline.html#readline_class_interface
[`readline.InterfaceCompleter`]: readline.html#readline_use_of_the_completer_function
