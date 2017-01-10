<!-- YAML
added: v0.3.4
-->

Construct a new socket object.

`options` is an object with the following defaults:

```js
{
  fd: null,
  allowHalfOpen: false,
  readable: false,
  writable: false
}
```

`fd` allows you to specify the existing file descriptor of socket.
Set `readable` and/or `writable` to `true` to allow reads and/or writes on this
socket (NOTE: Works only when `fd` is passed).
About `allowHalfOpen`, refer to `createServer()` and `'end'` event.

`net.Socket` instances are [`EventEmitter`][] with the following events:

