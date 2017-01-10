<!-- YAML
added: v0.1.99
-->

* `msg` {Buffer} - The message
* `rinfo` {Object} - Remote address information

The `'message'` event is emitted when a new datagram is available on a socket.
The event handler function is passed two arguments: `msg` and `rinfo`. The
`msg` argument is a [`Buffer`][] and `rinfo` is an object with the sender's
address information provided by the `address`, `family` and `port` properties:

```js
socket.on('message', (msg, rinfo) => {
  console.log('Received %d bytes from %s:%d\n',
              msg.length, rinfo.address, rinfo.port);
});
```

