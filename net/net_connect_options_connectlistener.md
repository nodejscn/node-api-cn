<!-- YAML
added: v0.7.0
-->

A factory function, which returns a new [`net.Socket`][] and automatically
connects with the supplied `options`.

The options are passed to both the [`net.Socket`][] constructor and the
[`socket.connect`][] method.

The `connectListener` parameter will be added as a listener for the
[`'connect'`][] event once.

Here is an example of a client of the previously described echo server:

```js
const net = require('net');
const client = net.connect({port: 8124}, () => {
  // 'connect' listener
  console.log('connected to server!');
  client.write('world!\r\n');
});
client.on('data', (data) => {
  console.log(data.toString());
  client.end();
});
client.on('end', () => {
  console.log('disconnected from server');
});
```

To connect on the socket `/tmp/echo.sock` the second line would just be
changed to

```js
const client = net.connect({path: '/tmp/echo.sock'});
```

