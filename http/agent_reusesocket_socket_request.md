<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}
* `request` {http.ClientRequest}

Called when `socket` is attached to `request` after being persisted because of
the keep-alive options. Default behavior is to:

```js
socket.ref();
```

This method can be overridden by a particular `Agent` subclass.

