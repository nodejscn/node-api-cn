<!-- YAML
added: v8.1.0
-->

* `socket` {net.Socket}

Called when `socket` is detached from a request and could be persisted by the
Agent. Default behavior is to:

```js
socket.unref();
socket.setKeepAlive(agent.keepAliveMsecs);
```

This method can be overridden by a particular `Agent` subclass. If this
method returns a falsy value, the socket will be destroyed instead of persisting
it for use with the next request.

